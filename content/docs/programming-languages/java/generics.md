---
weight: 999
title: "Generics"
description: ""
icon: "article"
date: "2026-03-12T13:55:19+00:00"
lastmod: "2026-03-12T13:55:19+00:00"
draft: false
toc: true
---

# Generics, Streams & Lambdas in Java

Ein Uberblick uber drei der wichtigsten modernen Java-Features, die zusammen sehr maechtig werden — besonders beim Arbeiten mit Collections und Datenverarbeitung.

---

## Generics

Generics ermöglichen **typsichere, wiederverwendbare** Klassen, Interfaces und Methoden. Statt mit `Object` zu arbeiten (und ueberall casten zu muessen), gibt man den Typ direkt mit.

### Grundprinzip

```java
// Ohne Generics — unsicher
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0); // expliziter Cast nötig

// Mit Generics — typsicher
List<String> list = new ArrayList<>();
list.add("hello");
String s = list.get(0); // kein Cast nötig
```

### Eigene generische Klasse

```java
public class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

Box<Integer> intBox = new Box<>(42);
Box<String> strBox = new Box<>("Java");
```

### Bounded Type Parameters

Mit `extends` kann man den erlaubten Typ einschraenken:

```java
public <T extends Number> double sum(List<T> list) {
    double total = 0;
    for (T item : list) {
        total += item.doubleValue();
    }
    return total;
}
```

### Wildcards

| Syntax | Bedeutung |
|--------|-----------|
| `<?>` | Unbekannter Typ |
| `<? extends T>` | T oder Subtyp (read-only) |
| `<? super T>` | T oder Supertyp (write-friendly) |

```java
public void printList(List<?> list) {
    for (Object o : list) System.out.println(o);
}
```

> **Meinung:** Wildcards sind anfangs verwirrend — das Prinzip "producer extends, consumer super" (PECS) hilft dabei, die richtige Wahl zu treffen.

---

## Lambdas

Einfuhrung mit **Java 8**. Lambdas sind anonyme Funktionen, die ueberall dort verwendet werden koennen, wo ein **Functional Interface** erwartet wird (Interface mit genau einer abstrakten Methode).

### Syntax

```java
// Vorher: anonyme innere Klasse
Runnable r = new Runnable() {
    public void run() { System.out.println("Hello"); }
};

// Mit Lambda
Runnable r = () -> System.out.println("Hello");
```

### Haeufige Functional Interfaces

| Interface | Signatur | Verwendung |
|-----------|----------|------------|
| `Runnable` | `() -> void` | Threads, Tasks |
| `Supplier<T>` | `() -> T` | Wert liefern |
| `Consumer<T>` | `T -> void` | Wert verbrauchen |
| `Function<T,R>` | `T -> R` | Umwandlung |
| `Predicate<T>` | `T -> boolean` | Filterlogik |
| `BiFunction<T,U,R>` | `(T,U) -> R` | Zwei Inputs |

```java
Predicate<String> isLong = s -> s.length() > 5;
Function<String, Integer> toLength = String::length; // Methodenreferenz
Consumer<String> printer = System.out::println;
```

### Methodenreferenzen

Kurzschreibweise fuer einfache Lambdas:

```java
// Lambda          →   Methodenreferenz
x -> x.toString()    →   Object::toString
x -> list.add(x)     →   list::add
() -> new Foo()      →   Foo::new
```

---

## Streams

Die **Stream API** (Java 8+) ermöglicht deklarative, funktionale Datenverarbeitung auf Collections. Ein Stream ist **lazy** — Operationen werden erst bei einer Terminaloperation ausgefuehrt.

### Stream-Pipeline

```
Quelle → Intermediate Operations (lazy) → Terminal Operation (eager)
```

```java
List<String> names = List.of("Alice", "Bob", "Charlie", "Anna");

List<String> result = names.stream()
    .filter(n -> n.startsWith("A"))    // intermediate
    .map(String::toUpperCase)           // intermediate
    .sorted()                           // intermediate
    .collect(Collectors.toList());      // terminal

// result: ["ALICE", "ANNA"]
```

### Wichtige Intermediate Operations

| Operation | Beschreibung |
|-----------|-------------|
| `filter(Predicate)` | Elemente filtern |
| `map(Function)` | Elemente transformieren |
| `flatMap(Function)` | Nested streams flatten |
| `sorted()` / `sorted(Comparator)` | Sortieren |
| `distinct()` | Duplikate entfernen |
| `limit(n)` / `skip(n)` | Groesse begrenzen / ueberspringen |
| `peek(Consumer)` | Debugging ohne Veraenderung |

### Wichtige Terminal Operations

| Operation | Beschreibung |
|-----------|-------------|
| `collect(Collector)` | In Collection umwandeln |
| `forEach(Consumer)` | Iteration |
| `count()` | Anzahl |
| `reduce(...)` | Aggregation |
| `findFirst()` / `findAny()` | Erstes Element (Optional) |
| `anyMatch` / `allMatch` / `noneMatch` | Boolean-Pruefung |
| `min(Comparator)` / `max(Comparator)` | Extremwerte |

### Collectors

```java
// In List sammeln
List<String> list = stream.collect(Collectors.toList());

// In Map gruppieren
Map<Integer, List<String>> byLength = names.stream()
    .collect(Collectors.groupingBy(String::length));

// Joinen
String joined = names.stream()
    .collect(Collectors.joining(", ", "[", "]"));
// → "[Alice, Bob, Charlie, Anna]"
```

### Numeric Streams

Fuer Primitiv-Typen gibt es spezialisierte Streams: `IntStream`, `LongStream`, `DoubleStream`.

```java
int sum = IntStream.rangeClosed(1, 10).sum(); // 55

OptionalDouble avg = List.of(1, 2, 3, 4, 5).stream()
    .mapToInt(Integer::intValue)
    .average();
```

### Parallel Streams

```java
long count = names.parallelStream()
    .filter(n -> n.length() > 3)
    .count();
```

> **Meinung:** Parallel Streams klingen verlockend, sind aber nicht immer schneller. Bei kleinen Collections oder zustandsabhaengigen Operationen koennen sie sogar langsamer sein. Erst messen, dann optimieren.

---

## Alles zusammen: ein Beispiel

```java
record Person(String name, int age, String city) {}

List<Person> people = List.of(
    new Person("Alice", 30, "Berlin"),
    new Person("Bob", 25, "Munich"),
    new Person("Charlie", 35, "Berlin"),
    new Person("Anna", 28, "Munich")
);

// Alle Berliner, sortiert nach Alter, nur die Namen
List<String> berlinNames = people.stream()
    .filter(p -> p.city().equals("Berlin"))
    .sorted(Comparator.comparingInt(Person::age))
    .map(Person::name)
    .collect(Collectors.toList());

// ["Alice", "Charlie"]

// Durchschnittsalter pro Stadt
Map<String, Double> avgAgeByCity = people.stream()
    .collect(Collectors.groupingBy(
        Person::city,
        Collectors.averagingInt(Person::age)
    ));
```

---

## Zusammenfassung

| Feature | Seit | Kernnutzen |
|---------|------|------------|
| Generics | Java 5 | Typsicherheit & Wiederverwendbarkeit |
| Lambdas | Java 8 | Kompakte, funktionale Ausdruecke |
| Streams | Java 8 | Deklarative Datenverarbeitung |

Die drei Features ergaenzen sich perfekt: Generics machen die Stream-API typsicher, Lambdas machen Stream-Operationen praegnant und lesbar.

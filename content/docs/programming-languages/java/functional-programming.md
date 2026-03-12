---
weight: 999
title: "Functional Programming"
description: ""
icon: "article"
date: "2026-03-12T13:56:21+00:00"
lastmod: "2026-03-12T13:56:21+00:00"
draft: false
toc: true
---

# Funktionale Programmierung in Java

Java ist primär eine objektorientierte Sprache, hat aber seit **Java 8 (2014)** starke funktionale Features erhalten. Seitdem kann man in Java echten funktionalen Stil schreiben — ohne auf externe Libraries angewiesen zu sein.

---

## Kernkonzepte

### 1. Lambda-Ausdrücke

Lambdas sind anonyme Funktionen, die direkt als Argument übergeben werden können.

```java
// Klassisch (anonyme Klasse)
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};

// Mit Lambda
Runnable r = () -> System.out.println("Hello");

// Mit Parameter und Rückgabewert
Comparator<String> comp = (a, b) -> a.compareTo(b);
```

---

### 2. Functional Interfaces

Ein **Functional Interface** hat genau eine abstrakte Methode. Das ist die Basis für Lambdas in Java.

| Interface | Signatur | Beschreibung |
|---|---|---|
| `Function<T, R>` | `T -> R` | Transformation |
| `Consumer<T>` | `T -> void` | Seiteneffekt |
| `Supplier<T>` | `() -> T` | Wert erzeugen |
| `Predicate<T>` | `T -> boolean` | Bedingung prüfen |
| `BiFunction<T, U, R>` | `(T, U) -> R` | Zwei Inputs |

```java
Function<String, Integer> length = String::length;
Predicate<Integer> isEven = n -> n % 2 == 0;
Supplier<List<String>> listFactory = ArrayList::new;
Consumer<String> printer = System.out::println;
```

> **Eigene Functional Interfaces** mit `@FunctionalInterface` annotieren — das gibt Compiler-Schutz.

---

### 3. Method References

Kurzschreibweise für Lambdas, die nur eine Methode aufrufen.

```java
// Statische Methode
Function<String, Integer> parse = Integer::parseInt;

// Instanzmethode auf Objekt
Consumer<String> print = System.out::println;

// Instanzmethode auf Typ
Function<String, String> upper = String::toUpperCase;

// Konstruktor
Supplier<ArrayList<String>> create = ArrayList::new;
```

---

### 4. Streams API

Die Stream API ist das Herzstück der funktionalen Java-Programmierung. Sie ermöglicht deklarative Verarbeitung von Datenmengen.

```java
List<String> names = List.of("Anna", "Bob", "Clara", "David", "Eva");

List<String> result = names.stream()
    .filter(name -> name.length() > 3)     // Predicate
    .map(String::toUpperCase)               // Function
    .sorted()                               // Zwischenoperation
    .collect(Collectors.toList());          // Terminaloperation

// result: [ANNA, CLARA, DAVID]
```

**Wichtige Stream-Operationen:**

```java
// map — Transformation
stream.map(x -> x * 2)

// flatMap — Verschachtelte Streams flatten
stream.flatMap(list -> list.stream())

// filter — Filtern
stream.filter(x -> x > 0)

// reduce — Aggregation
stream.reduce(0, Integer::sum)

// collect — In Datenstruktur sammeln
stream.collect(Collectors.groupingBy(String::length))

// forEach — Seiteneffekt (kein Rückgabewert)
stream.forEach(System.out::println)
```

---

### 5. Optional

`Optional<T>` vermeidet `NullPointerException` und zwingt zum expliziten Umgang mit fehlenden Werten.

```java
Optional<String> name = Optional.of("Alice");

// Klassisches Null-Checking vs. funktional
String upper = name
    .filter(n -> n.length() > 3)
    .map(String::toUpperCase)
    .orElse("UNKNOWN");
```

> **Meinung:** Optional sollte primär als Rückgabetyp verwendet werden, nicht als Methodenparameter oder Feldtyp — das ist in der Community breiter Konsens.

---

### 6. Function Composition

Funktionen lassen sich kombinieren mit `andThen` und `compose`.

```java
Function<Integer, Integer> times2 = x -> x * 2;
Function<Integer, Integer> plus3  = x -> x + 3;

// andThen: erst times2, dann plus3
Function<Integer, Integer> times2ThenPlus3 = times2.andThen(plus3);
times2ThenPlus3.apply(5); // (5 * 2) + 3 = 13

// compose: erst plus3, dann times2
Function<Integer, Integer> composed = times2.compose(plus3);
composed.apply(5); // (5 + 3) * 2 = 16
```

---

## Praktisches Beispiel: Datenpipeline

```java
record Person(String name, int age, String city) {}

List<Person> people = List.of(
    new Person("Alice", 30, "Berlin"),
    new Person("Bob", 17, "Hamburg"),
    new Person("Clara", 25, "Berlin"),
    new Person("David", 16, "München")
);

Map<String, List<String>> adultsByCity = people.stream()
    .filter(p -> p.age() >= 18)
    .collect(Collectors.groupingBy(
        Person::city,
        Collectors.mapping(Person::name, Collectors.toList())
    ));

// {Berlin=[Alice, Clara], Hamburg=[Bob]}
```

---

## Immutability & Pure Functions

Funktionale Programmierung bevorzugt **unveränderliche Daten** und **reine Funktionen** (kein globaler State, gleicher Input = gleicher Output).

```java
// Nicht funktional — mutiert Zustand
List<Integer> numbers = new ArrayList<>(List.of(1, 2, 3));
numbers.add(4); // Seiteneffekt!

// Funktional — neue Liste erzeugen
List<Integer> extended = Stream.concat(
    numbers.stream(),
    Stream.of(4)
).collect(Collectors.toUnmodifiableList());
```

Java Records (seit Java 16) helfen bei Immutability:

```java
record Point(int x, int y) {
    Point translate(int dx, int dy) {
        return new Point(x + dx, y + dy); // neues Objekt, unveraendert
    }
}
```

---

## Wann funktional, wann OOP?

| Situation | Empfehlung |
|---|---|
| Datentransformationen, Pipelines | Funktional (Streams) |
| Komplexe Businesslogik mit State | OOP |
| Null-sichere Rückgabewerte | Optional |
| Callbacks, Event-Handler | Lambdas / Functional Interfaces |
| Unveraenderliche Datenobjekte | Records + Immutable Collections |

> **Meinung:** Java ist keine rein funktionale Sprache und das ist okay. Der Sweet Spot liegt im Mix: OOP fuer die Struktur, funktionale Stile fuer Datenverarbeitung und Transformationen. Wer voll-funktional in der JVM unterwegs sein will, sollte einen Blick auf **Kotlin** oder **Scala** werfen.

---

## Weiterführende Themen

- [Stream Collectors im Detail](collectors)
- [CompletableFuture & asynchrone Programmierung](completable-future)
- [Vavr — funktionale Library für Java](https://vavr.io)

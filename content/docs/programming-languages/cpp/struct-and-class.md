---
weight: 999
title: "Struct and class"
description: ""
icon: "article"
date: "2024-09-24T16:43:44+02:00"
lastmod: "2024-09-24T16:43:44+02:00"
draft: false
toc: true
---

## Struct Beispiel

**Point.h**

```cpp
#pragma once // Preprocessor Anweisung: Sorgt dafuer, dass diese Header Datei nur einmal in die Kompilationseinheit inkludiert wird
#include <cmath>
#include <iostream>
#include <ostream>

struct Point { // struct = class public:
    int m_x = 0, m_y = 0; // x und y sind public; Styleguide: Jede Member Variable beginnt mit m_...

    Point(int x = 0, int y = 0)
        : m_x(x),
          m_y(y) { // constructor
        std::cout << "# Point ctor: " << *this << std::endl; //*this: this-pointer resp. "Dereferenzierungs-Operator", ansonsten wuerde die virtuelle Addresse des Point-Objektes zurueckgegeben werden.
    }

    ~Point() { // destructor
        std::cout << "# Point dtor: " << *this << std::endl;
    }

    // Ausgabeoperator (operator overloading)
    /*
     * friend: Bedeutet, dass dieser Operator keine Instanz Methode ist
     * Instanz Methoden haben ein versteckes Argument (*this) was dazu fuehren wuerde,
     * dass diesem Binaeren-Operator faktisch drei Argumente uebergeben werden was nicht erlaubt ist.
     * Mit 'friend' markierte Funktionen sind "befreundet" mit der Klasse und duerfen auf die Member Variablen der Klasse zugreifen.
     *
     * ostream&: der ostream wird als Referenz wieder zurueckgegeben
     * operator<<: Binaerer Operator mit zwei Argumenten. Das erste Argument steht links und das zweite Argument rechts vom Operator.
     *
     *
     * Sprich: (os << p1) gibt wieder ein os zurueck
    */
    friend std::ostream& operator<<(std::ostream& os, const Point& p) {
        return os << '(' << p.m_x << ',' << p.m_y << ')';

        // Folgendes wuerde auch gehen:
        // os << '(' << p.m_x << ',' << p.m_y << ')';
        // return os;
    }

    /*
     * const am Schluss bedeutet, dass das this-Objekt nicht veraendert wird oder werden kann.
     * i.e. Die Funktion hat somit nur Lesezugriff auf das this-Objekt.
     *
     * Wenn steht 'const Point p', wird per "by value" uebergeben. Das hat zur Folge, dass am Schluss dieser Funktion der Destruktor des uebergebenen Objektes aufgerufen wird.
     * Durch 'const Point& p' wird eine readonly Referenz auf das Point Objekt uebergeben
     *
     * Mit [[nodiscard]] markiert man die Funktion, dass der Rueckgabewert nicht ignoriert werden soll. Es wuerde aber nur Warnung ausgegeben werden. 
    */
    double dist(const Point& p) const {
        // Wenn steht 'const Point p', wird per "by value" uebergeben. Das hat zur Folge, dass am Schluss dieser Funktion der Destruktor des uebergebenen Objektes aufgerufen wird.
        // Durch 'const Point& p' wird eine readonly Referenz auf das Point Objekt uebergeben

        const int dx = p.m_x - m_x;
        const int dy = p.m_y - m_y;
        return hypot(dx, dy); // Pythagoras
    }

}; // Am Schluss wird immer ein abschliessender Strichpunkt erwartet
```

**main.cpp**

```cpp
#include <iostream>
#include "Point.h"

int main() {
    std::cout << "Classes Example" << std::endl;
    // Point p1, p2; // Geht, falls die Member Variablen initialisiert sind und ein Standardkonstruktor oder Konstruktor mit Default-Werten vorhanden ist. Sonst kommt ein Error oder irgend ein Wert.
    // Point p1{}, p2{}; // So werden die Attribute von Point mit 0 initialisiert. (Standardkonstruktor oder Default-Werte)
    Point p1{2, 3}, p2{7, 9}; // Explizites Initialisieren der beiden Attribute mit 0.
    // Point p1{2}, p2{9}; // Fehlende Attribute werden bei einem Standardkonstruktor mit 0 initialisiert.
    // Point p1(0, 0), p2(0, 0); // Ab c++20: Explizites Initialisieren der beiden Attribute mit 0.

    // p1.m_x = 4;
    // p1.m_y = 6;
    // p2.m_x = 14;
    // p2.m_y = 18;

    std::cout << "p1 = " << p1 << " p2 = " << p2 << std::endl;
    std::cout << "Distanz von p1 zu p2 ist: " << p1.dist(p2) << std::endl;

    std::cout << "Point size = " << sizeof(Point) << std::endl; // 8 (2*4 Bytes)

    // Die Aufrufe von Destruktoren ist in umgekehrter Reihenfolge zu den Konstruktor-Aufrufen.
    return 0;
}
```

## Klassen Beispiel

**Person.h**

```cpp
#pragma once
#include <iostream>
#include <string>

class Person {
    std::string m_name;
    int m_age;

public:
    /*
     * Parameter:
     * - Alle Objekte: by reference (string& name)
     * - Primitive Variablen: by value (int age)
    */
    Person(const std::string& name, int age)
        : m_name(name)
        , m_age(age)
    {}

    int getAge() const;
    void setName(const std::string& name);

    // Variante A
    friend std::ostream& operator<<(std::ostream& os, const Person& p);

    // Variante B: Funktion in der Header-Datei definieren
    // friend std::ostream& operator<<(std::ostream& os, const Person& p) {
    //     return os << '(' << p.m_name << ',' << p.m_age << ')';
    // }

};
```

**Person.cpp**

```cpp
#include "Person.h"
// In Person.h wird "string" bereits inkludiert und muss hier nicht nochmal inkludiert werden.

int Person::getAge() const {
    return m_age;
}

// Der Parameter 'name' wird wieder als Referenz uebergeben damit dieser nicht zweimal kopiert wird.
// Zweimal waere: 1. bei der Uebergabe in die Funktion und 2. beim Zuweisen des Parameters zur Member Variable.
void Person::setName(const std::string& name) {
    m_name = name;
    // = ist ein Assignment-Operator und kopiert den Inhalt des Parameters in die Member Variable.
    // Somit ist die Member Variable wieder "eigenstaendig".
}

// Variante A: Direkt in der cpp-Datei definieren
std::ostream& operator<<(std::ostream& os, const Person& p) {
    return os << '(' << p.m_name << ',' << p.m_age << ')';
}

```

**main.cpp**

```cpp
#include <iostream>
#include "Person.h"

int main() {
    std::cout << "Classes Example" << std::endl;
    Person sepp{"Sepp", 33};
    Person susi{"Susi", 44};
    std::cout << "sepp = " << sepp << std::endl; // (Sepp,33)
    std::cout << "susi = " << susi << std::endl; // (Susi,44)

    std::cout << "sepp.getAge() = " << sepp.getAge() << std::endl; // 33
    std::cout << "susi.getAge() = " << susi.getAge() << std::endl; // 44

    susi.setName("Vreni");
    std::cout << "susi = " << susi << std::endl; // (Vreni,44)

    std::cout << "int size = " << sizeof(int) << std::endl; // 4 Bytes
    std::cout << "std::string size = " << sizeof(std::string) << std::endl; // 40 Bytes
    std::cout << "Person size = " << sizeof(Person) << std::endl; // 48 (4 + 40 + 4->(damit es insgesamt eine Vielfaches von 8 wird) Bytes

    Person& refPers = sepp; // Referenz muss immer initialisiert werden
    std::cout << "refPers = " << refPers << std::endl; // (Sepp,33)
    refPers = susi; // Wichtig: So werden alle Attribut-Werte auf 'sepp' kopiert
    std::cout << "refPers = " << refPers << std::endl; // (Vreni,44)
    std::cout << "sepp = " << sepp << std::endl; // (Vreni,44)

    return 0;
}
```

## Parameterübergabe

```cpp
// By Value
void foo1(int x) // by value: Daten (auch Zeiger) werden kopiert

//By Reference
void foo3(const Person& p) // in: referenzierte Person wird nicht kopiert
void foo4(Person& p) // in-out: referenzierte Person wird nicht kopiert
// kann aber in foo4 verändert werden

// By Pointer
void foo5(Point* p) // good-practice: nur für out-Parameter verwenden, da beim Aufruf der out-Parameter 
// gut über den Adressoperator erkennbar ist
```

> Datentypen mit weniger oder gleichviel Speicher wie zwei Zeiger werden üblicherweise "by value" übergeben

## Rückgabewerte

**By Value**

Die Daten werden in Form eines temporären Objekts zurückkopiert. 
Bei grossen Objekten sollte man effizientere in-out oder out Parameterübergabe nutzen.

```cpp
double sqrt(double x)
Point move(const Point& p, int dx) // Ansatz: Point is immutable
```

**By Reference**

Darf nur verwendet werden, wenn die Referenz auf das zurückgegebene Objekt 
eine längere Lebensdauer als die Ausführung der Funktion hat.

```cpp
Point& Point::move(int dx, int dy) { 
    … return *this; 
} // Point is mutable

// falsche Verwendung (verwendet impliziten Zeiger auf zerstörtes Objekt)
Point& createPoint(int x, int y) { 
    Point p(x, y); 
    return p; 
}
```

## Initialisierungslisten

**Beispiel**

```cpp
#include <initializer_list> 

struct Tuple {
    int value[];
    Tuple(const initializer_list<int>& v); // ctor #1 
    Tuple(int a, int b, int c); // ctor #2
    Tuple(const initializer_list<int>& v, size_t cap); // ctor #3
};

Tuple t1(4, 5, 6); // () ctor #2 wird verwendet
Tuple t2{1, 2, 3}; // {} ctor #1 wird verwendet
Tuple t3{2, 4, 6, 8}; // {} ctor #1 wird verwendet 
Tuple t4{{2, 4, 6}, 3}; // {{},} ctor #3 wird verwendet
```

**Andere Beispiele:** 

```cpp
void print(const initializer_list<int>& ls) {
    for (auto i: ls) cout << i << ' '; 
    cout << endl;
}

for (auto i :{ 2, 4, 6, 8 }) cout << i << ',';
```

## Strukturiertes Binden von Werten

**Array**

```cpp
int arr[3] = { 2, 3, 4 };
auto [a, b, c] = arr; // Variablen a, b und c erhalten; Kopien der drei Arraywerte
```

**Pair**

```cpp
pair<int, double> p = { 5, 3.14 };
auto [i, d] = p; // Variable i ist vom Typ int, d vom Typ double

map<string, int> m;
for(const auto& [key, value] : m) {
    cout << key << ',' << value << endl;
}
```

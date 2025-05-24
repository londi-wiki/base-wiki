---
weight: 999
title: "Operator Overloading"
description: ""
icon: "article"
date: "2024-10-22T14:39:03+02:00"
lastmod: "2024-10-22T14:39:03+02:00"
draft: false
toc: true
---

# Allgemein

Signatur einer Methode besteht aus:
- Namensraum
- Klasse
- Name + Namespace
- Parameterliste
  - Anzahl
  - Typen
  - Reihenfolge
  - Parameterbezeichner sind irrelevant
  - Wertekategorie
- Rückgabetyp gehört **nicht** dazu

Alle Methoden müssen eine eindeutige Signatur haben.

Beispiel:

```cpp
class Point {
    double m_x, m_y, m_z;
public:
    Point& move(double x, double y = 0, double z = 0);
    Point& move(double delta[3]); 
    Point& move(const Point& p);
};
```

# Operatoren

## Output Operator

```cpp
friend std::ostream& operator<<(std::ostream& os, const Point& p) {
    return os << '(' << p.m_x << ',' << p.m_y << ')';
}
```

## Vergleichsoperatoren

```cpp
// bool operator==(const Point& p) const {
//     return m_x == p.m_x && m_y == p.m_y;
// }

friend bool operator==(const Point& lhs, const Point& rhs) {
    return lhs.m_x == rhs.m_x && lhs.m_y == rhs.m_y;
}

// bool operator<(const Point& p) const {
//     // lexikografische Ordnung
//     return m_x < p.m_x || m_x == p.m_x && m_y < p.m_y;
// }

// lhs = left hand side
friend bool operator<(const Point& lhs, const Point& rhs) {
    // lexikografische Ordnung
    return lhs.m_x < rhs.m_x || lhs.m_x == rhs.m_x && lhs.m_y < rhs.m_y;
}
```

```cpp
using namespace std;

// Generischer Operator
// template<typename T>
// bool operator<=(const T& lhs, const T& rhs) {
//     return lhs == rhs || lhs < rhs;
// }

int main() {
    Point p1, p2;

    // boolalpha macht aus 1/0 => true/false
    cout << "(p1 == p2): " << boolalpha << (p1 == p2) << endl; // true
    cout << "(p1 < p2): " << boolalpha << (p1 < p2) << endl; // false

    // Der Punkt kann auch mit Zahlen verglichen werden, falls beim Konstruktor nicht 'explicit' definiert ist
    cout << "(p1 == 0): " << boolalpha << (p1 == 0) << endl; // true
    cout << "(p1 < 1): " << boolalpha << (p1 < 1) << endl; // true
    // geht auch, aber nur wenn es nicht mit 'friend' deklariert ist (instanz methode)
    // cout << "(p1 < 1): " << boolalpha << (p1.operator<(1)) << endl;

    // Funktioniert, weil es kommutativ ist
    cout << "(0 == p2): " << boolalpha << (0 == p2) << endl; // true

    // Funktioniert erst dann, wenn der Vergleichsoperator mit 'friend' deklariert ist
    cout << "(1 < p2): " << boolalpha << (1 < p2) << endl; // false

    // Funktioniert erst dann, wenn der die '<='-Operation oder der spaceship-operator deklariert wird
    cout << "(p1 <= p2): " << boolalpha << (p1 <= p2) << endl;

    auto x = operator<=>(p1, p2);
    cout << "type of x: " << typeid(x).name() << endl; // struct std::strong_ordering

    return 0;
}
```

## Spaceship Operator <=>

Der spaceship Operator wird auch "three-way comparison operator" genannt und ist vergleichbar mit dem compareTo von Java.

Der Spaceship-Operator wurde in C++20 eingeführt und bietet eine elegante Möglichkeit, alle Vergleichsoperationen mit einer einzigen Implementierung zu definieren. Hier sind die wichtigsten Punkte:

Der Operator gibt einen von drei möglichen Werten zurück:
- Negativ (strong_ordering::less): wenn links < rechts
- Null (strong_ordering::equal): wenn links == rechts
- Positiv (strong_ordering::greater): wenn links > rechts

```cpp
// lexikografische Ordnung
friend auto operator<=>(const Point& lhs, const Point& rhs) noexcept = default;

// -----------
// falls selber implementiert, muss der '=='-Operator ebenfalls implementiert werden
friend std::weak_ordering operator<=>(const Point& lhs, const Point& rhs) {
    return std::weak_ordering::less;
};
// eq mit spaceship-operator
bool operator==(const Point& p) const {
    return std::is_eq(*this <=> p);
}
// -----------
```

Weitere Beispiele:

```cpp
#include <iostream>
#include <compare>

class Point {
    int x, y;
public:
    Point(int x, int y) : x(x), y(y) {}
    
    // Spaceship Operator definieren
    auto operator<=>(const Point& other) const {
        // Erst x vergleichen
        if (auto cmp = x <=> other.x; cmp != 0)
            return cmp;
        // Wenn x gleich ist, y vergleichen
        return y <=> other.y;
    }
    
    // Optional: == Operator für einfachere Gleichheitsprüfung
    bool operator==(const Point& other) const = default;
};

int main() {
    // Beispiel 1: Einfache Zahlenvergleiche
    int a = 10;
    int b = 20;
    auto result1 = a <=> b;
    
    if (result1 < 0)
        std::cout << "a ist kleiner als b\n";
    else if (result1 > 0)
        std::cout << "a ist grösser als b\n";
    else
        std::cout << "a ist gleich b\n";
    
    // Beispiel 2: Benutzerdefinierte Klasse
    Point p1(1, 2);
    Point p2(1, 3);
    
    auto result2 = p1 <=> p2;
    
    if (result2 < 0)
        std::cout << "p1 ist kleiner als p2\n";
    else if (result2 > 0)
        std::cout << "p1 ist grösser als p2\n";
    else
        std::cout << "p1 ist gleich p2\n";
    
    // Beispiel 3: Automatisch generierte Vergleichsoperatoren
    if (p1 < p2)
        std::cout << "p1 ist kleiner als p2\n";
    
    if (p1 == p2)
        std::cout << "p1 ist gleich p2\n";
    
    return 0;
}
```

## Cast Operator

```cpp
// Explicit setzt voraus, dass beim casten, explizit den cast mit zum Beispiel '(int)' durchgeführt werden muss.
explicit operator int() const  { return m_x + m_y; }
```

## Index Operator

```cpp
class PointVector {
    size_t m_capacity; // die Grösse des Arrays auf dem Heap
    size_t m_size; // Anzahl Objekte im Array: m_size <= m_capacity
    std::unique_ptr<Point[]> m_data; // Zeiger auf den Heap

public:
    PointVector()
        : m_capacity(0)
          , m_size(0)
          , m_data(nullptr) {
        std::cout << "std-ctor" << std::endl;
    }
    
    ...
    
    // index-operator (read)
    const Point& operator[](const size_t idx) const {
        // return *(m_data.get() + idx);
        return m_data[idx];
    }

    // index-operator (write)
    Point& operator[](const size_t idx) {
        return m_data[idx];
    }    
```

## Literal Operator

Bekannte Zahlen-Suffixe für Literale:
- 1.0 => double
- 1.0f => float
- 1 => int
- 1U => unsigned int
- 1L => long
- 1UL => unsigned long
- 1ULL => unsigned long long
- 1LL => long long

Hinweise:
- eigenes Suffix _suffix definieren, um Literale eines speziellen Typs zu markieren (vom Standard definierte Suffixe beginnen ohne _)
- globale Operatoren
- Ganzzahl 
  - type operator"" _suffix(unsgined long long)
- Fliesskommazahl
  - type operator"" _suffix(long double)
- Zeichen
   - type operator"" _suffix(char)
- Zeichenketten
   - type operator"" _suffix(const char*)

**Beispiel:**

```cpp
std::complex c = 5i; // c ist die komplexe Zahl (0,5) 
constexpr auto duration = 10s; // duration ist 10 Sekunden

constexpr long double operator"" _km(long double d) { return d*1000; }
constexpr long double operator"" _deg(long double d) { return d*pi/180; }

Complex operator"" _i(long double d) { return Complex(0,d); }
Complex operator"" _i(unsigned long long n) { return Complex(0,n); }

std::complex c = 5i; // c ist die komplexe Zahl (0,5)
Complex c = 4_i; // eigene Klasse für komplexe Zahlen 
auto dist = 10.0_km; // Distanz in Kilometer, dist in Meter
auto angle = 30_deg; // Winkel in Grad, angle in Radiant
```

## cast operator

### c-style-cast vs. static_cast

Ein `static_cast` ist in C++ sicherer und klarer als ein C-Style-Cast. Hier sind einige Vorteile:

1. **Typensicherheit**: `static_cast` führt zur Kompilierzeit eine Typprüfung durch, was bedeutet, dass viele Fehler frühzeitig erkannt werden können.
2. **Lesbarkeit**: `static_cast` macht den Cast-Typ explizit, was den Code lesbarer und verständlicher macht.
3. **Einschränkungen**: `static_cast` erlaubt nur bestimmte Arten von Casts, was das Risiko von unsicheren oder fehlerhaften Casts reduziert.

Ein Beispiel:
```cpp
int i = static_cast<int>(p1);
```

ist sicherer und klarer als:
```cpp
int i = (int)p1;
```

Es gibt noch folgende:
- dynamic_cast: Bei Vererbung üblich
- const_cast: const "weg" oder "hinzu" casten
- reinterpret_cast: Bei Rohpointer die nicht den "richtigen" Typ haben üblich

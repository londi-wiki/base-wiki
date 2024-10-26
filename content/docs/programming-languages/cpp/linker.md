---
weight: 999
title: "Linker"
description: ""
icon: "article"
date: "2024-10-26T13:49:58+02:00"
lastmod: "2024-10-26T13:49:58+02:00"
draft: false
toc: true
---

# Allgemein

TODO

# One definition rule

Das Deklarieren einer Friend-Funktion in mehreren Kompilationseinheiten sollte grundsätzlich vermieden werden und führt meist zur Verletzung der "ODR - One defintion rule".

Beispiel - Linker-Fehler (häufigster Fall):

```cpp
// point.h
class Point {
    int m_x, m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y) {}
    
    // Diese Definition im Header führt zu multiplen Definitionen
    friend bool operator==(const Point& lhs, const Point& rhs) {
        return lhs.m_x == rhs.m_x && lhs.m_y == rhs.m_y;
    }
};
```
Oder allgemein: Undefined Behavior (wenn die Definitionen nicht exakt identisch sind oder der Linker die mehrfache Definition nicht erkennt)

## Lösungsansätze

1. Inline-Definition (modern, bevorzugt):

```cpp
class Point {
    int m_x, m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y) {}
    
    // inline verhindert ODR-Verletzung
    friend inline bool operator==(const Point& lhs, const Point& rhs) {
        return lhs.m_x == rhs.m_x && lhs.m_y == rhs.m_y;
    }
};
```

2. Deklaration im Header, Definition in einer CPP-Datei:

```cpp
// point.h
class Point {
    int m_x, m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y) {}
    
    // Nur Deklaration
    friend bool operator==(const Point& lhs, const Point& rhs);
};

// point.cpp
bool operator==(const Point& lhs, const Point& rhs) {
    return lhs.m_x == rhs.m_x && lhs.m_y == rhs.m_y;
}
```

3. Moderne C++-Lösung mit defaulted Operator (wenn möglich):

```cpp
class Point {
    int m_x, m_y;
public:
    Point(int x, int y) : m_x(x), m_y(y) {}
    
    // Lässt den Compiler die Implementierung generieren
    bool operator==(const Point&) const = default;
};
```

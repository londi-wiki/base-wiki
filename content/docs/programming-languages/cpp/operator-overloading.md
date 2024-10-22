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
- Name
- Parameterliste
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
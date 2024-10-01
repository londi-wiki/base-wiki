---
weight: 999
title: "Const_constexpr"
description: ""
icon: "article"
date: "2024-10-01T18:31:41+02:00"
lastmod: "2024-10-01T18:31:41+02:00"
draft: false
toc: true
---

# Const

Mit `const` kann der Wert einer Variable nach dem Setzen nicht mehr geändert werden. `const` kann nur auf Variablen gesetzt werden.

Stichwort: Unveränderlich

```cpp
const int a = 1;
int const b = 1;
```

# Constexpr

Das Schlüsselwort `constexpr` setzt voraus, dass ein Wert zur Kompilationszeit zur Verfügung steht.
`constexpr` kann sowohl auf Variablen als auch auf Methoden gesetzt werden.

```cpp
constexpr int a = 3;

constexpr int foo() {
  return 7;
}

constexpr int b = foo(); // OK, weil foo() auch mit constexpr markiert ist.
```

Achtung! Der Compiler hat eine Sicherheit inform einer "Limitte" definiert, 
welche auf eine maximalen Anzahl an Operationen prüft.

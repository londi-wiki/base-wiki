---
weight: 999
title: "Type_conversion"
description: ""
icon: "article"
date: "2024-10-01T19:25:23+02:00"
lastmod: "2024-10-01T19:25:23+02:00"
draft: false
toc: true
---

## Typkonvertierung

```cpp
// static_cast: normale Typkonvertierung
int x = static_cast<int>(2.0);

// dynamic_cast: down-cast in Klassenhierarchie
Base *b = new Derived(21);
Derived *d = dynamic_cast<Derived*>(b);

// const_cast: const hinzufügen oder entfernen 
const Point p; 
const_cast<Point&>(p).setX(4);

// reinterpret_cast: keine Compiler-Checks
float f = 3.14f;
int bitRepresentation = *reinterpret_cast<int*>(&f);
```

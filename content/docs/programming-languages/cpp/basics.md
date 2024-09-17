---
weight: 999
title: "Basics"
description: ""
icon: "article"
date: "2024-09-17T19:00:04+02:00"
lastmod: "2024-09-17T19:00:04+02:00"
draft: false
toc: true
---

# Basics

## Memory Mapping

- Stack: lokale Variablen, Parameter
- Heap: mit new alloziert
- Data: statische Daten, fixe Zeichenketten

Das System sorgt dafür, dass ein Prozess nur auf die eigenen Daten im Speicher zugreifen kann.

## Dateien

- *.c: C-Quellcode
- *.cpp: C++-Quellcode
- *.h: C/C++ Header Dateien
- *.hpp: wird hauptsächlich für header-only-Implementierungen verwendet

## Programmerzeugung

### Präprozessor

- Programmcode darf Makros enthalten
- Makros werden unmittelbar vor der Kompilation evaluiert
- Bedingte Kompilation

Verwendung:
- #define XYZ, #define MyMacro(arg1, arg2)
  - definiert ein Symbol/Makro XYZ mit oder ohne Parameter
  - Präprozessor löst Symbol auf, d.h. ersetzt es durch Ersetzungstext
- #undex
  - löscht die Definitino eines Symbols, d.h. das Symbol ist danach nicht mehr definiert
- #ifdef XYZ, #else, und #endif
- #if defined(XYZ) && defined(QR) || defined(UV)
  - bedingte Kompilation: die Kompilation eines Quellcode-Blocks ist abhängig von der Definition eines oder mehrerer logisch verknüpfter Symbole
- Stringizer
  - #define MyMacro(arg) cout << #arg << end

Beispiel:

```cpp
#include <iostream> 
using namespace std;

inline int sqr(int x) { 
    return x*x;
}

int main() {
    int k = 0, sum = 0;
    for (int i=1; i<=10; i++) { 
    #ifdef _DEBUG
        const int t = sqr(k++); 
        clog << t << endl;
        sum += t;
    #else
        sum += sqr(k++); 
        #endif
    }
    cout << sum << endl;
}
```

> Das Schlüsselwort inline in C++ gibt dem Compiler einen Hinweis, 
> dass die Funktion "inline" eingebunden werden soll. 
> Das bedeutet, dass der Compiler versucht, die Funktion an den Aufrufstellen direkt in den Code 
> zu "kopieren" (anstatt einen normalen Funktionsaufruf mit Sprung und Rückkehr zu machen). 
> Dies kann die Ausführung beschleunigen

### Compiler (VC++ CL, GCC, clang, intel C++, ...)

- Syntaxüberprüfung des Quellcodes
- Erzeugung von Objektdateien (Maschinencode mit *nicht* aufgelösten Verknüpfungen zu anderen Objektdateien, Endung *.obj)

### Linker (Binder)

- Erzeugung von Bibliotheken oder ausführbaren Programmen aus einzelnen Objektdateien
  - statische Bibliotheken werden zur Kompilationszeit eingebunden (*.lib, lib*.a)
  - dynamische Bibliotheken werden zur Laufzeit geladen (*.dll, lib*.so)
  - ausführbare Programme (*.exe, in Linux keine spezielle Endung)
- Verknüfung zwischen Objektdateien werden aufgelöst
- Optimierungen (z.B. Entfernung nicht verwendeter Prozeduren/Funktionen sind möglich)

> Dynamische Bibliotheken können auch von anderen Programmen (gleichzeitig) verwendet werden. Programme sind meist auch kleiner, da die Bibliotheken nicht statischen eingebunden sind.

### Allgemein

- Alle cpp-Dateien können unabhängig und somit parallel kompiliert werden. Erst durch den "Linker" wird eine Abhängigkeit (falls vorhanden) zueinander geschaffen.
- Die Kompilation geschieht in einem einzigen Ablauf, von oben nach unten.
- Inkludierte Dateien werden an der Stelle von `#include` in den Text eingefügt.
- zyklische Abhängigkeiten müssen durch Vordeklarationen aufgebrochen werden, Stichwort: Klassen- und Funktionsprototypen.

## Einfache Datentypen

Grundsatz:
- Speicherbedarf der einfachen Datentypen ist Compiler spezifisch
- alle ganzzahligen Datentypen (inkl. char) gibt es 
  - vorzeichenlos (unsigned) und 
  - vorzeichenbehaftet (signed) in der Zweierkomplementdarstellung

Integer mit definiertem Speicherbedarf: `#include <cstdint>`
- uint8_t
- int8_t
- ...

## Speicherklassen

- Statischer Speicher
  - globale Variablen, Variablen in einem Namensraum, Modulvariablen und Klassenvariablen
  - Variablen werden automatisch mit 0 initialisiert, falls nicht anderweitig definiert
  - Variablen bleiben während der ganzen Laufzeit des Programms im Speicher
- Automatischer Speicher (Stack)
  - Funktionsparameter, lokale Variablen
  - wird zur Laufzeit auf dem Stack angelegt und beim Verlassen des Blocks automatisch vom Stack entfernt
- Dynamischer Speicher (Heap)
  - Objekte werden zur Laufzeit mit new (C++) oder malloc (C) auf dem Heap alloziert
  - nicht mehr benötigte Objekte müssen mit delete (C++) oder free (C) freigegeben werden

## Beispiele

### Scope

```cpp
int main() {
    int x = 5;
    {
        int x = 3;
        std::cout << x << std::endl; // 3
    }
    std::cout << x << std::endl; // 5
}
```

### DEBUG

Code nur im DEBUG Modus ausführen:

```cpp
#ifdef _DEBUG
std::cout << "DEBUG" << std::endl;
#endif
```

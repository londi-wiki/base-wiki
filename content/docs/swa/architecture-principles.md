---
weight: 999
title: "Architecture Principles"
description: ""
icon: "article"
date: "2024-10-29T10:18:03+01:00"
lastmod: "2024-10-29T10:18:03+01:00"
draft: false
toc: true
---

# Architektur Prinzipien

## SOLID

1. Single Responsibility
2. Open/Closed
3. Liskov Substitution
4. Interface Segregation
5. Dependency Inversion


### Single Responsibility 

Siehe [Single Responsibility](https://wiki.strubli.com/docs/swa/architecture-patterns/#single-responsibility-prinzip-srp)

### Open/Closed

> "Classes should be open for extension but closed for modification."

### Liskov Substitution

> "Objekte einer Superklasse sollen durch Objekte ihrer Subklassen ersetzt werden können, ohne dass die korrekte Funktionsweise des Programms beeinträchtigt wird."

**Hauptaspekte des LSP:**

- Verhaltenskompatibilität
  - Subklassen müssen alle Verträge (Contracts) der Basisklasse erfüllen
  - Keine Abschwächung der Vorbedingungen
  - Keine Verstärkung der Nachbedingungen
  - Invarianten müssen erhalten bleiben
- Signaturkompatibilität
  - Parameter-Typen dürfen in Subklassen nur weiter werden
  - Rückgabe-Typen dürfen in Subklassen nur enger werden
  - Exceptions dürfen nur weniger oder spezieller werden

```mermaid
classDiagram
    %% Gute Implementierung
    class Shape {
        <<abstract>>
        #width: double
        #height: double
        +Shape(width: double, height: double)
        +calculateArea(): double*
    }
    
    class Rectangle {
        +Rectangle(width: double, height: double)
        +setWidth(width: double)
        +setHeight(height: double)
        +calculateArea(): double
    }
    
    class Square {
        +Square(side: double)
        +setSide(side: double)
        +calculateArea(): double
    }
    
    %% Schlechte Implementierung
    class Rectangle2 {
        #width: double
        #height: double
        +Rectangle2(width: double, height: double)
        +setWidth(width: double)
        +setHeight(height: double)
        +getArea(): double
    }
    
    class Square2 {
        +Square2(side: double)
        +setWidth(width: double)
        +setHeight(height: double)
        +getArea(): double
        note: "LSP Verletzung: setWidth/Height ändern beide Dimensionen"
    }
    
    %% Beziehungen
    Shape <|-- Rectangle : ✓ LSP konform
    Shape <|-- Square : ✓ LSP konform
    Rectangle2 <|-- Square2 : ✗ LSP verletzt
    
    note for Shape "Gute Implementierung:\n- Klare Abstraktion\n- Jede Unterklasse behält eigene Invarianten"
    note for Rectangle2 "Schlechte Implementierung:\n- Enge Kopplung\n- Überraschende Seiteneffekte"
```

**Gute Implementierung:**
- Shape als abstrakte Basisklasse
- Rectangle und Square als unabhängige Ableitungen
- Jede Klasse hat ihre eigenen, passenden Methoden
- LSP wird eingehalten, da jede Unterklasse die Basisklassen-Garantien erfüllt

**Schlechte Implementierung**
- Direkte Vererbung Rectangle2 -> Square2
- Square2 muss Methoden überschreiben, um Quadrat-Eigenschaften zu erzwingen
- LSP-Verletzung durch unerwartetes Verhalten der überschriebenen Methoden

**Best Practices**

1. Abstraktionen richtig verwenden
2. Ersetzbarkeit prüfen
3. Tell, Don't ask

### Interface Segregation

> "Clients sollten nicht gezwungen werden, von Interfaces abzuhängen, die sie nicht verwenden."

TODO...

### Dependency Inversion

TODO...

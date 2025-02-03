---
weight: 999
title: "Design Pattern Identification"
description: ""
icon: "article"
date: "2025-02-03T18:40:36+01:00"
lastmod: "2025-02-03T18:40:36+01:00"
draft: false
toc: true
---

# Allgemein

Jedes Design-Pattern hat ein wiederkehrendes Strukturelement. Bei Code Beispielen auf folgendes achten:

- Klassenbeziehungen (Erben, Interfaces, Komposition)
- Methoden-Signaturen (Factory-Methoden, Observer-Benachrichtigungen)
- Erstellungsmechanismen (Singleton-Instanzen, Factory-Methoden)
- Kommunikationswege (Events, Callbacks, Proxys)

# Schlüsselindikatoren

## Erzeugungsmuster (Creational Patterns)

| Pattern          | Merkmale im Code                                                                    | Hinweise                              |
|------------------|-------------------------------------------------------------------------------------|---------------------------------------|
| Singleton        | private static instance; private constructor; **getInstance() Methode**             | Nur eine Instanz erlaubt              |
| Factory Method   | abstract class mit create()-Methode; Subklassen überschreiben **create()**          | Flexible Objekt-Erzeugung             |
| Abstract Factory | Mehrere Factory-Klassen mit Methoden wie **createProductA()**, **createProductB()** | Erzeugung mehrerer verwandter Objekte |
| Builder          | Methoden wie **setPartA()**, **setPartB()** ; **build()-Methode** am Ende           | Schrittweise Objekterzeugung          |
| Prototype        | **clone()-Methode**, **implements Cloneable**                                       | Objekt-Kloning                        |

## Strukturmuster (Structural Patterns)

| Pattern   | Merkmale im Code                                                            | Hinweise                                        |
|-----------|-----------------------------------------------------------------------------|-------------------------------------------------|
| Adapter   | implements Zielinterface aber nutzt eine bestehende Klasse intern           | Schnittstelle anpassen                          |
| Decorator | wrap() oder setComponent() mit einer Referenz auf das gleiche Interface     | Dynamisches Verhalten hinzufügen                |
| Proxy     | Eine Klasse hat eine Referenz auf ein Objekt und kontrolliert Zugriff       | Zugriffsschutz, Lazy Loading                    |
| Composite | **List<Component> children** ; add() und remove() Methoden                  | Hierarchische Struktur (Baum)                   |
| Facade    | Eine Klasse, die mehrere andere Klassen kapselt und vereinfachte API bietet | Einfacher Zugriff auf ein komplexes System      |
| Bridge    | Abstraction hat eine Referenz auf Implementierung                           | Entkopplung von Abstraktion und Implementierung |

## Verhaltensmuster (Behavioral Patterns)

| Pattern                 | Merkmale im Code                                                                    | Hinweise                                         |
|-------------------------|-------------------------------------------------------------------------------------|--------------------------------------------------|
| Observer                | addObserver(), removeObserver(), notifyObservers()                                  | Event-Benachrichtigung                           |
| Strategy                | interface Strategy { execute(); } ; Klasse enthält **setStrategy()**                | Austauschbare Algorithmen                        |
| Command                 | interface Command { execute(); } ; Invoker speichert und führt commands aus         | Befehle kapseln und verzögert ausführen          |
| State                   | setState() Methode in Klasse ; Mehrere konkrete State-Klassen                       | Zustandswechsel durch Klassen-Instanzwechsel     |
| Template Method         | abstract class mit final Methode ; Bestimmte Schritte in Unterklassen überschrieben | Ablauf mit fixem Gerüst aber flexiblen Schritten |
| Chain of Responsibility | Handler next; handleRequest() ruft next.handleRequest() auf                         | Verarbeitungskette                               |
| Mediator                | Eine zentrale Klasse verwaltet Kommunikation zwischen Objekten                      | Vermeidung direkter Objektverknüpfung            |


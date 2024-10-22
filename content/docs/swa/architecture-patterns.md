---
weight: 999
title: "Architecture Patterns"
description: ""
icon: "article"
date: "2024-10-22T13:54:06+02:00"
lastmod: "2024-10-22T13:54:06+02:00"
draft: false
toc: true
---

# Entwurfsmuster

## Single Responsibility Prinzip (SRP)

Das Single Responsibility Principle (SRP), eines der fünf SOLID-Prinzipien,
ist ein fundamentales Konzept im objektorientierten Design. Es besagt,
dass eine Klasse oder ein Modul nur eine einzige Verantwortung haben sollte.
Das bedeutet, eine Klasse sollte nur für eine einzige Aufgabe oder Funktion
innerhalb eines Systems zuständig sein und nur einen Grund haben, sich zu ändern.

Die Idee hinter SRP ist, die **Kohäsion** innerhalb einer Klasse zu maximieren und
die **Abhängigkeiten zu minimieren**.

Wenn eine Klasse mehrere Verantwortlichkeiten hat, kann sich das negativ auf die Wartbarkeit,
Lesbarkeit und Flexibilität des Codes auswirken.

Anzeichen für Verletzungen des SRP:
- Zu viele Methoden oder Verantwortlichkeiten
- Methodennamen geben unterschiedliche Verantwortlichkeiten an
- Häufige Änderungen aufgrund unterschiedlicher Gründe
- Viele Abhängigkeiten

Massnahmen:
- Refaktorierung in kleinere, fokussierte Klassen
- Verwenden von Entwurfsmuster
- Prüfen auf Wiederverwendbarkeit
- Abhängigkeiten injizieren
- Unit Tests

## Prinzip der losen Kopplung

Lose Kopplung (Loose Coupling) ist ein Prinzip in der Softwareentwicklung,
das darauf abzielt, die Abhängigkeiten zwischen den Komponenten oder Modulen eines Systems
so gering wie möglich zu halten. Komponenten sollten so gestaltet sein,
dass sie unabhängig voneinander geändert oder verwendet werden können,
ohne dass andere Teile des Systems stark betroffen sind.

Anzeichen für starke Kopplung:
- Direkte Abhängigkeiten zwischen Modulen
- Viele Imports oder Abhängigkeiten
- Änderungen propagieren
- Zu viele Getter und Setter
- Zirkuläre Abhängigkeiten

Massnahmen:
- Verwende Schnittstellen und Abstraktionen
- Dependency Injection (DI)
- Beobachter- oder Ereignismuster
- Vermeide globale Zustände und Singleton-Muster
- Fassade- oder Adaptermuster
- Modularisierung
- Vermeide zirkuläre Abhängigkeiten

## Observer Pattern

Das Observer Pattern ist ein Verhaltensmuster, das verwendet wird, wenn ein Objekt (der Subject) mehrere andere Objekte (die Observers) über Änderungen informieren muss, ohne dass diese Objekte stark voneinander abhängen. Es wird oft in Situationen verwendet, in denen ein Ereignis mehrere Reaktionen auslösen soll.

Wann das Observer Pattern passend ist:
- Wenn sich der Zustand eines Objekts ändert und mehrere andere Objekte darüber benachrichtigt werden sollen.
- Wenn man eine lose Kopplung zwischen dem beobachteten Objekt und den abhängigen Objekten (Observers) erreichen möchte.

## Composite Pattern

Das Composite Pattern ist ein Strukturmuster, das verwendet wird,
um eine Baumstruktur von Objekten darzustellen, bei der Objekte und ihre Zusammenstellungen
gleich behandelt werden können. Das bedeutet, einzelne Objekte und Zusammensetzungen
von Objekten sollen auf die gleiche Weise genutzt werden können.

Wann das Composite Pattern passend ist:
- Wenn eine Baumstruktur von Objekten dargestellt werden soll, bei der einzelne Objekte und zusammengesetzte Objekte auf dieselbe Weise behandelt werden.
- Wenn eine rekursive Struktur erforderlich ist, bei der ein „Ganzes“ und „Teile“ gleichartig verarbeitet werden.
- Wenn Objekte (wie Verzeichnisse) andere Objekte (wie Dateien und Unterverzeichnisse) enthalten können, aber dennoch die gleiche Schnittstelle benötigen.

## Creational Patterns

- Singleton: Stellt sicher, dass eine Klasse nur eine einzige Instanz hat und bietet einen globalen Zugriffspunkt darauf.
- Factory Method: Definiert eine Schnittstelle zur Erstellung von Objekten, überlässt die Entscheidung über die Instanziierung aber den Unterklassen.
- Abstract Factory: Erzeugt eine Familie von verwandten oder abhängigen Objekten, ohne deren konkrete Klassen zu spezifizieren.
- Builder: Trennt die Konstruktion eines komplexen Objekts von seiner Repräsentation, sodass derselbe Konstruktionsprozess unterschiedliche Darstellungen erzeugen kann.
- Prototype: Erlaubt das Erstellen neuer Objekte durch das Kopieren eines Prototypen-Objekts.

## Structural Patterns

- Adapter: Konvertiert die Schnittstelle einer Klasse in eine andere Schnittstelle, die die Clients erwarten. Es ermöglicht das Zusammenarbeiten von Klassen, die sonst inkompatibel wären.
- Decorator: Fügt einem Objekt zur Laufzeit zusätzliche Funktionalitäten hinzu, ohne dessen Klasse zu ändern.
- Facade: Bietet eine vereinfachte Schnittstelle zu einem komplexen System von Klassen oder einer Bibliothek.
- Proxy: Bietet einen Stellvertreter oder Platzhalter für ein anderes Objekt, um zusätzliche Kontrolle (wie Zugriff oder Caching) hinzuzufügen.
- Bridge: Trennt eine Abstraktion von ihrer Implementierung, sodass beide unabhängig voneinander variieren können.

## Behavioral Patterns

- Strategy: Definiert eine Familie von Algorithmen, kapselt sie und macht sie austauschbar. Der Algorithmus kann zur Laufzeit geändert werden.
- Command: Kapselt eine Anforderung als ein Objekt, sodass Sie Anfragen als Objekte speichern, übergeben und bearbeiten können.
- Chain of Responsibility: Gibt eine Anforderung durch eine Kette von Handlern weiter, bis sie verarbeitet wird.
- Template Method: Definiert das Skelett eines Algorithmus in einer Methode, lässt jedoch Unterklassen einige Schritte des Algorithmus definieren.
- State: Ermöglicht es einem Objekt, sein Verhalten zu ändern, wenn sich sein interner Zustand ändert.
- Mediator: Definiert ein Objekt, das die Kommunikation zwischen verschiedenen Objekten vermittelt und entkoppelt.
- Visitor: Trennt einen Algorithmus von den Objekten, auf denen er arbeitet, sodass neue Operationen hinzugefügt werden können, ohne die Klassen zu ändern, auf die der Algorithmus angewendet wird.

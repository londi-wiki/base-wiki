---
weight: 999
title: "Loose Coupling"
description: ""
icon: "article"
date: "2025-02-05T19:38:25+01:00"
lastmod: "2025-02-05T19:38:25+01:00"
draft: false
toc: true
---

# Arten der Kopplung

## Datenkopplung (Data coupling)

**Beschreibung:** Zwei Klassen oder Methoden sind durch die Übergabe von Daten (Parameter, Objekte) verbunden. Dies ist die schwächste Form der Kopplung.

**Erkennung:** Eine Methode benötigt Parameter, um korrekt zu arbeiten. Z. B. die Methode dbAccessMethod(DatabaseConnection dbCon) im Code.

**Verbesserung:** Die Menge und Komplexität der übergebenen Daten reduzieren. Möglichst wenige Parameter verwenden oder Daten in einer Struktur encapsulieren.

## Steuerungskopplung (Control coupling)

**Beschreibung:** Eine Methode beeinflusst den Kontrollfluss einer anderen, indem sie Steuerungsparameter wie Flags übergibt.

**Erkennung:** Methoden enthalten Kontrollparameter (z. B. Boolean-Flags), die beeinflussen, welcher Code ausgeführt wird.

**Beispiel:** performTask(boolean isSpecialCase).

**Verbesserung:** Kontrollparameter vermeiden. Stattdessen separate Methoden oder Klassen für unterschiedliche Kontrolllogiken verwenden.


## Statische Kopplung (Static coupling)

**Beschreibung:** Eine Klasse ruft direkt eine statische Methode einer anderen Klasse auf. Dies führt zu einer starken Abhängigkeit von der spezifischen Implementierung.

**Erkennung:** Direkte Aufrufe wie Database.newConnection().

**Verbesserung:** Dependency Injection oder Factory-Methoden verwenden, um die Abhängigkeit zu abstrahieren.


## Schnittstellenkopplung (Interface coupling)

**Beschreibung:** Klassen sind über die Nutzung einer öffentlichen Schnittstelle (API) verbunden. Dies ist eine moderate Form der Kopplung, solange die Schnittstelle stabil ist.

**Erkennung:** Methodenaufrufe auf Objekte anderer Klassen, z. B. dbCon.createQuery().

**Verbesserung:** Gut definierte Schnittstellen oder abstrakte Klassen verwenden. Sicher stellen, dass Änderungen an einer Klasse keine Auswirkungen auf andere haben.


## Inhaltliche Kopplung (Content coupling)

**Beschreibung:** Eine Klasse greift direkt auf die internen Details (z. B. Felder oder Methoden) einer anderen Klasse zu.

**Erkennung:** Direkter Zugriff auf private oder geschützte Member einer anderen Klasse. Im gegebenen Code-Fragment tritt dies nicht auf.

**Verbesserung:** Die Implementierungsdetails durch den Einsatz von private und protected geschützt halten. Getter/Setter verwenden, um den Zugriff zu kontrollieren.

## Prozedurale Kopplung (Procedural coupling)

**Beschreibung:** Eine Methode erwartet, dass andere Methoden in einer bestimmten Reihenfolge aufgerufen werden, um korrekt zu funktionieren.

**Erkennung:** Methodenaufrufe, die eine strikte Sequenz benötigen, z. B. query.perform() muss nach query.createQuery() aufgerufen werden.

**Verbesserung:** Die korrekte Reihenfolge dokumentieren oder Design-Muster wie **Builder** oder **Templates** verwenden.

## Zeitliche Kopplung (Temporal coupling)

**Beschreibung:** Methoden hängen von einer bestimmten zeitlichen Reihenfolge ab, in der sie ausgeführt werden müssen.

**Erkennung:** Ein Objekt oder eine Methode funktioniert nur, wenn es in einem bestimmten Zustand ist, z. B. dbCon.open() vor dbCon.createQuery().

**Verbesserung:** Zustandsprüfungen oder Builder-Muster verwenden, um sicherzustellen, dass die Abfolge korrekt eingehalten wird.

## Externe Kopplung (External coupling)

**Beschreibung:** Abhängigkeit von externen Systemen wie Datenbanken, Netzwerken oder APIs.

**Erkennung:** Direkter Zugriff auf externe Ressourcen, z. B. Database.newConnection() verbindet sich mit einer Datenbank.

**Verbesserung:** Abstraktionen (Interfaces oder Adapter) verwenden, um die Abhängigkeit zu entkoppeln.

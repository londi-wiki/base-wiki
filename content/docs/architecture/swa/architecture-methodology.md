---
weight: 999
title: "Architecture Methodology"
description: ""
icon: "article"
date: "2024-10-22T13:55:35+02:00"
lastmod: "2024-10-22T13:55:35+02:00"
draft: false
toc: true
---

# Allgemein

## Definition Software-Architektur

Software-Architektur beschreibt die Struktur eines Systems, einschliesslich Komponenten, Beziehungen und Prinzipien. Sie ist wichtig für Skalierbarkeit, Wartbarkeit und Effizienz.

## Kernziele einer Architekturmethodik

Hauptziele sind Modularität, Wiederverwendbarkeit, Skalierbarkeit, Performance, Sicherheit und Wartbarkeit.

## Unterschied zwischen funktionalen und nicht-funktionalen Anforderungen

Funktionale Anforderungen beschreiben, was ein System tun soll (z. B. Login-Funktion), 
während nicht-funktionale Anforderungen beschreiben, wie es dies tun soll (z. B. Sicherheit, Performance).

# Begrifflichkeiten

## Architecture Condition

Die Architecture Condition bezieht sich auf die Rahmenbedingungen, 
unter denen eine Architektur entworfen wird. Dies umfasst Anforderungen, 
Einschränkungen und Annahmen, die eine entscheidende Rolle im Designprozess spielen. 
Diese Bedingungen beeinflussen die Gestaltung der Architektur und setzen Leitplanken für den Entwurf.

## Architecture Significance

Architecture Significance bezeichnet die Bedeutung einer architektonischen Entscheidung 
in Bezug auf die Auswirkungen, die sie auf das gesamte System hat. In der Regel bezieht 
sich dies auf Entscheidungen, die schwerwiegende Folgen haben oder teuer und aufwendig zu ändern sind. 
Nur signifikante (wichtige) Entscheidungen werden als „architektonisch“ betrachtet.

## Architecture Approach

Architecture Approach beschreibt die Vorgehensweise, die ein Architekt bei der Entwicklung der 
Architektur verfolgt. Dies umfasst Methoden, Techniken, und die allgemeine Strategie, 
um ein System zu entwerfen, zu implementieren und zu warten. Der Ansatz beeinflusst, 
wie die Architektur unter Berücksichtigung der Bedingungen und der signifikanten Entscheidungen 
umgesetzt wird.

# Unterschiede

**Condition** beschreibt die Rahmenbedingungen oder Einschränkungen, die eine Architekturentscheidung beeinflussen. 
Dies können technische, organisatorische oder externe Faktoren sein.

**Significance** beschreibt die Bedeutung und den Einfluss einer bestimmten Architekturentscheidung. 
Sie erklärt, warum eine Entscheidung wichtig ist und welche Auswirkungen sie hat.

**Approach** hingegen beschreibt den konkreten Lösungsweg oder die Strategie zur Umsetzung einer Architekturentscheidung.

**Beispiel:**

- Condition: Das Unternehmen betreibt bereits ein monolithisches System mit einer grossen Codebasis und muss eine schrittweise Migration ermöglichen. Ausserdem gibt es regulatorische Vorgaben zur Datenspeicherung in der EU.
- Significance: Die Entscheidung für eine Microservices-Architektur ist bedeutend, weil sie Skalierbarkeit und Flexibilität ermöglicht.
- Approach: Die Umsetzung erfolgt durch eine API-gesteuerte Kommunikation mit Docker und Kubernetes für die Container-Orchestrierung.


# Faktoren

Mehrere Faktoren bestimmen den Approach, darunter:

- Architecture Condition – Welche **Rahmenbedingungen** bestehen (z. B. bestehende Systeme, Budget, Compliance)?
- Significance – Welche **Auswirkungen** hat die Entscheidung (z. B. Performance, Wartbarkeit)?
- Technologische Möglichkeiten – Welche Technologien und Best Practices sind geeignet?
- Business-Anforderungen – Welche Geschäftsziele müssen unterstützt werden?

**Beispiel:**

Ein Unternehmen entscheidet sich für eine Event-driven Architecture, weil:

- Die Architektur **signifikant** für die Echtzeitverarbeitung von Daten ist.
- Die **Rahmenbedingungen** Kafka als Middleware vorgeben.
- Der **Approach** eine asynchrone Kommunikation mit Event Sourcing nutzt.



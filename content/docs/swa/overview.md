---
weight: 999
title: "Overview"
description: ""
icon: "article"
date: "2024-10-22T08:23:43+02:00"
lastmod: "2024-10-22T08:23:43+02:00"
draft: false
toc: true
---

# Classical Architecture

> Die klassische Architektur befasst sich mit der Ordnungsstruktur von Teilen eines
beabsichtigten Ganzen.
Dabei verfolgt die Architektur einen architektonischen Zweck, der darauf abzielt
Architekturbedingungen (z. B. der Wunsch nach funktionalem, bezahlbarem Wohnraum) mit
gegebener architektonischer Mittel (z. B. Baumaterialien, Werkzeuge, Techniken und Methoden).

Der klassische Begriff der Architektur umfasst sowohl den systematischen Prozess
der Planung, des Entwurfs und der Implementierung von Architektur als auch das Ergebnis dieses
Architekturprozesses.

Architektur = Architekturprozess + Ergebnis des Architekturprozesses

1. Aufnehmen 
2. Planen 
3. Analysieren 
4. Entwerfen 
5. Implementieren/Umsetzen 
6. Validieren

Architektur entwirft Systeme so, dass sie die gewünschten externen und internen
Fähigkeiten, Charakteristika oder Eigenschaften haben, sodass die Systeme ihren Zweck erfüllen können.

Externe Fähigkeiten <=> Interne Merkmale/Eigenschaften

Dieser allgemeine Ansatz für die Architektur eines Systems wird immer wieder fortgesetzt, 
bis das Ganze und seine Teile vollständig konstituiert sind.

**Beispiel:** [dokchess](https://www.dokchess.de/)

# Enterprise Operating Model

Hier ist die Übersetzung:

Architektur findet nicht auf einer grünen Wiese statt (d. h. ohne Kontext) und niemals ohne Grund. 

Zudem muss Architektur organisatorisch umgesetzt werden, wofür Architekturfunktionen verantwortlich sind.  
Eine Architekturfunktion etabliert Architekturfähigkeiten innerhalb der Organisation – 
es handelt sich um ein soziotechnisches System, das Architekturdiziplinen verwirklicht, 
indem es deren Beiträge in ein Betriebsmodell des Unternehmens integriert.  
Ein Betriebsmodell spezifiziert und erfasst, wie die internen Abläufe einer Organisation gestaltet sind, 
um den Kunden einen Mehrwert zu bieten. Es beschreibt, wie eine Organisation zusammenarbeitet – 
beschränkt sich jedoch auf die wesentlichen Aspekte der organisatorischen Zusammenarbeit.

**Stichwort:** Operating model cancas

[operatingmodelcanvas.com](https://operatingmodelcanvas.com/)

![operatingmodelcanvas](https://operatingmodelcanvas.com/wp-content/uploads/2017/02/slide11.jpg)

# Value delivery chain / Wertschöpfungskette

Eine Wertschöpfungskette betrachtet eine Organisation als eine Reihe von Prozessen auf verschiedenen Ebenen der Prozessaggregation. Darüber hinaus wird eine Organisation als ein System betrachtet, das in Subsysteme zerlegt ist, wobei jedes Subsystem seine Eingaben, Transformationsprozesse und Ausgaben hat.

Plan => Build => Run

# Architecture Disciplines

## Unternehmensarchitektur (Enterprise Architecture):
Diese Disziplin stellt sicher, dass die verschiedenen Architekturansätze eines Unternehmens aufeinander abgestimmt sind. 
Sie legt die übergreifenden Richtlinien, Methoden und Rahmenbedingungen fest, 
um eine kohärente Ausrichtung zwischen verschiedenen Geschäftsbereichen und technischen Lösungen 
zu gewährleisten.

## Domänenarchitektur (Domain Architecture):
Diese Disziplin fokussiert sich auf spezifische Geschäftsbereiche oder Domänen innerhalb eines Unternehmens. 
Sie bietet Transparenz und Orientierung bei der Entscheidung, 
welche Systeme innerhalb einer Domäne verbessert oder angepasst werden müssen. 
Domänenarchitektur befasst sich sowohl mit der aktuellen (Ist-Zustand) 
als auch der zukünftigen (Soll-Zustand) Architektur und erstellt Roadmaps und Standards für die Domäne.

## Softwarearchitektur (Software Architecture) / Lösungsarchitektur (Solution Architecture):
Die Softwarearchitektur konzentriert sich auf die technische Umsetzung und Verbesserung einzelner 
Softwaresysteme. Sie wird verwendet, um Probleme zu identifizieren und zu lösen, 
indem neue Systeme entwickelt oder bestehende Systeme modifiziert werden, um die Anforderungen zu erfüllen. 
Diese Disziplin stellt sicher, dass die Lösungen den funktionalen und nicht-funktionalen Anforderungen gerecht werden.

## Box-and-arrow Diagram

| **Aspekt**               | **Logical View**                          | **Development View**                                                                              |
|--------------------------|-------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Boxen darstellen**     | Objekte                                   | Module, Klassen, Pakete oder Komponenten                                                          |
| **Pfeile darstellen**    | Beziehungen/Interaktion zwischen Objekten | Abhängigkeiten oder Kommunikationspfade zwischen Modulen   (Vererbung, Assoziation, Abhängigkeit) |

# System architektur

Die teleologische und ontologische Systemperspektive unterscheiden sich in den Informationen, die sie über ein System vermitteln, sowie in den Zielgruppen, die sie ansprechen.

## Teleologische Perspektive

Diese Perspektive fokussiert sich auf den **Zweck** und die **Funktionalität** eines Systems, 
also das **"Was"** das System tut und warum es existiert.

Sie beschäftigt sich mit den extern sichtbaren Fähigkeiten eines Systems, 
den **Funktionen** und **Qualitäten**, die es erfüllen soll.

Typische Fragen in dieser Perspektive wären:
- Was soll das System leisten?
- Welche Funktionen müssen erfüllt werden, um den Systemzweck zu erreichen?
- Welche Qualitätseigenschaften (z.B. Leistung, Sicherheit, Zuverlässigkeit) sind wichtig?

Verantwortung: Business/Enterprise Architekten, Fachpersonen

## Ontologische Perspektive

Diese Perspektive betrachtet das **"Wie"**, also die **Struktur**, **Komponenten** und den **Aufbau** des Systems.

Es geht um die internen Details, wie das System aufgebaut ist, 
welche Subsysteme oder Komponenten es gibt und wie diese miteinander verbunden sind.

Typische Fragen in dieser Perspektive wären:
- Wie ist das System zusammengesetzt?
- Welche Bausteine (Komponenten) gibt es, und wie interagieren sie miteinander?
- Welche technischen Details sind relevant?

Verantwortung: Solution Architekt / Software Engineer

## Allgemeine Aussagen

- Durch Verbindungen (z.B. Funktionsaufrufen, Datenaustausch), die zwischen Systemen geschaffen werden, entstehen neue Systeme.
- Neben den Fähigkeiten, die ein System etabiliert und seinen Nutzen anbietet, evolviert auch die Architektur des Systems selbst über seine Lebensspanne hinweg.
- Ein Architektursichtenmodell beschreibt, welche Sichten auf ein System ein Softwarearchitekt zu welchem Zweck, entwickeln sollte, welche Modelltypen zur Modellierung einer Sicht sinnvoll sind und welche Sichten wie kombiniert werden sollten, um daraus ganzheitliche (i.e., holistische) Systemeinsichten abzuleiten.
- Alle Softwaresysteme adressieren sowohl fachliche als auch technische Belange. Denken Sie beim Begriff der fachlichen Belange an die fachlichen, bzw. funktionalen Fähigkeiten eines Softwaresystems, während Sie beim Begriff der technischen Belange an dessen nichtfunktionalen Fähigkeiten denken dürfen (z.B. Sicherheit, Verfügbarkeit, Performance).
- Jedes System hat eine Architektur - unabhangig davon, ob diese bewusst entwickelt oder beschrieben wurde.
- Ein view model ist eine Systematik bestehend aus viewpoints, types of models und Beziehungen zwischen diesen. 
- Architekturbeschreibung besteht weitgehend aus Modellen. Welche Modelle für welche Aspekte einer Architekturbeschreibung verwendet werden, wird von entsprechenden Sichtenmodellen beschrieben und empfohlen.
- Auf Lösungsarchitektur spezialisierte Sichtenmodelle konzentrieren sich auf folgende Komponententypen: funktionale Komponenten, informationelle Komponenten und betriebliche (i.e., operationale) Komponenten.

# System Evolution

![system-evolution](/images/system-evolution.png)

Quelle: Stephan Murer et al empirisch

Das Schaubild stellt die Beziehung zwischen Agilität (y-Achse) und Funktionalität (x-Achse) eines Systems dar.

**Agilität:** Die Fähigkeit des Systems, 
schnell und effizient auf Veränderungen zu reagieren. 
Eine höhere Agilität bedeutet, dass das System flexibler 
auf neue Anforderungen oder Umstellungen reagieren kann.

**Funktionalität:** Die Gesamtheit der Funktionen und Fähigkeiten, 
die ein System bietet, also die Funktionalität, 
die das System für die Nutzer bereitstellt.

**Bedeutung der Pfeile:**
Die Pfeile im Diagramm zeigen den Verlust der Agilität mit 
zunehmender Funktionalität des Systems. 
Je mehr Funktionalität ein System hinzufügt, 
desto weniger agil wird es. Es gibt zwei kritische Punkte im Diagramm:
- C1: Dieser Punkt stellt den Moment dar, in dem der Verlust an Agilität etwa das Fünffache des funktionalen Zugewinns beträgt. Das bedeutet, dass ab diesem Punkt jede Erhöhung der Funktionalität den Verlust an Agilität stark überwiegt.
- C2: Hier wird der Verlust an Agilität so groß, dass der Zugewinn an Funktionalität kaum noch einen positiven Effekt hat. Mit anderen Worten: Jede weitere funktionale Verbesserung macht das System so unflexibel, dass der zusätzliche Nutzen marginal wird.

## Problematik, die Murer et al entdeckt haben:**

Murer et al. entdeckten in ihrer empirischen Forschung, 
dass viele Softwaresysteme im Laufe ihrer Entwicklung 
immer mehr Funktionalität hinzugewinnen, 
was jedoch zu einem erheblichen Verlust der Agilität führt. 
Dies führt dazu, dass das System weniger anpassungsfähig wird und 
zukünftige Änderungen immer aufwendiger und kostspieliger werden. 
Ab einem gewissen Punkt (C2) sind die Funktionsgewinne durch das System zu teuer, 
weil die Verluste in der Agilität überwiegen.

## Mögliche Massnahmen:

**Kontinuierliche Refaktorierung:** Systeme sollten regelmäßig umstrukturiert und optimiert werden, 
um ihre Flexibilität zu bewahren. Durch Refaktorierung können unnötige Komplexitäten beseitigt und 
die Agilität erhöht werden.

**Modularisierung:** Systeme sollten in kleinere, unabhängige Module zerlegt werden. 
Dies ermöglicht es, einzelne Module zu verändern oder zu erweitern, 
ohne das gesamte System zu beeinflussen. So bleibt die Gesamtarchitektur flexibel und agil.

**Managed Evolution:** Dies bedeutet, dass Systeme nicht nur nach funktionalen Anforderungen 
erweitert werden sollten, sondern dass auch die langfristige Wartbarkeit und Agilität beachtet 
werden muss. Änderungen sollten mit Blick auf die zukünftige Entwicklung vorgenommen werden, 
um das System anpassungsfähig zu halten.

**Technische Schulden minimieren:** Technische Schulden entstehen, wenn schnelle und unsaubere 
Lösungen implementiert werden, um kurzfristige funktionale Anforderungen zu erfüllen. 
Murer et al. schlagen vor, technische Schulden frühzeitig anzugehen, 
um langfristige Probleme zu vermeiden und die Agilität des Systems zu sichern.

**Starke Governance:** Es sollte eine klare Governance-Struktur geben, die sicherstellt, 
dass Entscheidungen zur Erweiterung der Funktionalität immer auch die Auswirkungen 
auf die Agilität berücksichtigen.

# Single Responsibility Prinzip (SRP)



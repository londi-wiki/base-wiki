---
weight: 999
title: "Serverless Applications"
description: ""
icon: "article"
date: "2025-01-20T02:00:00+02:00"
lastmod: "2025-01-20T02:00:00+02:00"
draft: false
toc: true
---

# Serverless Applications

**Vorteile**

- Keine Server-/Hardwareverwaltung
- Automatische Skalierung
- Kostenersparnis
- Schnelle Entwicklung und Bereitstellung
- Event-getriebene Architektur
- Höhere Verfügbarkeit und Fehlertoleranz
- Integrierte Sicherheit

**Nachteile**

- Eingeschränkter Zugriff auf Infrastruktur: Falls Hardware Optimierungen angesprochen werden wollen
- Latenz und Cold starts: Beim ersten Start benötigt der erste Aufruf länger, um die Funktion bereitzustellen.
- Laufzeit und Ressourcengrenzen: Max. Laufzeit bei AWS (15min)
- Komplexes Debugging und Monitoring: Da der Code nicht auf einem fix zugewiesenen System läuft, kann das Debugging schwieriger sein.
- Abhängigkeit von einem Anbieter (Vendor Lock-in)
- Kosten können unvorhersehbar sein
- Zustandslosigkeit (ausser man bindet eine externe Datenquelle separat an)
- Limitierte Unterstützung von langen Verbindungen
- Fehlende lokale Entwicklungsparität: Man kann die Funktion lokal nicht gleich laufen lassen wie auf dem Cloud Anbieter. Es gibt zwar Serverless Frameworks (AWS SAM), jedoch bestehen dann nach wie vor Unterschiede zwischen der lokalen und Serverless Umgebung.




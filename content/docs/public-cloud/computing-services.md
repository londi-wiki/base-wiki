---
weight: 999
title: "Computing Services"
description: ""
icon: "article"
date: "2024-10-08T14:45:59+02:00"
lastmod: "2024-10-08T14:45:59+02:00"
draft: false
toc: true
---

## Lernziele
- Verständnis der verschiedenen Cloud-Computing-Dienste, einschließlich ihrer Vor- und Nachteile.
- Anwendung des Konzepts von Serverless Computing für das Hosting von Anwendungen in der Cloud.
- Kenntnisse über die Sicherheitsaspekte von Cloud-Computing-Diensten.

## Isolation von Workloads
In der Cloud teilen sich mehrere Workloads denselben Host. Die Isolation erfolgt auf drei Ebenen:
1. **Workload von Workload**: Verhindert, dass sich Workloads gegenseitig beeinflussen.
2. **Host von Workload**: Schützt den Host vor einem fehlerhaften Workload.
3. **Workload vom Host**: Schutz, falls der Host nicht vertrauenswürdig ist, eine gängige Situation in der Cloud.

## Isolationstechniken
- **Hardware Security Modules (HSMs)**: Für Schlüsselmanagement, jedoch nicht weit verbreitet in der Cloud.
- **FPGAs**: Programmierbare Chips, schwierig zu entwickeln und nicht oft verwendet.
- **Trusted Execution Environments (TEEs)**: In modernen CPUs weit verbreitet, schaffen vertrauenswürdige Ausführungsumgebungen.

## Confidential Computing
- Schützt sensible Daten während der Verarbeitung, indem der Code in isolierten Umgebungen ausgeführt wird, die vor externen Eingriffen geschützt sind.
- Dies erfordert einen speziellen Software-Stack.

## Compute Services
1. **Virtuelle Maschinen**: Klassische Infrastruktur als Service (IaaS), bei der feste Instanztypen mit flexiblen Speicher- und Netzwerkkonfigurationen bereitgestellt werden.
2. **Serverless Functions**: Eine serverlose Architektur ermöglicht die Ausführung von Code ohne Verwaltung von Servern. Code wird hochgeladen und automatisch ausgeführt, basierend auf Ereignissen oder direkten Aufrufen.

## Skalierung und Verwaltung
- **Auto-Scaling**: Automatische Skalierung von Instanzen basierend auf der Nachfrage.
- **Snapshots**: Erstellen von Speicherabbildern für Backups und Tests, unabhängig vom Betriebssystem.
- **Netzwerk**: Unterstützung für IPv4 und IPv6, mit der Möglichkeit, IP-Adressen und Netzwerkkonfigurationen zu verwalten.

## Sicherheit
- Die Sicherheitsverantwortung in der Cloud wird zwischen dem Anbieter und dem Nutzer aufgeteilt.
- Aspekte wie Infrastruktursicherheit, Identitäts- und Zugriffsmanagement sowie Datenschutz sind von zentraler Bedeutung.

## Anwendungsfälle
- **Serverless**: Ideal für die Verarbeitung von Dateien, Datenanalyse und das Hosten von Backend-Logiken für Web- und mobile Anwendungen.
- **Virtuelle Maschinen**: Werden in skalierbaren, fehlertoleranten Architekturen für verschiedene Anwendungen wie Datenbanken und Streaming-Dienste genutzt.

## Überwachung und Fehlerbehandlung
- Cloud-Dienste bieten umfangreiche Überwachungsmöglichkeiten, um Leistung, Zuverlässigkeit und Verfügbarkeit zu gewährleisten.
- Für serverlose Anwendungen werden Fehler detailliert an den Aufrufer zurückgemeldet, und es können benutzerdefinierte Fehlerbehandlungsmechanismen implementiert werden.

## Zusammenfassung
- Cloud-Computing-Dienste bieten flexible, skalierbare und sichere Lösungen für unterschiedliche Workloads.
- Durch die Nutzung von sowohl virtuellen Maschinen als auch serverlosen Architekturen können Nutzer verschiedene Anwendungsfälle effizient abdecken.

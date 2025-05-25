---
weight: 999
title: "Least Privilege"
description: ""
icon: "article"
date: "2024-10-26T14:17:22+02:00"
lastmod: "2024-10-26T14:17:22+02:00"
draft: false
toc: true
---

# Principle of Least Privilege" (PoLP)

Grundkonzept:

- Jeder Benutzer, Prozess oder Service erhält nur die minimal notwendigen Rechte
- Nur die Berechtigungen, die für die jeweilige Aufgabe erforderlich sind
- Zugriffe werden standardmässig verweigert, ausser sie werden explizit gewährt

## Praktische Umsetzung nach Bereichen

1. Betriebssysteme

- Normale Benutzer arbeiten ohne Admin-Rechte
- Separate Accounts für administrative Tätigkeiten
- Temporäre Rechteerhöhung nur bei Bedarf (sudo in Linux)
- Dateisystemberechtigungen minimal halten
- Services mit eingeschränkten Benutzerkonten ausführen

2. Server

- Dedizierte Service-Accounts für jeden Dienst
- Root/Administrator-Zugang stark einschränken
- Netzwerkports nur öffnen wenn nötig
- Firewall-Regeln nach Whitelist-Prinzip
- Separate Benutzer für Wartung und Monitoring

3. Datenbanken

- Unterschiedliche Nutzerrollen (Read, Write, Admin)
- Schema-spezifische Berechtigungen
- Row-Level Security wo sinnvoll
- Separate Accounts für Anwendungen und Administratoren

4. Microservices/Container

- Container nur mit notwendigen Bibliotheken
- Read-Only Filesysteme wo möglich
- Netzwerkisolation zwischen Services
- Keine privilegierten Container wenn vermeidbar

5. Cloud-Umgebungen

- IAM-Rollen mit minimalen Rechten
- Temporäre Credentials statt permanenter Schlüssel
- Resource-basierte Policies
- Segmentierung nach Umgebungen (Dev/Prod)

## Best practice

1. Dokumentation

- Alle Berechtigungen dokumentieren
- Begründung für Rechte festhalten
- Regelmässige Überprüfung

2. Monitoring

- Zugriffe protokollieren
- Ungewöhnliche Aktivitäten erkennen
- Regelmässige Audits durchführen

3. Automatisierung

- Automatische Rechtevergabe nach Rollen
- Zentrale Verwaltung von Zugriffsrechten
- Automatische Erkennung ungenutzter Rechte

4. Prozesse

- Standardisierte Prozesse für Rechtevergabe
- Regelmässige Überprüfung und Anpassung
- Dokumentierte Eskalationswege


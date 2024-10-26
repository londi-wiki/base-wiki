---
weight: 999
title: "Acid Base"
description: ""
icon: "article"
date: "2024-10-26T14:17:13+02:00"
lastmod: "2024-10-26T14:17:13+02:00"
draft: false
toc: true
---

# ACID (Atomicity, Consistency, Isolation, Durability)

ACID ist das traditionelle Datenbankmodell:

1. Atomicity (Atomarität):
- Transaktionen werden entweder vollständig oder gar nicht ausgeführt
- Bei Fehlern wird alles rückgängig gemacht (Rollback)

2. Consistency (Konsistenz):
- Die Datenbank ist immer in einem gültigen Zustand
- Alle definierten Regeln und Constraints werden eingehalten

3. Isolation (Isolation):
- Parallele Transaktionen beeinflussen sich nicht gegenseitig
- Jede Transaktion arbeitet, als wäre sie alleine

4. Durability (Dauerhaftigkeit):
- Erfolgreich abgeschlossene Transaktionen sind permanent gespeichert
- Daten gehen auch bei Systemausfällen nicht verloren

# BASE (Basically Available, Soft state, Eventually consistent)

Base ist das neuere Konzept:

1. Basically Available:
- System ist grundsätzlich verfügbar
- Teilausfälle werden toleriert

2. Soft State:
- Daten können temporär inkonsistent sein
- Der Zustand kann sich auch ohne Eingaben ändern

3. Eventually Consistent:
- Konsistenz wird nicht sofort, aber nach einer gewissen Zeit erreicht
- Das System konvergiert zu einem konsistenten Zustand

## Vergleich und Einsatzgebiete:

ACID eignet sich für:

- Finanztransaktionen
- Buchungssysteme
- Kritische Geschäftsprozesse
- Wenn **Datenkonsistenz** höchste Priorität hat

BASE eignet sich für:

- Soziale Medien
- Big Data Anwendungen
- Systeme mit hoher Skalierbarkeit
- Wenn **Verfügbarkeit** wichtiger ist als sofortige Konsistenz

Die Wahl zwischen ACID und BASE hängt von deinen spezifischen Anforderungen ab:

Braucht es absolute Datenkonsistenz? → ACID
Ist Skalierbarkeit und Verfügbarkeit wichtiger? → BASE
Kann temporäre Inkonsistenzen toleriert werden? → BASE
Wird mit kritischen Geschäftsdaten gearbeitet? → ACID

---
weight: 999
title: "12 Factor App"
description: ""
icon: "article"
date: "2026-04-13T09:09:59+00:00"
lastmod: "2026-04-13T09:09:59+00:00"
draft: false
toc: true
---

# 12-Factor App Prinzipien

Die 12-Factor-App-Methodik wurde 2011 von Heroku entwickelt und ist der de-facto Standard für cloud-native, containerisierte Applikationen. Die Prinzipien sind direkt relevant für unsere **P3 Container First** Architektur-Guideline und die Anforderung, dass alle selbst betriebenen Lösungen auf OpenShift lauffähig sein müssen.

> **Quelle:** [12factor.net](https://12factor.net) – Heroku (2011)

---

## Die 12 Faktoren

### I – Codebase
Eine Codebase, versioniert in einem Repository. Viele Deployments davon – aber immer nur eine einzige Quelle der Wahrheit.

**Implikation:** Kein Copy-Paste von Code zwischen Umgebungen. Feature-Flags und Konfiguration steuern das Verhalten pro Umgebung.

---

### II – Abhängigkeiten
Alle Abhängigkeiten explizit deklarieren und isolieren. Keine impliziten System-Pakete voraussetzen.

**Implikation:** `package.json`, `pom.xml`, `requirements.txt` etc. müssen vollständig und aktuell sein. Keine Annahmen über vorinstallierte Tools auf dem Host.

---

### III – Konfiguration ⚠️
Konfiguration in Umgebungsvariablen speichern – nie im Code. Alles was zwischen Umgebungen variiert, gehört in env vars.

**Implikation:** Häufigster Stolperstein bei OpenShift-Migrationen. Hardcodierte URLs, Passwörter oder Umgebungsbezeichnungen im Code sind ein Blocker.

---

### IV – Backing Services
Datenbanken, Queues, externe APIs als angehängte Ressourcen behandeln – austauschbar über Konfiguration, nicht über Code.

**Implikation:** Lokale Datenbank und Cloud-Datenbank sind identisch aus Sicht der App. Wechsel erfolgt nur via Konfiguration.

---

### V – Build, Release, Run
Build-Stage, Release-Stage und Run-Stage strikt trennen. Keine Code-Änderungen zur Laufzeit – jede Änderung durchläuft den Build-Prozess.

**Implikation:** CI/CD-Pipelines müssen diese drei Phasen explizit abbilden. Hotfixes direkt im Container sind verboten.

---

### VI – Prozesse ⚠️
App als einen oder mehrere zustandslose Prozesse ausführen. Kein lokaler State, kein Sticky-Session – State gehört in Backing Services.

**Implikation:** Häufigster Stolperstein. Applikationen, die State im lokalen Filesystem oder Arbeitsspeicher halten, müssen vor der Container-Migration refaktoriert werden.

---

### VII – Port Binding
Services über Port-Binding selbst bereitstellen – kein externer Webserver nötig. Die App ist selbst der Server.

**Implikation:** Keine Abhängigkeit auf Apache/IIS als Laufzeitumgebung. Die App startet eigenständig auf einem konfigurierbaren Port.

---

### VIII – Nebenläufigkeit
Skalierung über Prozess-Modell – horizontale Skalierung statt vertikaler. Verschiedene Prozesstypen für verschiedene Workloads.

**Implikation:** OpenShift skaliert über Replicas. Die App muss mehrfach parallel laufen können ohne Konflikte.

---

### IX – Einweggebrauch
Prozesse sind schnell startbar und sauber stoppbar (graceful shutdown). Robustheit gegenüber plötzlichem Tod ist Pflicht.

**Implikation:** SIGTERM muss sauber behandelt werden. Keine laufenden Transaktionen dürfen beim Pod-Neustart verloren gehen.

---

### X – Dev/Prod-Parität ⚠️
Entwicklung, Staging und Produktion so ähnlich wie möglich halten. Unterschiede zwischen Umgebungen sind der häufigste Fehlergrund.

**Implikation:** Häufigster Stolperstein. "Works on my machine" ist kein akzeptables Argument. Container lösen dieses Problem strukturell.

---

### XI – Logs
Logs als Ereignisstrom behandeln – einfach auf stdout schreiben, nie in Dateien. Die Plattform kümmert sich um Routing und Speicherung.

**Implikation:** Kein Log4j-File-Appender in Produktion. OpenShift/EFK-Stack übernimmt Log-Aggregation.

---

### XII – Admin-Prozesse
Einmalige Admin-Tasks (Migrationen, Skripte) als eigenständige Prozesse im gleichen Release-Kontext ausführen – nicht als Sonderfall im laufenden Betrieb.

**Implikation:** DB-Migrationen laufen als Init-Container oder Job in OpenShift, nicht manuell per SSH auf dem Server.

---

## Relevanz für unsere Zielarchitektur

| Faktor | Relevanz | Bemerkung |
|--------|----------|-----------|
| III – Konfiguration | Hoch | Häufigster Blocker bei OpenShift-Migration |
| VI – Zustandslose Prozesse | Hoch | Kritisch für horizontale Skalierung |
| X – Dev/Prod-Parität | Hoch | Container lösen dies strukturell |
| IX – Graceful Shutdown | Mittel | Wichtig für Rolling Deployments |
| XI – Logs | Mittel | Integration mit zentralem Log-Stack |
| I–XII (alle) | Richtlinie | Neue Eigenentwicklungen müssen alle 12 Faktoren erfüllen |

> **Architektur-Entscheid:** Neue Eigenentwicklungen und migrierte Systeme müssen alle 12 Faktoren erfüllen. Bestehende Systeme werden im Rahmen der Gap-Analyse gegen diese Kriterien bewertet.

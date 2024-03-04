---
weight: 999
title: "Http Summary"
description: ""
icon: "article"
date: "2024-03-04T09:26:16+01:00"
lastmod: "2024-03-04T09:26:16+01:00"
draft: false
toc: true
---

## Was ist HTTP?

- verbindungsloses Protokoll
- zustandsloses Protokoll

## Unterschied GET/POST

- GET sendet Daten über die URL, während POST Daten im Body des Requests sendet.
- GET ist eine sichere Methode, während POST unsicher ist

## Welche Aussagen sind korrekt?

- HTTP Methode, die safe ist, ist auf idempotent

## Maximal Grösse bei POST?

- Unbegrenzt (z.B. mit chunked encoding)

## Sind auch weitere HTTP Methoden erlaubt?

- Ja, zum Beispiel: COPY, MOVE, LOCK, ...

## Unterschied GET/POST Request

- GET Request kann man nur eine begrenzte Anzahl Daten an den Server geschickt werden, mit einem Post Request hingegen beliebig grosse Dateien

## Welche der folgenden Methoden sind HTTP Methoden?

- TRACE
- GET
- OPTION
- POST
- PATCH
- DELETE
- HEAD
- PUT
- CONNECT

## Idempotente Methoden

- GET, HEAD, PUT, DELETE, OPTIONS sind idempotent
- Wenn idempotente Methoden mehrfach ausgeführt werden, so haben sie auf dem Server denselben Effekt wie wenn sie nur einmal ausgeführt werden.

## safe

- GET, HEAD, OPTIONS
- MMethoden welche keinen Effekt auf dem Server haben

## 500er

- Servererror

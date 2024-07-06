---
weight: 999
title: "Http Servlets Summary"
description: ""
icon: "article"
date: "2024-03-11T09:31:23+01:00"
lastmod: "2024-03-11T09:31:23+01:00"
draft: false
toc: true
---

## service methode überschreiben

- OPTIONS

Ausgabe: "OPTIONS"

## Patch methode 

- doPatch gibt es nicht: deshalb service-methode überschreiben

## content length

- content length: 5
- println("1234567890")

Ausgabe: "12345"

Wegen der Logik vom Servlet.

## doGet mit print anstatt println

w.print("1234567890")

Ausgabe: 
- Transfer-encoding: chunked
- Content-length: 10
- "und nach einer gewissen Zeit terminiert curl mit Fehlermeldung: curl(18) transfer closed with outstanding read data remaining."


## GET thread mit println aber unendlich

Daten werden in einen Buffer geschrieben und an den Client gesendet wenn dieser voll ist (nach ~1500 Zeichen)
Ausgabe: 
- Nach etwa 80 sekunden kommen die ersten 0..1535 Ausgaben und dann wartet es wieder bis zu den nächsten ~1500 Zeichen...
- Lösung: nach jedem println ein flush ausführen.

Kann man mit telnet testen: setlocalecho on:
```bash
GET /simple/go/ HTTP/1.1
HOST: localhost
```


## println und flush in einem loop

mit telnet sieht man:

```bash
1
0
1
1
1
2
1
3
...
```

## servlets thread-safe?

- ja, solange service oder doGet, ... nur auf lokale Daten zugreifen


## webxml

GET localhost:8080/ds/currency/convert

mögliche url patterns:
- /*
- /currency/convert

Wenn die Applikation im ROOT liegt, sieht es anders aus.

## loadOnStartup

- Reihenfolge wann die Servlets geladen und initialisiert werden sollen

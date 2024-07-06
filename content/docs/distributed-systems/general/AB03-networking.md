---
weight: 999
title: "AB03 Networking"
description: ""
icon: "article"
date: "2024-02-19T10:33:44+01:00"
lastmod: "2024-02-19T10:33:44+01:00"
draft: false
toc: true
---

# Aufgabe 1

```bash
> netstat -a -n | grep 1234

tcp        0      0 127.0.0.1:44962         127.0.0.1:1234          ESTABLISHED
tcp        0      0 127.0.0.1:41844         127.0.0.1:1234          ESTABLISHED
tcp        0      0 127.0.0.1:33832         127.0.0.1:1234          ESTABLISHED
tcp6       0      0 :::1234                 :::*                    LISTEN
tcp6       0      0 127.0.0.1:1234          127.0.0.1:44962         ESTABLISHED
tcp6       0      0 127.0.0.1:1234          127.0.0.1:33832         ESTABLISHED
tcp6       0      0 127.0.0.1:1234          127.0.0.1:41844         ESTABLISHED
```

Was können Sie über die Sockets der Echo-Klienten aussagen?

> Der Client erstellt eine Verbindung zum Server und definiert ebenfalls einen Socket (z.B. 44962, ...).
> Man sieht in der Ausgabe sowohl die Clients auch als die Server und den Port auf dem aktuell gehört wird.

# Aufgabe 2

a) Können zwei Echo Klienten auf derselben Maschine denselben lokalen Port verwenden (z.B. Port 
7777) um auf den Echoserver (mit Port 1234) zuzugreifen? 

> Nein: Address already in use: bind
 
b) Kann ein Port auf einem Rechner sowohl für einen ServerSocket als auch für einen Klienten Socket 
verwendet werden? Unterscheidet ein System zwischen ausgehenden und eingehenden Ports?

> Nein: Address already in use: bind

# Aufgabe 3

Wie verhält sich EchoServer1 (non-threaded) wenn der Backlog auf 2 gesetzt wird und mehrere Kli-
enten geöffnet (aber nicht geschlossen) werden?

> Wenn drei Clients verbindet werden, erhält dieserr einen Fehler. Connection refused: connect

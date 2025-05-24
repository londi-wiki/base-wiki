---
weight: 999
title: "Tcp Ip"
description: ""
icon: "article"
date: "2024-11-01T21:41:32+01:00"
lastmod: "2024-11-01T21:41:32+01:00"
draft: false
toc: true
---

# TCP IP

## TCP-Verbindungsaufbau (Three-Way-Handshake)

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    Note over C,S: 1. Verbindungsaufbau (Three-Way Handshake)
    C->>S: SYN (seq=x)
    S->>C: SYN-ACK (seq=y, ack=x+1)
    C->>S: ACK (ack=y+1)
```

## TCP-Datentransfer

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    Note over C,S: 2. Datentransfer
    C->>S: SEQ=100, 100 Bytes
    S->>C: ACK=200
    C->>S: SEQ=200, 100 Bytes
    S->>C: ACK=300
    Note over C,S: Sliding Window ermöglicht mehrere unbestätigte Pakete

```

## TCP-Fehlerbehandlung

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    Note over C,S: 3. Fehlerbehandlung
    C->>S: SEQ=400, 100 Bytes
    Note over S: Paket verloren
    C->>S: SEQ=500, 100 Bytes
    S->>C: ACK=400 (Duplicate ACK)
    Note over C: Timeout oder<br/>3 Duplicate ACKs
    C->>S: SEQ=400, 100 Bytes (Retransmission)
    S->>C: ACK=600

```

## TCP-Verbindungsabbau (Four-Way-Handshake)

```mermaid
sequenceDiagram
    participant C as Client
    participant S as Server

    Note over C,S: 4. Verbindungsabbau
    C->>S: FIN
    S->>C: ACK
    S->>C: FIN
    C->>S: ACK
    Note over C,S: Verbindung beendet

```

## Überlaststeuerung (Congestion Control)

Die an der Datenübertragung beteiligten Kommunikationspartner, in der Regel Client und Server, wissen nicht, wie viel Übertragungskapazität auf der Übertragungsstrecke zur Verfügung steht.

Angenommen, Sender und Empfänger seien beide an Gigabit Ethernet Schnittstellen
angeschlossen. Irgendwo auf dem Weg dazwischen sei aber ein viel langsamerer Link
(z.B. 64 kbit/s). Wie merkt der Sender, dass er Daten nur mit der Bandbreite des
langsamen Links schicken kann?

Der Sender erkennt die verfügbare Bandbreite durch TCP's Überlastkontrolle (Congestion Control). Hier ist der Ablauf:

1. TCP's Überlastkontrolle basiert auf dem Prinzip der Paketverluste und Verzögerungen:

2. Was passiert:
- Wenn der Sender Daten mit 1 Gbit/s sendet, aber der langsamste Link nur 64 kbit/s verarbeiten kann, stauen sich die Pakete in den Routern vor dem langsamen Link
- Die Router-Puffer füllen sich
- Wenn die Puffer voll sind, werden neue Pakete verworfen
- Diese Paketverluste interpretiert TCP als Überlastung (Congestion)

3. TCP's Reaktion:
- Bei Paketverlusten reduziert TCP seine Senderate (Congestion Window wird verkleinert)
- Bei erfolgreicher Übertragung erhöht TCP die Rate langsam wieder (Slow Start bzw. Congestion Avoidance)
- Dieser Prozess pendelt sich auf die verfügbare Bandbreite ein

4. Zusätzliche Indikatoren:
- Steigende Round-Trip Times durch gefüllte Puffer (Bufferbloat)
- Verzögerte oder doppelte ACKs
- Explicit Congestion Notification (ECN), falls unterstützt

Durch diesen Mechanismus passt sich TCP automatisch an die langsamste Verbindung der Strecke an, auch wenn Sender und Empfänger selbst an schnelleren Links angeschlossen sind.

## Datenrate berechnen

**Beispiel:**

1. Die maximale TCP-Datenrate wird durch folgende Formel bestimmt:
   Maximale Datenrate = Fenstergrösse / Round-Trip Time

2. Gegeben:
    - Round-Trip Time (RTT) = 100 ms = 0,1 Sekunden
    - Maximale Fenstergrösse ohne Window Scaling = 65535 Bytes (nicht 65636)

3. Berechnung:
   Maximale Datenrate = 65535 Bytes / 0,1 Sekunden
   = 655350 Bytes pro Sekunde
   ≈ 5,24 Megabytes pro Sekunde
   ≈ 41,94 Megabit pro Sekunde

Die maximale theoretische Datenrate beträgt also etwa 41,94 Mbit/s, 
unabhängig von der tatsächlich verfügbaren Bandbreite der Verbindung.
Dies zeigt eine wichtige Einschränkung des TCP-Protokolls ohne Window Scaling: 
Selbst wenn die physikalische Leitung eine höhere Bandbreite erlauben würde, 
kann TCP ohne Window Scaling diese nicht ausnutzen.

Deshalb wurde Window Scaling als Erweiterung eingeführt, 
um höhere Durchsatzraten auf Verbindungen mit hohem Bandwidth-Delay-Produkt zu ermöglichen.


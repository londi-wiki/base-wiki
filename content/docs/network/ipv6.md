---
weight: 999
title: "Ipv6"
description: ""
icon: "article"
date: "2024-10-16T21:04:00+02:00"
lastmod: "2024-10-16T21:04:00+02:00"
draft: false
toc: true
---


# Aufbau

- 128 Bit in hexadezimaler Schreibweise
- Format: x:x:x:x:x:x:x:x (jedes x besteht aus einem vierstelligem hexadezimalem Wert)
- Ein Segment von 16 Bit oder vier Hexadezimalwerten wird "Hextet" genannt.

**Beispiel**

```bash
2001:0db8:0000:1111:0000:0000:0000:0200
2001:0db8:0000:00a3:abcd:0000:0000:1234 
```

## Abkürzen

- Führende Nullen eines Sextets können weggelassen werden:
  - 01ab -> 1ab
  - 09f0 -> 9f0
  - 0a00 -> a00
  - 00ab -> ab
- Doppelpinkt kann eine einzelne, zusammenhängende Zeichenkette aus einem oder mehreren 16 Bit Hextets ersetzen, die ausschliesslich aus Nullen bestehen.

```bash
2001 : 0db8 : 0000 : 1111 : 0000 : 0000 : 0000 : 0200
2001 :  db8 :    0 : 1111 :    0 :    0 :    0 :  200
2001 :  db8 :    0 : 1111 ::                      200
```

## Adresstypen

- Unicast: Eindeutige Schnittstelle für ein IPv6 fähiges Gerät
- Multicast: Um IPv6 Pakete an mehrere Ziele zu senden
- Anycast: Beliebige IPv6 Unicast Adresse, die mehrere Geräten zugewiesen wird. Ein Paket, das an eine Anycast Adresse gesendet wird, wird an das nächstgelegene Gerät mit dieser Adresse weitergeleitet.

Bei IPv6 gibt es **keine** Broadcast Adressen, jedoch aber eine IPv6-All-Nodes-Multicast-Adresse.

## Präfixlänge

Eine IPv6 Adresse besteht aus zwei Teilen:
- Prefix: Für das Routing
- IF-ID (Interface Identifier): Für die Adressierung

Die Präfixlänge gibt an, wie viele der ersten Bits einer IPv6-Adresse den Netzwerkanteil 
(also das Präfix) darstellen. Dies ist vergleichbar mit der Netzmaske bei IPv4.
Die Präfixlänge wird in CIDR-Notation angegeben und erscheint nach einem Schrägstrich (z. B. /64).

Beispiel: Bei einer Adresse wie `2001:db8::/64` bedeutet das /64, 
dass die ersten 64 Bits der Adresse das Präfix (also den Netzwerkteil) darstellen. 
Die restlichen 64 Bits werden für den Interface Identifier verwendet, 
um einzelne Geräte innerhalb dieses Netzwerks zu identifizieren.

Die Präfixlänge kann theoretisch zwischen **0** und **128** liegen, wobei 0 bedeutet, 
dass gar kein Präfix definiert ist, 
und 128 eine vollständig definierte Adresse darstellt.

## Präfix

Das Präfix in einer IPv6-Adresse ist der Teil, der den Netzwerkanteil repräsentiert. 
Dieser Teil ist für alle Geräte im selben Subnetz identisch und wird von Routern verwendet, 
um Pakete zu den richtigen Netzwerken zu leiten.

**Global Unicast Adressen (öffentliche Adressen):** 

Diese Adressen haben oft ein Präfix von /48 oder /64. Beispiel: `2001:db8:abcd::/64`.
- `2001:db8:abcd::` ist das Präfix, das für das Netzwerk verwendet wird.
- Dieses Präfix ist für alle Geräte in diesem Netzwerk gleich. Es definiert das Subnetz, in dem sich die Geräte befinden.

**Link-Local Adressen (LLA):** 

Diese haben das Präfix fe80::/10. Beispiel: `fe80::1a2b:3c4d:5e6f:7f8h`.
- Hier ist fe80:: das Präfix, das anzeigt, dass es sich um eine Link-Local-Adresse handelt, 
die nur im lokalen Netzwerksegment verwendet wird.

## Interface Identifier (IF-ID)

Der Interface Identifier (IF-ID) ist der Teil der IPv6-Adresse, 
der ein Gerät innerhalb eines Netzwerks eindeutig identifiziert. 
Dieser Teil wird oft aus der MAC-Adresse des Geräts generiert oder kann zufällig bzw. 
manuell konfiguriert werden. In den meisten Fällen sind die letzten 64 Bits einer IPv6-Adresse 
für den Interface Identifier reserviert.

**Interface Identifier und EUI-64:**

Früher wurde häufig der EUI-64-Algorithmus verwendet, 
um den Interface Identifier aus der MAC-Adresse des Geräts zu generieren:

- Die 48-Bit MAC-Adresse des Geräts (z. B. `00:11:22:33:44:55`) wird in einen 64-Bit-Wert umgewandelt, 
indem `ff:fe` in die Mitte eingefügt wird, was `00:11:22:ff:fe:33:44:55` ergibt.
- Zusätzlich wird das 7. Bit des ersten Bytes invertiert, um sicherzustellen, dass die Adresse korrekt für IPv6 verwendet werden kann.

In modernen Netzwerken wird diese Methode oft durch Privacy Extensions ersetzt, die temporäre, 
zufällige Interface Identifiers generieren, um die Privatsphäre der Nutzer zu schützen.

## Unique Local Address (ULA)

- Eindeutig lokale Adressen

## Global Unicast Address (GUA)

- Global eindeutige Adressen

## Link Local Address (LLA)

Eine IPv6-Link-Local-Adresse (LLA) ermöglicht es einem Gerät, mit anderen IPv6-fähigen
Geräten auf demselben Link und nur auf diesem Link (Subnetz) zu kommunizieren.

# IP Verteilung

## Router Solicitation (RS) und Router Advertisement (RA)

Router Solicitation (RS) und Router Advertisement (RA) sind zentrale Nachrichten im 
Neighbor Discovery Protocol (NDP) von IPv6. Sie ermöglichen die automatische Konfiguration 
von Geräten in einem Netzwerk und sind für die Adressvergabe und die Router-Erkennung entscheidend.

**Router Solicitation (RS)** ist eine Nachricht, die von einem IPv6-Gerät (Host) gesendet wird, 
um Router im Netzwerk zu finden und Konfigurationsinformationen anzufordern.

**Router Advertisement (RA)** ist die Antwort des Routers auf eine RS-Nachricht oder 
wird periodisch von Routern gesendet, um den Hosts im Netzwerk wichtige Netzwerkinformationen zur 
Verfügung zu stellen.

## SLAAC

Stateless Address Autoconfiguration (SLAAC) ist eine Methode, 
die in IPv6 verwendet wird, um Geräten zu ermöglichen, 
ihre eigene IPv6-Adresse automatisch und ohne die Notwendigkeit eines DHCPv6-Servers zu konfigurieren. 
SLAAC ermöglicht es einem Gerät, eine IPv6-Adresse und andere notwendige Netzwerkinformationen zu erhalten, 
indem es auf Informationen hört, die vom Router über Router Advertisement (RA)-Nachrichten bereitgestellt werden.

Vorgehen:

1. Link Local Address (LLA) vergeben
   - Präfix: `fe80::/10`
   - Interface Identifier (die letzten 64 Bits der Adresse): meist auf Basis der MAC-Adresse, EUI-64 Format
2. Senden einer Router Solicitation (RS) Nachricht
   - RS Nachricht an Multicast Adresse `ff02::2` (alle Router im lokalen Netzwerk) senden
   - Informationen erhalten:
     - Gültige IPv6 Präfix
     - DHCPv6?
3. Empfangen einer Router Advertisement (RA) Nachricht
   - Router antwortet auf RS Nachricht (oder sendet periodisch unaufgefordert) eine RA Nachricht an das Gerät
   - Nachricht enthält:
     - IPv6 Präfix, Beispiel: `2001:db8:abcd::/64`
     - Router Adresse welche als Standardgateway verwendet wird
     - Gültigkeitsdauer: Wie lange die Präfix gültig ist und wann es erneuert werden muss
     - SLAAC Flags:
       - A-Flag (Autonomous Flag): Gibt an, dass das Gerät seine eigene IPv6-Adresse mithilfe von SLAAC erstellen kann.
       - M-Flag (Managed Flag): Gibt an, dass DHCPv6 verwendet werden sollte, um eine Adresse zu beziehen (wird bei SLAAC nicht benötigt).
       - O-Flag (Other Flag): Gibt an, dass DHCPv6 verwendet werden sollte, um zusätzliche Konfigurationsinformationen (z. B. DNS-Server) zu beziehen, auch wenn SLAAC für die Adresszuweisung verwendet wird.
4. Erstellen einer globalen IPv6 Adresse
   - Basierend auf den erhaltenen Informationen erstellt das Gerät seine eigene globale IPv6 Adresse
   - Präfix: Verwendet das vom Router bereitgestellte Präfix
   - Interface Identifier: Der zweite Teil der Adresse wird durch das Gerät generiert, oft MAC-Adresse oder mit zufällig generierte Zahlen (Privacy Extensions)
5. Duplicate Address Detection (DAD)
- Bevor das Gerät die neue Adresse verwendet, führt es eine Duplicate Address Detection (DAD) durch, um sicherzustellen, dass keine andere Station im Netzwerk bereits dieselbe Adresse verwendet.
- Dies geschieht, indem das Gerät eine spezielle Neighbor Solicitation-Nachricht an die Multicast-Adresse sendet, die seiner neuen IPv6 Adresse entspricht.
- Wenn keine Antwort auf diese Nachricht zurückkommt, kann das Gerät sicher sein, dass die Adresse einzigartig ist und sie verwenden.


## Stateless DHCPv6 / Stateful DHCPv6

Stateless DHCPv6 ergänzt SLAAC, indem es Geräten ermöglicht, 
zusätzliche Konfigurationsinformationen zu erhalten, die SLAAC allein nicht bereitstellen kann. 
Dies betrifft Informationen wie DNS-Server, NTP-Server oder andere Konfigurationsdetails, 
die nicht in den Router Advertisement (RA)-Nachrichten enthalten sind.

Funktionsweise von Stateless DHCPv6:
- Ein Gerät, das seine Adresse über SLAAC konfiguriert hat, kann eine DHCPv6 Information Request-Nachricht an einen Stateless DHCPv6-Server senden.
- Der stateless DHCPv6-Server antwortet mit den zusätzlichen Informationen, die das Gerät benötigt, wie z. B. die IPv6-Adressen der DNS-Server.

**Stateless DHCPv6 liefert keine IP-Adressen.** Stattdessen stellt es nur zusätzliche Informationen bereit, während die IPv6-Adresse weiterhin durch SLAAC konfiguriert wird.

**Unterschied zu Stateful DHCPv6:**

- Stateful DHCPv6: Ähnlich wie DHCP bei IPv4, wo der Server sowohl die IP-Adresse als auch andere Netzwerkinformationen zuweist.
- Stateless DHCPv6: Der Server weist keine IP-Adressen zu. Die Adresskonfiguration erfolgt durch SLAAC, und der Server liefert nur zusätzliche Informationen wie DNS-Server.

Einsatz von SLAAC und stateless DHCPv6

In vielen Netzwerken werden SLAAC und Stateless DHCPv6 kombiniert, um sowohl die IPv6-Adresse als auch die zusätzlichen Netzwerkinformationen zu konfigurieren. Dies wird oft durch die Verwendung von Flags in den Router Advertisement (RA)-Nachrichten gesteuert:

- O-Flag (Other Configuration Flag): Wenn dieses Flag in der RA-Nachricht gesetzt ist, signalisiert es dem Gerät, dass es **stateless DHCPv6** verwenden sollte, um zusätzliche Informationen wie DNS-Server zu erhalten.
- M-Flag (Managed Flag): Wenn dieses Flag gesetzt ist, weist es das Gerät an, **stateful DHCPv6** zu verwenden, um sowohl die IP-Adresse als auch andere Netzwerkinformationen vom DHCPv6-Server zu beziehen.

# Subnetz

## Warum subnetz?

- Für die Organisation und effiziente Verwaltung von Netzwerken
- Durch die Aufteilung eines Netzwerks in Subnetze können Administratoren das Netzwerk strukturieren und die Adressverteilung besser steuern.
- Subnetze ermöglichen eine bessere Kontrolle und Sicherheit innerhalb eines Netzwerks
- IPv6-Subnetze vereinfachen das Routing und die Verwaltung von Netzwerken
- IPv6 bietet einen so großen Adressraum, dass Subnetze problemlos erstellt werden können, ohne sich Sorgen um eine knappe Anzahl von Adressen zu machen.
- Ein häufiges Szenario, in dem Subnetze verwendet werden, ist die Trennung von bestimmten Diensten.
- IPv6 unterstützt neben dem klassischen Unicast-Routing auch Multicast und Anycast. Diese Technologien können besonders nützlich sein, wenn sie in einem klar strukturierten Netzwerk mit Subnetzen eingesetzt werden.
- Durch die Verwendung von Subnetzen kann ein Netzwerk strukturiert geplant und einfach dokumentiert werden.

## Wie geht das?

**Grundbegriffe:**
- Präfix: Netzwerkteil einer IPv6 Adresse. Es wird durch die Anzhal der festen Bits der Adresse festgelegt, z.B. /64 bedeutet, dass die ersten 64 Bits das Netzwerk darstellen.
- Präfixlänge: Gibt an wie viele Bits für den Netzwerkteil verwendet werden. Die restlichen Bits stehen für den Host- oder Interface Identifier zur Verfügung.
- Subnetz: Eine Unterteilung eines grösseren Netzwerks in kleinere, logisch getrennte Einheiten.
- Interface Identifier: Der Teil der IPv6 Adresse, der das spezifische Gerät innerhalb eines Netzwerks identifiziert. Normalerweise 64 Bits lang.

**Beispiel Subnetting:**

Präfix: `2001:db8:abcd::/48`

- Die ersten 48 Bits der Adresse sind fest und für das Netzwerk verwendet
- Die restlichen 80 Bits (128-48) können für Subnetze und Geräte verwendet werden
- In der Praxis werden die nächsten 16 Bits oft für Subnetting verwendet, um mehrere Subnetze innerhalb dieses Netzwerks zu erstellen. Das ergibt ein /64-Subnetz, was in IPv6 der Standard für die Netzwerkkonfiguration ist.

### Vorgehen

1. Definieren vom Hauptpräfix

Z.B.: `2001:db8:abcd::/48` -> Die ersten 48 Bits sind festgelegt.

2. Anzahl Subnetze definieren

Von den verbleibenden 80 Bits können 16 Bits für die Subnetze verwendet werden.

Dies ergibt: 2^16 = 65'536 Subnetze.

Jedes Subnetz hätte das Präfix /64, da 48 + 16 = 64.

3. Erstellen der Subnetze

Beispiel:

```bash
Subnetz 1: 2001:db8:abcd:0001::/64
Präfix: 2001:db8:abcd:0001::/64

Subnetz 2: 2001:db8:abcd:0002::/64
Präfix: 2001:db8:abcd:0002::/64

Subnetz 3: 2001:db8:abcd:0003::/64
Präfix: 2001:db8:abcd:0003::/64

Subnetz 65536: 2001:db8:abcd:ffff::/64
Präfix: 2001:db8:abcd:ffff::/64
```

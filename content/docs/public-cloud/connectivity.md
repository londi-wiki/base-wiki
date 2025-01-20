---
weight: 999
title: "Connectivity and Loadbalancing"
description: ""
icon: "article"
date: "2025-01-21T12:00:00+02:00"
lastmod: "2025-01-21T12:00:00+02:00"
draft: false
toc: true
---

# Connectivity and Loadbalancing

## Allgemeine Faktoren

- Bandbreite: Höhere Bandbreite ermöglicht schnellere Datenübertragung, reduziert Engpässe.
- Latenz: Geringe Latenz ist wichtig für Echtzeitanwendungen und interaktive Workloads
- Netzwerkprotokoll: Optimierungen wie TCP/IP-Tuning oder Nutzung von IDP beeinflussen die Performance
- Redundanz und Verfügbarkeit: Sicherstellen, dass Verbindungen ausfallsicher sind.
- Sicherheit: Verschlüsselung, VPN oder dedizierte Verbindungen wie AWS Direct Connect beeinflussen die Wahl
- Kosten: Skalierbarkeit und Preismodelle (Pay-as-you-go oder feste Verträge)

**Einfluss auf die Performance**

- Höhere Bandbreite reduziert Datenübertragungszeiten
- Niedrige Latenz verbessert die Reaktionsfähigkeit von Anwendungen
- Optimierte Protokolle minimieren Overhead

**Beispiel Übertragungsberechnung**

```
Übertragung von einem Petabyte, 1 Gbit/s Übertragungsgeschwindigkeit

1 Gbit/s = 125 MB/s
1 PB = 1'000'000 GB

Übertragungsdauer: 

1'000'000 GB / 125 MB/s 

= (1'000'000 x 1024 MB) / 125 MB/s 

= 81 Tage (ohne Overhead)


Mit Protokolloverhead (ca. 20%) realistischer: ~ 97 Tage.
```

## Latenz und Data Gravity

- Einfluss auf Anwendungsgeschwindigkeit: Höhere Latenzen führen zu langsameren Datenzugriffen.
- Replikation: Latenzen können bei verteilten Datenbanken Synchronisationsprobleme verursachen.
- Echtzeitanwendungen: Anwendungen wie Videostreaming oder IoT benötigen geringe Latenz.
- Datenverarbeitungen: Bei datenintensiven Workloads (z.B. Machine Learning) wirken sich Latenzen auf die Verarbeitungsgeschwindigkeit aus.

## AWS Direct Connect vs. Azure ExpressRoute

**Einsatz**

- Dedizierte Verbindung zu AWS/Azure, bypassing des öffentlichen Internets.

**Vorteile**

- Geringe Latenz: Direkte Verbindung minimiert Routing-Zeit
- Höhere Sicherheit: Datenübertragung erfolg nicht über das öffentliche Internet.
- Zuverlässigkeit: Bessere Performance und Verfügbarkeit.

# Mikrosegmentierte Netzwerke

**Vorteile**

- Fein granularer Zugriff: Kontrolle auf Anwendungsebene statt nur auf Netzwerkebene.
- Erhöhte Sicherheit: Isolation von Workloads reduziert das Risiko von Angriffen.
- Compliance: Granulare Regeln helfen bei der Einhaltung von Vorschriften.
- Dynamische Anpassung: Änderungen im Netzwerk erfordern keine physische Anpassungen.

**Herausforderungen bei on-prem Datenzentren**

- Alte Netzwerkinfrastrukturen: Legacy-Hardware unterstützt oft keine Mikrosegmentierung.
- Komplexität: Erfordert umfangreiche Planung und Verwaltung.
- Kosten: Hohe Investitionen in Software und Hardware
- Weniger Flexibilität: Änderungen an physischen Netzwerken sind aufwendiger.

# VPC / Virtual Networks

**Vorteile**

- Isolation: Eigene private Netzwerkumgebungen für Cloud-Ressourcen.
- Sicherheit: Kontrollierter Zugriff durch Security Groups und NACLs
- Skalierbarkeit: Einfaches Hinzufügen von Subnetzen und Ressourcen.
- Integration: Verbindung mit On-Premise-Netzwerken möglich.
- Kosteneffizienz: Pay-as-you-go für Netzwerknutzungen.

# Datacenter Zone mit AWS Public Cloud verbinden

- AWS Direct Connect: Dedizierte Verbindung für sicherer und schnelle Anbindung.
- Site-to-Site VPN: Verschlüsseltes VPN über das Internet.
- Transit Gateway: Verbindung mehrerer VPCs und On-Premise-Netzwerke.
- VPC Peering: Direkte Verbindung zwischen VPCs

# NACLs und Security Groups

**Unterschiede**

NACLs (Network Access Control Lists):

- Ebenen: Subnetz-Ebene.
- Richtung: Regeln für ein- und ausgehenden Traffic
- Regeln: Stateless, müssen für Rückverkehr explizit angegeben werden.
- Einsatz: Basis-Sicherheit auf Subnetz-Ebene.

Security Groups:

- Ebenen: Instanz-Ebene
- Richtung: Regeln für ein- ausgehenden Traffic
- Regeln: Stateful, Rückverkehr wird automatisch erlaubt
- Einsatz: Feingranulare Kontrolle für spezifische Ressourcen.


# Subnetz-Konzept mit DMS, Secure und High Secure Zone in AWS-Cloud

1. VPC erstellen: VPC mit CIDR-Block definieren
2. Subnetz erstellen
   1. DMZ (öffentlich): Öffentlich zugängliche Ressourcen (z.B. Webserver)
   2. Secure (privat): Hochsensible Daten und Anwendungen.
   3. High Secure (privat): Hochsensible Daten und Anwendungen
3. Routing-Tabellen einrichten
   1. DMZ-Subnetz: Internet-Gateway für öffentlichen Zugriff
   2. Private Subnetze: Keine Internetzugriff, nur über VPN/Direct Connect erreichbar
4. Security-Gruppen und NACLs: Zugriff pro Subnetz und Instanz regeln

# Loadbalancer

**Heuristiken**

- Round Robin: Gleichmässige Verteilung der Anfragen
- Least Connections: An Server mit den wenigsten aktiven Verbindungen
- Weighted Round Robin: Bevorzugung leistungsfähiger Server
- IP Hashing: Client-IP entscheidet über den Zielserver

**Vorteile Layer-4-LoadBalancer**

- Schnelligkeit: Operiert auf Netzwerkebene, weniger Overhead
- Protokollunabhängigkeit: Funktioniert mit TCP/UDP
- Effizient: Weniger Ressourcenverbrauch

**Vorteile Layer-7-LoadBalancer**

- Anwendungsintelligenz: Inhalte der Anfragen (z. B. HTTP-Header) werden berücksichtigt.
- SSL Offloading: Verarbeitung von SSL/TLS-Verbindungen
- Routing: Basierend auf Pfaden oder HTTP-Headern.



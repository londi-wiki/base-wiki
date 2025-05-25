---
weight: 999
title: "Hyperscaling"
description: ""
icon: "article"
date: "2025-01-20T12:10:00+02:00"
lastmod: "2025-01-20T12:10:00+02:00"
draft: false
toc: true
---

# Hyperscaling

## Arten von Skalierung

**Vertikale Skalierung (Scale-Up)**

- Erhöhen der Ressourcen eines einzelnen Systems (mehr CPU, RAM, Speicherplatz)
- Einfach umzusetzen, aber limitiert durch Hardwaregrenzen
- Beispiel_ Upgrade eines Servers von 16 GB auf 64 GB RAM

**Horizontale Skalierung (Scale-Out)**

- Hinzufügen von mehr Systemen (Servern oder Instanzen) zu einem Cluster
- Erfordert verteilte Systeme, Load-Balancing und Synchronisierung
- Beispiel: Hinzufügen von weiteren Webservern hinter eine Load Balancer

**Unterschiede**

- Vertikale Skalierung ist einfacher, aber weniger flexibel
- Horizontale Skalierung bietet bessere Elastizität und Fault Tolerance, benötigt aber komplexere Architektur

## Burst-Instanzen

**Besonderheiten**

- Burst-Instanzen (z.B. AWS T2/T3) können CPU-Ressourcen für kurze Zeit über ihren Grundwert hinaus nutzen, indem sie CPU-Credits aufbauen.
- Kostengünstig für Workloads mit sporadischer Last (z.B. Entwicklungs- oder Testsysteme)

**Schlimmster Workload**

- Langfristig hoher CPU-Verbrauch, der die Credits schnell aufbraucht. Danach wird die Performance auf das Baseline-Level gedrosselt.


# Horizontaler Skalierung

## Herausforderungen

- Datenkonsistenz: Synchronisierung zwischen mehreren Knoten
- Load Balancing: Effiziente Verteilung des Traffics
- Stateful Anwendungen: Erfordern zusätzliche Lösungen wie Datenbankreplikation oder externe Caches
- Kosten: Mehr Systeme bedeuten höhere Betriebskosten
- Netzwerklatenz: Kommunikation zwischen Knoten kann Engpässe verursachen

**Wann funktioniert Horizontaler Skalierung schlecht?**

- Stateful Workloads mit vielen Abhängigkeiten (z.B. monolithische Anwendungen)
- Anwendungen, die nicht parallelisiert werden können (z.B. viele sequentielle Berechnungen)

# Elastizität

**Herausforderungen bei Elastizität**

- Latenz bei Skalierung: Instanzen benötigten Zeit, um hochzufahren und in den Pool integriert zu werden
- Vorhersagbarkeit: Schwankungen im Traffic sind schwer vorhersehbar
- Stateful Workloads: Daten müssen zwischen Instanzen synchronisiert werden, was Verzögerungen verursacht.
- Kostenoptimierung: Balancieren zwischen Overprovisioning und Unterkapazität

# Kubernetes-Instanzen auf Hyperscalern

**Besonderheiten**

- Managed Services: Hyperscaler wie AWS (EKS), Azure (AKS) und Google Cloud (GKE) bieten verwaltete Kubernetes-Cluster
- Automatisierung: Skalierung, Upgrades und Wartung werden teilweise automatisch gehandhabt.
- Integration: Nahtlose Nutzung von Cloud-spezifischen Diensten (z.B. Load Balancers, Monitoring, Speicher)

**Möglichkeiten der Kubernetes-Installationen auf Hyperscalern**

- Elastizität: Automatische Skalierung von Pods basierend auf Workloads
- Multi-Region Deployment: Verteilung von Workloads über mehrere Regionen
- Integration: Nutzung von Cloud-Diensten wie Datenbanken, Storage und Monitoring-Tools
- Portabilität: Anwendungen können zwischen verschiedenen Hyperscalern oder On-Prem Systemen migriert werden.

# Use case: Split eines Monolithen in eine Microservicearchitektur

1. Identifikation von Domänen
   1. Zerlegen des Monolithen in logische Geschäftsfunktionen (z.B. Authentifizierung, Payment, User Management)
2. Definieren von APIs
    1. Entwickeln von Schnittstellen für die Kommunikation zwischen den Microservices.
3. Datenbank aufteilen
   1. Jeder Microservice sollte eine eigene Datenbank oder Datendomäne haben, um Endkopplung zu gewährleisten.
4. Deployment & Orchestrierung
   1. Einsatz von Containern (z.B. Docker) und Kubernetes zur Verwaltung
5. Observability einbauen
   1. Logging, Monitoring und Tracing für alle Services

## Serverless Infrastrukturen

**Komplett serverless Infrastrukturen**

- Dienste wie AWS Lambda, Azure Functions oder Google Cloud Functions bieten echte Serverless-Architekturen.
- Entwickler kümmern sich nur um den Code, während die Infrastruktur vollständig vom Anbieter verwaltet wird.

**Was muss man bei Kubernetes betreiben?**

- Bei managed Kubernetes (z. B. EKS/AKS):
  - Cluster Nodes: Worker Nodes müssen bereitgestellt und skaliert werden.
  - Networking: Load Balancer, Ingress-Controller konfigurieren.
  - Speicher: Persistent Volumes verwalten.
  - Observability: Monitoring und Logging implementieren.


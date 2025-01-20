---
weight: 999
title: "Kubernetes"
description: ""
icon: "article"
date: "2025-01-21T00:01:00+02:00"
lastmod: "2025-01-21T00:01:00+02:00"
draft: false
toc: true
---

# Kubernetes

## Allgemein

Kubernetes (oft als "K8s" abgekürzt) ist eine Open-Source-Plattform zur Automatisierung der 
Bereitstellung, Skalierung und Verwaltung von containerisierten Anwendungen. 
Es hilft dabei, Anwendungen über Cluster von Maschinen hinweg zu orchestrieren und bietet Funktionen wie:

- Automatisches Deployment von Containern.
- Skalierung (horizontal und vertikal) basierend auf der Nachfrage.
- Selbstheilung, indem ausgefallene Container automatisch neu gestartet werden.
- Lastverteilung zwischen Containern.

# Komponenten

## Cluster

Ein Kubernetes-Cluster besteht aus mehreren Machinen (Nodes), die zusammenarbeiten, um containerisierte Anwendungen auszuführen.

- Control Plane: Verwalten die Gesamtarchitektur und kontrollieren, wie Anwendungen auf Worker Nodes ausgeführt werden.
- Worker Nodes: Führen die Anwendungen (Container) aus.

## Control Plane

Die Control Plane verwaltet den Zustand des Clusters. Zu ihren Hauptkomponenten gehören:

**API Server**

- Schnittstellen, über die Benutzer, Tools und andere Komponenten mit Kubernetes kommunizieren
- Nimmt Befehle entgegen und leitet sie an andere Komponenten weiter.

**etcd**

- Eine verteilte, hochverfügbare Key-Value-Datenbank
- Speichert den gesamten Zustand des Clusters (z.B. welche Pods wo laufen).

**Scheduler**

- Weist neue Workloads (Pods) den passenden Nodes zu, basierend auf Ressourcenverfügbarkeit, Policy und Anforderungen.

**Controller Manager**

- Enthält verschiedene Controller, die den Zustand des CLusters überwachen und sicherstellen, dass die gewünschte Konfiguration eingehalten wird (z.B. DeploymentController, NodeController).

**Cloud Controller Manager**

- Interagiert mit der Cloud-Plattform (z.B. AWS, Azure, GCP), um ressourcenspezifische Funktionen wie Load Balancer oder Storage zu verwalten.

## Worker Nodes

Worker Nodes führen die containerisierten Anwendungen aus. Sie enthalten folgende Komponenten:

**Kubelet**

- Agent, der auf jedem Worker Node läuft.
- Überwacht den Zustand der Pods und stellt sicher, dass die spezifizierten Container laufen.

**Kube Proxy**

- Netzwerk-Proxy, der Netzwerkregeln umsetzt und dafür sorgt, dass Pods miteinander und mit externen Diensten kommunizieren können.

**Container Runtime**

- Software, die die Container tatsächlich ausführt. Beispiele sind Docker, containerd oder CRI-O

## Container

Container sind standardisierte Einheiten, die Code, Abhängigkeiten und Runtime-Umgebungen enthalten. Sie sind leichtgewichtig und portabel, was Kubernetes so effektiv macht.

# Kubernetes in der Cloud einrichten

## Konzeptuelle Schritte

1. Wähle einen Managed Kubernetes-Dienst:
   1. Azure Kubernetes Service (AKS): Kubernetes wird von Azure verwaltet.
   2. Amazon Elastic Kubernetes Service (EKS): Kubernetes wird von AWS verwaltet.
2. Plane die Architektur:
   1. Clustergröße: Wie viele Nodes brauchst du?
   2. Region: In welcher geografischen Region soll der Cluster laufen?
   3. Netzwerk: Plane ein virtuelles Netzwerk und Subnetze.
3. Automatisiere Deployments:
   1. Verwende Infrastructure-as-Code-Tools wie Terraform, um die Einrichtung zu automatisieren.
4. Skalierbarkeit und Monitoring:
   1. Nutze Tools wie Prometheus oder Grafana, um den Cluster zu überwachen.
   2. Verwende Auto-Scaling-Mechanismen.

## Einrichtung in Azure (AKS)

- Azure übernimmt die Verwaltung der Control Plane.
- Schritte:
  - Erstelle ein AKS-Cluster via Azure-Portal oder CLI.
  - Konfiguriere Ressourcen wie Load Balancer und Storage.
  - Nutze das kubectl CLI-Tool, um Anwendungen zu deployen und zu verwalten. 

## Einrichtung in AWS (EKS)
   
- AWS übernimmt ebenfalls die Verwaltung der Control Plane.
- Schritte:
  - Erstelle ein EKS-Cluster via AWS Management Console oder CLI.
  - Setze ein Node-Group für Worker Nodes auf (EC2-Instances oder Fargate).
  - Richte IAM-Rollen für Kubernetes und Anwendungen ein.


---
weight: 999
title: "Nist Cloud Computing Definition"
description: ""
icon: "article"
date: "2025-01-26T13:38:27+01:00"
lastmod: "2025-01-26T13:38:27+01:00"
draft: false
toc: true
---

# Nist Cloud Computing Definition

NIST = National Institute of Standards and Technology (NIST)

# Fünf Merkmale

## On-Demand Self-Service

Benutzer können **Ressourcen** wie Rechenleistung, Speicher oder Netzwerke ohne menschliches 
Zutun direkt **über ein Portal oder eine API bereitstellen**.

Hyperscaler-Beispiel: Bei AWS können Sie über die Management-Konsole EC2-Instanzen starten, 
ohne dass ein Mitarbeiter involviert ist.

## Broad Network Access

**Zugriff** auf die Cloud-Ressourcen ist **über Standardnetzwerke** (z. B. das **Internet**) und 
eine Vielzahl von Geräten (z. B. Smartphones, Laptops) möglich.

Hyperscaler-Beispiel: Google Cloud ermöglicht es, Anwendungen über das Internet auszuführen und 
zu verwalten, unabhängig davon, ob Sie auf einem Laptop oder einer API arbeiten.

## Resource Pooling

**Ressourcen werden in einem Pool gebündelt und dynamisch auf mehrere Kunden (Mandanten) verteilt**. 
Kunden wissen nicht, wo genau die Ressourcen physisch gehostet werden.

**Hyperscaler-Beispiel: Microsoft Azure verwendet Multi-Tenant-Architekturen, bei denen 
die Ressourcen effizient verteilt werden, während sie für jeden Kunden logisch isoliert bleiben.**

## Rapid Elasticity

**Ressourcen können schnell und elastisch bereitgestellt werden**, um den Anforderungen 
des Kunden zu entsprechen – oft automatisch.

Hyperscaler-Beispiel: Amazon Auto Scaling skaliert automatisch EC2-Instanzen basierend 
auf dem aktuellen Bedarf.

## Measured Service

Cloud-Systeme messen und optimieren Ressourcennutzung automatisch (**Pay-as-you-go**).

Hyperscaler-Beispiel: Bei Google Cloud zahlen Sie nur für die tatsächliche Nutzung, 
wie z. B. für die Millisekunden, in denen Ihre Funktionen in Google Cloud Functions ausgeführt werden.

# Drei Service-Modelle

## Infrastructure as a Service (IaaS)

Grundlegende IT-Ressourcen wie Rechenleistung, Speicher und Netzwerke.

Beispiel: AWS EC2 (Elastic Compute Cloud)

## Platform as a Service (PaaS)

Plattformen für die Entwicklung und Bereitstellung von Anwendungen ohne direkten Zugriff auf die zugrunde liegende Infrastruktur.

Beispiel: Google App Engine.

## Software as a Service (SaaS)

Bereitstellung von Anwendungen, die direkt über das Internet genutzt werden können.

Beispiel: Microsoft 365 oder Google Workspace.

# Vier Bereitstellungsmodelle

## Public Cloud

Die Cloud-Infrastruktur wird von einem Drittanbieter betrieben und ist **öffentlich verfügbar**.

Beispiel: Google Cloud oder AWS.

## Private Cloud

Cloud-Dienste werden ausschliesslich von einer Organisation genutzt und entweder intern oder extern betrieben.

Beispiel: Eine von Azure betriebene On-Premises-Lösung oder lokaler Anbieter.

## Hybrid Cloud

Kombination aus Public und Private Cloud.

Beispiel: AWS Outposts, das Public-Cloud-Funktionen in eine private Infrastruktur integriert.

## Community Cloud

**Mehrere Organisationen teilen sich eine spezifische Cloud-Infrastruktur mit ähnlichen Anforderungen.**

Beispiel. Gemeinsame Cloud-Plattformen für Forschungsorganisationen.

# NIST bei Hyperscalern

Hyperscaler wie AWS, Azure, Google Cloud entsprechen der NIST-Definition, da sie:

- Skalierbarkeit: Massive Ressourcenpools bieten, die global verfügbar sind.
- Automatisierung: Nahtlose Bereitstellung und Skalierung über Self-Service-Portale ermöglichen.
- Flexibilität: Alle drei Service-Modelle (**IaaS, PaaS, SaaS**) und verschiedene Bereitstellungsmodelle unterstützen.

# Übersicht der NIST-Merkmalen in Bezug auf Public, Private, Hybrid und Community Cloud

| **NIST-Merkmale**           | **Public Cloud**                                                                      | **Private Cloud**                                                                        | **Hybrid Cloud**                                                                                         | **Community Cloud**                                                                                    |
|-----------------------------|---------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **On-Demand Self-Service**  | Benutzer können Ressourcen direkt über das Internet bereitstellen (z. B. AWS, Azure). | Organisationen können intern Self-Service-Portale nutzen, oft mit mehr Kontrolle.        | Kombination aus Public- und Private-Cloud-Portalen für flexible Bereitstellung.                          | Gemeinschaftlicher Zugriff durch berechtigte Organisationen, oft mit Self-Service-Funktionen.          |
| **Broad Network Access**    | Zugriff über öffentliche Netzwerke wie das Internet, kompatibel mit vielen Geräten.   | Zugriff oft nur innerhalb der Organisation oder über ein **VPN** für externe Geräte.     | Public-Cloud-Ressourcen über Internet und Private-Cloud-Ressourcen über dedizierte Netzwerke erreichbar. | Zugriff für autorisierte Gemeinschaftsmitglieder, oft über ein gemeinsames Netzwerk oder Internet.     |
| **Resource Pooling**        | Ressourcen werden zwischen mehreren Kunden geteilt (Multi-Tenancy).                   | Ressourcen sind exklusiv für eine Organisation reserviert.                               | Ressourcen können zwischen Public- und Private-Clouds aufgeteilt werden.                                 | Ressourcen werden von mehreren Organisationen mit gemeinsamen Interessen geteilt.                      |
| **Rapid Elasticity**        | Unbegrenzte Skalierbarkeit, um dynamisch auf Nachfrage zu reagieren.                  | Skalierung ist begrenzt durch die verfügbare interne Infrastruktur.                      | Skalierbarkeit hängt von Public-Cloud-Integration und internen Ressourcen ab.                            | Gemeinschaftliche Infrastruktur kann skaliert werden, ist jedoch oft begrenzter als Public Clouds.     |
| **Measured Service**        | **Pay-as-you-go-Modell** mit transparenter Ressourcennutzung und Abrechnung.          | Abrechnung erfolgt intern, keine direkte Kostenaufschlüsselung wie in der Public Cloud.  | Kombination aus Public-Cloud-Nutzung (Pay-as-you-go) und internen Abrechnungsmodellen.                   | Ressourcen werden je nach Nutzung der teilnehmenden Organisationen gemessen und verteilt.              |







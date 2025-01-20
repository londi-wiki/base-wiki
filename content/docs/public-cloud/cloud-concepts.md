---
weight: 999
title: "Cloud Concepts"
description: ""
icon: "article"
date: "2025-01-19T12:00:00+02:00"
lastmod: "2025-01-19T12:00:00+02:00"
draft: false
toc: true
---

# Cloud Concepts

| Aspekt        | IaaS (Infrastructure as a Service)                                                                                                         | PaaS (Platform as a Service                                                                                                              | SaaS (Software as a Service)                                                                                                                     |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Definition    | Bietet grundlegende Infrastruktur wie virtuelle Maschinen, Speicher und Netzwerke, die Benutzer selbst konfigurieren und verwalten können. | Bietet eine Plattform mit Entwicklungs- und Bereitstellungstools für Anwendungen, ohne dass Benutzer die Infrastruktur verwalten müssen. | Bietet vollständig entwickelte Anwendungen, die über das Internet genutzt werden können, ohne sich um Wartung oder Verwaltung kümmern zu müssen. |              
| Einsatzgebiet | Flexible Skalierung und Kontrolle der IT-Infrastruktur, besonders geeignet für Unternehmen mit eigener IT-Kompetenz.                       | Entwickeln, Testen und Bereitstellen von Anendungen, ohne sich um die zugrunde liegende Infrastruktur zu kümmern.                        | Bereitstellung von Endbenutzeranwendungen für eine breite Palette von Geschäftsanforderungen.                                                    |              
| Verwaltung    | Benutzer verwalten Infrastruktur wie Betriebssysteme, Datenbanken und Anwendungen.                                                         | Benutzer verwalten Anwendungen, während der Anbieter die Plattform und Infrastruktur verwaltet.                                          | Der Anbieter verwaltet alles, einschliesslich Infrastruktur, Plattoform und Anwendungen.                                                         |        
| Kostenmodell  | Pay-as-you-go für genutzte Resourcen (CPU, RAM, ...)                                                                                       | Pay-as-you-go oder nutzungsbasierte Abrechnung für die Plattform.                                                                        | Abonnements oder nutzungsbasierte Abrechung für den Softwarezugriff.                                                                             |
| Beispiele     | Azure Virtual Machines / Amazon EC2 / Google Compute Engine                                                                                | Azure App Service / AWS Elastic Beanstalk / Google App Engine                                                                            | Microsoft 365 / Google Workspace / Slack                                                                                                         |

## Shared Responsibility Model

Je nach Dienstleistung (IaaS oder Paas) ist der Kunde von Public Cloud Services für das ganze Betriebssystem 
oder nur für den Betrieb der Software zuständig. Hierbei muss der Kunde ggf. selber Updates oder Patches durchführen. 
Auf jeden Fall ist die Hardware Sicherheit durch den Cloud-Provider sichergestellt.

# Regionen und Verfügbarkeitszonen

**Regionen**

Regionen sind geografisch getrennte Bereiche, die aus mehreren Rechenzentren bestehen. Sie sind so gestaltet, dass die nahe an den Endbenutzern sind, um niedrige Latenz und gesetzliche Compliance zu gewährleisten. Jede Region wird unabhängig betrieben, um Ausfälle in anderen Regionen nicht zu beeinflussen.

**Verfügbarkeitszonen (Availability Zones)**

Regionen bestehen aus mehreren Verfügbarkeitszonen (AZs). Eine Verfügbarkeitszone ist ein physisch separater Rechenzentrumsstandort innerhalb einer Region. Sie verfügt über eine eigene Stromversorgung, Netzwerk und Kühlung, um eine hohe Verfügbarkeit zu gewährleisten. Dienste können in mehreren Zonen bereitgestellt werden, um Redundanzen und Ausfallsicherheit zu erreichen.

**Netzwerk- und Datenreplikation**

Cloud Anbieter ermöglichen die Datenreplikation zwischen Zonen, um eine höhere Verfügbarkeit und Disaster Recovery sicherzustellen. Sie bieten Mechanismen für den globalen Datenzugriff über Regionsgrenzen hinweg.

# CISPE Code of Conduct

-	Datenschutzkonformität: 
Cloud Provider und deren Infrastruktur müssen den Vorgaben der DSGVO entsprechen.
-	Verarbeitung personenbezogener Daten: 
Cloudbetreiber sind lediglich Auftragverarbeiter was bedeutet, dass sie nur nach Auftrag vom Kunden verarbeitet werden dürfen.
-	Datenlokalisierung und Datenresidenz: 
Die Möglichkeit, Daten ausschliesslich in der EU zu speichern muss gewährleistet werden.
-	Sicherheitsvorkehrungen: 
Physische, technische und organisatorische Massnahmen müssen für die Sicherheit der Daten gewährleistet werden.
-	Transparent: 
Cloud Provider müssen transparent und offen erklären, wie sie die Daten schützen.
Sicherheitsvorkehrungen, Datenstandort, Verantwortlichkeiten im Rahmen der Datenverarbeitung
-	Auditierbarkeit und Zertifizierungen: 
Es muss regelmässig durch unabhängige Audits die Einhaltung der CISPE Code of Conduct geprüft werden.
-	Rechte der betroffenen Person: 
Cloud Provider müssen sicherstellen, dass die Rechte der betroffenen Person nach DSGVO umgesetzt werden können. Dazu gehören: Auskunft, Löschung oder Berichtigung von Daten.

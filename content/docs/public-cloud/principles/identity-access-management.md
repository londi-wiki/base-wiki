---
weight: 999
title: "Identity Access Management"
description: ""
icon: "article"
date: "2025-01-20T12:45:00+02:00"
lastmod: "2025-01-20T12:45:00+02:00"
draft: false
toc: true
---

# Identity Access Management

## Allgemein

**Aufgaben**

- Identitätsmanagement: Erstellen und Verwalten von Benutzern, Gruppen und Rollen
- Authentifizierung: Sicherstellen, dass nur autorisierte Benutzer und Anwendungen auf Ressourcen zugreifen können
- Autorisierung: Zuweisung von Berechtigungen basierend auf Policies
- Granulare Zugriffskontrolle: Detaillierte Kontrolle über den Zugriff auf spezifische AWS-Ressourcen
- Multi-Factor Authentication (MFA): Zusätzliche Sicherheitsebene durch MFA
- Audit- und Compliance-Unterstützung: Überwachung von IAM-Aktivitäten durch AWS CloudTrail

## IAM Service AWS und Azure

| Aspekt              | AWS IAM                                            | Azure IAM                                      |
|---------------------|----------------------------------------------------|------------------------------------------------|
| Ressourcenkontrolle | Identity-based und Resource-based Policies         | Rollenzuweisungen und rollenbasierte Kontrolle |
| Rollenmodell        | Rollen und Policies für Services und Nutzer        | Zuweisung von Rollen an Benutzer/Objekte       |
| Verwaltungszugriff  | Benutzerzugriff erfolgt durch CLI, API, Konsole    | Zugriff über Azure Portal oder CLI             |
| Integration         | Unterstützung SAML 2.0, Federation, AD-Integration | Starke Integration mit Azure AD                |

## ABAC Konzept

**ABAC (Attribute-Based Access Control)**

- Zugriff wird basierend auf Attributen wie Benutzermerkmalen (z.B. Abteilung) oder Ressourcen-Tags (z.B. "Environment:Production") gesteuert

**Vorteile**

- Granularität: Präzise Zugriffskontrolle basierend auf Attributen
- Skalierbarkeit: Policies sind dynamisch und erfordern keine manuelle Anpassung für jeden Benutzer.
- Flexibilität: Ermöglicht Regeln wie "Entwickler können auf Ressourcen ihrer eigenen Abteilung zugreifen"

## Unterschied ABAC und RBAC

**RBAC (Role-Based Access Control)**

- Berechtigungen basieren auf **Rollen**, die Benutzern zugewiesen werden
- Beispiel: Rolle "Admin" hat volle Zugriffsrechte

**ABAC (Attribute-Based Access Control)**

- Berechtigungen basieren auf Attributen, z.B. Tags oder Metadaten
- Beispiel: Zugriff erlaubt, wenn `Abteilung = "Marketing"`

**Unterschiede**

- RBAC ist statisch und erfordert explizite Rollenzuweisung
- ABAC ist dynamischer und erlaubt komplexe Bedingungen

# Aufbau eines IAM-Systems

- Benutzer: Einzelne Identitäten (z.B. Mitarbeiter)
- Gruppen: Sammlung von Benutzern mit gemeinsamen Berechtigungen
- Rollen: Temporäre Berechtigungen für Benutzer oder Services
- Policies: Regeln, die den Zugriff definieren
- Authentifizierungsmechanismen: Passwörter, MFA, API-Schlüssel
- Protokollierung: Nachverfolgen von Aktionen (z.B. AWS CloudTrail)

## Rolle vs Gruppe

**Gruppe**

- Sammlung von Benutzern mit gemeinsamen Berechtigungen
- Berechtigungen werden über Policies auf die Gruppe angewendet

**Rolle**

- Temporäre Identität, die bestimmten Zugriff gewährt
- Wird oft von Services oder externen Nutzern verwendet

**Unterschied**

- Gruppen sind für Benutzerverwaltungen, Rollen für Servicezugriffe und temporäre Autorisierungen


# Einrichten eines AWS-Accounts

- Root-Account sichern: MFA aktivieren, minimale Nutzung.
- IAM-Nutzer verwenden: Keine direkten Logins mit Root, sondern über dedizierte IAM-Benutzer.
- Least Privilege Principle: Nur die notwendigsten Berechtigungen vergeben.
- MFA aktivieren: Für alle Benutzer und Rollen.
- Passwortrichtlinien: Sicherstellen, dass starke Passwörter verwendet werden.
- Logging: Aktivieren von AWS CloudTrail für Audit-Zwecke.
- Netzwerk-Sicherheit: Nutzung von Security Groups und NACLs.
- Ressourcen-Tags verwenden: Zur besseren Verwaltung und Überwachung.

## Verbindung eines eigenen AD mit der AWS-Cloud

**AWS Directory Service**

- AD Connector: Verbindung des lokalen AD mit AWS.
- AWS Managed AD: Vollständig verwalteter AD-Service in der Cloud.

**Federation Services**

- SAML 2.0 zur Integration mit dem lokalen AD.

**Allgemein**

- VPN oder Direct Connect: Verbindung des lokalen Netzwerks mit AWS-Ressourcen.
- Single Sign-On (SSO): Integration von AD mit AWS SSO.

## Beispiel: Federated Authentication

Definition

- Benutzer einer externen Identität (z.B. Google, AD) greifen über eine föderierte Authentifizierung auf AWS zu

Beispiel

- Ein Unternehmen nutzt Azure AD für Identitätsmanagement
- Mitarbeiter melden sich über Azure AD an und erhalten über SAML-Integration temporären Zugriff auf AWS

# Blast Radius

**Definition**

Der potenzielle Schadensbereich, den ein Fehler oder eine Sicherheitslücke verursachen kann.

**Rolle bei IaC**

- Modularität: Infrastruktur wird in kleinere Einheiten zerlegt, um den Blast Radius zu begrenzen.
- Testing: Änderungen an IaC können vorher getestet werden, um Fehler zu minimieren.
- Least Privilege: Rollen und Zugriffsrechte sind strikt auf spezifische Ressourcen begrenzt.
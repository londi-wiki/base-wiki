---
weight: 999
title: "Moolith Microservice"
description: ""
icon: "article"
date: "2024-11-04T09:23:41+01:00"
lastmod: "2024-11-04T09:23:41+01:00"
draft: false
toc: true
---

# Vergleich

| Aspekte/Typ   | Monolith                                            | Modulith                                  | Microservice                                                                                    |
|---------------|-----------------------------------------------------|-------------------------------------------|-------------------------------------------------------------------------------------------------|
| Vorteile      | - Einfaches Deployment<br/>- technische Grenzen     | - fachliche Grenzen<br/>- Erweiterbarkeit | - Unabhängigkeit zwischen Services<br/>- Einarbeitung neuer Team-Mitglieder einfacher           |
| Nachteile     | - Erweiterbarkeit schwieriger<br/>- starke Kopplung | - Skalierbarkeit (Betrieb)                | - Infrastruktur notwendig (Broker, (Messaging))<br/>- DTOs müssen für jede Impl. vorhanden sein |

## Modulith bei Spring Boot

- [Guide to Modulith with Spring Boot](https://piotrminkowski.com/2023/10/13/guide-to-modulith-with-spring-boot/)
- [Spring.io Modulith](https://spring.io/projects/spring-modulith)

## Bemerkung GOlang

GO's Umgang mit Paketen und Abhängigkeiten basiert auf dem Konzept der "Package-Oriented Design" oder auch "Go Package Pattern". 

Dies aufgrund des Problems der zirkulären Abhängigkeiten:
- In Go sind zirkuläre Abhängigkeiten zwischen Paketen nicht erlaubt
- Wenn Paket A Paket B importiert und Paket B wiederum Paket A importiert, führt das zu einem Kompilierungsfehler
- Dies ist eine bewusste Designentscheidung der Go-Entwickler

Der Lösungsansatz:
- Statt technischer Trennung (z.B. alle Services, alle Repositories, alle Controller in separaten Paketen)
- Verwenden von fachlicher/domänenorientierter Trennung
- Jedes Paket repräsentiert einen abgeschlossenen fachlichen Bereich

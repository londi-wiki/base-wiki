---
weight: 999
title: "Database"
description: ""
icon: "article"
date: "2025-01-20T03:20:00+02:00"
lastmod: "2025-01-20T03:20:00+02:00"
draft: false
toc: true
---

# Datenbanken

## Vorteile in der Cloud

- Automatisierung: Provisionierung, Backup, Patch-Management und Skalierung werden automatisch verwaltet.
- Skalierbarkeit: Vertikale und horizontale Skalierung bei Bedarf.
- Verfügbarkeit: Hohe Verfügbarkeit durch Multi-AZ-Replikation und automatische Failover-Mechanismen.
- Kostenoptimierung: Pay-as-you-go-Modelle, keine Investitionen in Hardware.
- Sicherheit: Verschlüsselung von Daten, rollenbasierte Zugriffskontrolle und Compliance-Zertifizierungen.
- Integration: Nahtlose Integration mit anderen Cloud-Diensten wie Speicher, Analytics und Monitoring.


## Datenbank Typen

**Relationale Datenbanken (SQL)**

- AWS RDS (MySQL; PostgreSQL, ...)
- Google Cloud SQL
- Azure SQL Database

**NoSQL-Datenbanken**

- Key-Value Stores: DynamoDB (AWS), Azure Table Storage
- Document Stores: MongoDB Atlas, Couchbase, AWS DocumentDB
- Columnar Databases: Apache Cassandra (AWS Keyspaces), HBase
- Graph Databases: AWS Neptune, **Azure Cosmos DB** (Graph API), Neo4j

**Data Warehouses**

- Beispiele: AWS Redshift, Google BigQuery, Snowflake

**Time-Series Datenbanken**

- Beispiele: InfluxDB, Amazon Timestream

**In-Memory Datenbanken**

- Beispiele: Redis, Memcached

**Search-Datenbanken**

- Beispiele: Elasticsearch, OpenSearch

# Data Gravity

**Definition**

Data Gravity beschreibt das Phänomen, dass große Datenmengen Anwendungen, 
Services und Workflows „anziehen“, weil es ineffizient ist, große Datenmengen zu bewegen.

**Aspekte**

- Kosten: Datenverschiebungen zwischen Regionen oder Clouds sind teuer.
- Performance: Anwendungen profitieren von geringer Latenz, wenn sie in der Nähe der Daten ausgeführt werden.
- Compliance: Daten müssen oft in bestimmten Regionen bleiben (z. B. DSGVO).
- Integration: Datenintensive Workloads wie Analytics und Machine Learning erfordern lokal verfügbare Daten.

# CAP Theorem

- (C) Consistency
- (A) Availability
- (P) Partition Tolerance

Partition Tolerance kann in der Cloud nicht ignoriert werden:

- Verteilte Systeme: Cloud-Architekturen sind intrinsisch verteilt, oft über mehrere Regionen.
- Netzwerkpartitionen: Netzwerkfehler sind unvermeidlich, daher ist Partitionstoleranz ein Muss.
- Verfügbarkeit: Um Dienste in der Cloud bereitzustellen, muss Partitionstoleranz implementiert werden, um den Zugriff auf Daten während Partitionen zu gewährleisten.

## AC (Availability + Consistency)

Verzicht auf Partitionstoleranz, daher weniger geeignet für verteilte Systeme. 
Beispiel: Relationale Datenbanken mit Single-Node (MySQL ohne Replikation).

## AP (Availability + Partition Tolerance)

Verzichten auf Konsistenz unter Netzwerkteilung.
Beispiele: DynamoDB, Cassandra, Couchbase


## CP (Consistency + Partition Tolerance)

Verzicht auf Verfügbarkeit während Netzwerkteilungen.
Beispiele: MongoDB, HBase, ZooKeeper

# ACID in CAP Theorem

ACID = Atomic, Consistent, Isolated, Durable

- Konsistenz: ACID-Datenbanken garantieren starke Konsistenz (C), was in verteilten Systemen eine Herausforderung darstellt.
- Partitionstoleranz: In einer Cloud-Umgebung kann Partitionstoleranz (P) nicht ignoriert werden.
- Verfügbarkeit: ACID-Datenbanken priorisieren Konsistenz und verzichten oft auf Verfügbarkeit (z. B. durch Locking-Mechanismen).


# Use Cases

## NoSQL DB für JSON Dateien

**Geeignete NoSQL Datenbanken**

- MongoDB: JSON-ähnliches BSON-Format, Abfragen mit JSON-Syntax, Schema-Flexibilität.
- Couchbase: JSON-native Speicherung, Full-Text-Suche, Echtzeit-Analysen.
- Amazon DocumentDB: Vollständig verwaltet, kompatibel mit MongoDB.
- DynamoDB: Unterstützt JSON-Datenformate, integrierte Skalierung.

**Features**

- Flexible Schemata
- Indexierung und Abfragen basierend auf JSON-Feldern
- Integrierte Skalierbarkeit
- Unterstützung für verteilte Architekturen

## Dokumente in DocumentDB

**Vorteile gegenüber DynamoDB**

- Kompatibilität: **DocumentDB ist mit MongoDB kompatibel** und ermöglicht die Nutzung von MongoDB-Tools und -Bibliotheken.
- Komplexe Abfragen: DocumentDB unterstützt umfangreiche Abfragen, Joins und Aggregationen, die in DynamoDB schwer umzusetzen sind.
- Transaktionen: DocumentDB bietet Multi-Dokument-Transaktionen; DynamoDB ist eingeschränkt in der Transaktionsunterstützung.
- Datenmodell: DynamoDB ist Key-Value-basiert und nicht ideal für komplexe dokumentbasierte Strukturen.

## Kombination von Redis, NoSQL-DB und relationales System

**E-Commerce Plattform**

**Redis (In-Memory Cache)**
- Speicherung von Sitzungsdaten und häufig abgefragten Produkten, um die Ladezeiten zu minimieren.
- Beispiel: **Schnellzugriff auf Warenkorbdaten oder Produktkategorien**.

**NoSQL-Datenbank (z. B. MongoDB)**
- Speicherung von Produktkatalogen, Bewertungen und Benutzerdaten als JSON-Dokumente.
- Beispiel: Flexibilität bei der Handhabung von Produktattributen.

**Relationales System (z. B. PostgreSQL)**
- Verwaltung von Transaktionsdaten und Benutzerkonten.
- Beispiel: Speicherung von Bestellungen, Rechnungen und Benutzerprofilen **mit ACID-Eigenschaften**.





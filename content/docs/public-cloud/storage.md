---
weight: 999
title: "Storage"
description: ""
icon: "article"
date: "2024-10-08T14:32:35+02:00"
lastmod: "2024-10-08T14:32:35+02:00"
draft: false
toc: true
---

# Allgemein

Es gibt vier verschiedene Arten Daten zu speichern:

- Block
- File
- Blob / Object
- Datenbank

## Produkte

| Cloud Provider | Block Storage         | File Storage    | Object Storage        |
|----------------|-----------------------|-----------------|-----------------------|
| AWS            | EBS                   | EFS             | S3                    |
| Azure          | Azure Managed Disks   | Azure Files     | Azure Blob Storage    |
| Google Cloud   | Google Persistent Disk | Cloud Filestore | Google Cloud Storage  |

## Wichtige Lernziele
- Die Unterschiede zwischen verschiedenen Cloud-Speichertypen verstehen.
- Cloud-basierten Objektspeicher einrichten, Daten hoch- und herunterladen sowie Konsistenzmodelle für Daten verstehen.

# Speicherklassifizierungen

1. **Objektspeicher**:
    - Ausgelegt für das Verwalten großer Mengen unstrukturierter Daten.
    - Daten werden in Containern (oft „Buckets“ genannt) gespeichert und sind über eindeutige URLs zugänglich.
    - Unterstützt globale Zugänglichkeit über REST-APIs und eignet sich für Anwendungsfälle mit großen Datensätzen.

2. **Blockspeicher**:
    - Bietet festplattenähnlichen Speicher, der hauptsächlich in Cloud-Infrastrukturen verwendet wird.
    - Ideal für Anwendungen, die geringe Latenz erfordern, und kann je nach Bedarf skaliert werden.
    - Wird häufig für die Speicherung von virtuellen Maschinen oder Datenbanken verwendet.

3. **Dateispeicher**:
    - Ähnlich wie traditionelle Netzwerkspeichersysteme, die es mehreren Systemen ermöglichen, auf gemeinsame Dateien zuzugreifen.
    - Geeignet für Szenarien, in denen mehrere virtuelle Maschinen gleichzeitig auf einen gemeinsamen Datensatz zugreifen müssen.

## Speichermerkmale

- **Dauerhaftigkeit**: Extrem hoch, um sicherzustellen, dass Daten vor Verlust geschützt sind.
- **Verfügbarkeit**: Entwickelt, um immer verfügbar zu sein, mit hohen Verfügbarkeitsgarantien.
- **Skalierbarkeit**: Unterstützt praktisch unbegrenzte Kapazitäten sowohl für Objekt- als auch Blockspeichersysteme.
- **Sicherheit**: Bietet detaillierte Zugriffskontrollen, um sicherzustellen, dass Daten nur für autorisierte Benutzer zugänglich sind.

## Datenmanagement und Richtlinien
- Speichersysteme beinhalten häufig Funktionen wie **Versionierung**, um frühere Versionen von Dateien nachzuverfolgen und wiederherzustellen.
- Daten werden mittels **Replikation** gesichert, um Konsistenz und Backup über verschiedene Regionen oder Verfügbarkeitszonen hinweg zu gewährleisten.
- Lifecycle-Richtlinien können eingerichtet werden, um Daten basierend auf ihrem Alter oder ihren Zugriffsmustern zu verschieben oder zu löschen, was Kosten und Effizienz optimiert.

## Backup-Lösungen
- Cloud-Speichersysteme bieten integrierte Backup-Mechanismen, die sowohl manuelle als auch automatische Backups unterstützen.
- Diese Lösungen ermöglichen flexible Wiederherstellungsoptionen im Falle eines Datenverlusts oder Systemausfalls.

## Datenübertragung und Migration
- Es stehen Werkzeuge zur Verfügung, um eine effiziente Datenübertragung, auch bei sehr großen Datenmengen, zu ermöglichen.
- Für große Datensätze können physische Datentransferdienste genutzt werden, um lange Netzwerktransferzeiten zu vermeiden.

## Konsistenzmodelle
- Die meisten Cloud-Speichersysteme bieten **eventuelle Konsistenz**, was bedeutet, dass Datenaktualisierungen Zeit benötigen können, um vollständig über alle Systeme propagiert zu werden.
- Es gibt auch **Read-after-Write-Konsistenz**, die sicherstellt, dass neu geschriebene Daten sofort für nachfolgende Lesevorgänge verfügbar sind.

## Anwendungsfälle
- Häufige Szenarien umfassen die Verwendung von Speicher für Backup und Archivierung, das Hosten von statischen Websites oder das Bereitstellen von dynamischen Medieninhalten.
- Hohe Verfügbarkeit und Skalierbarkeit machen Cloud-Speicher ideal für Anwendungen, die erhebliche Datenverarbeitung und -zugriff erfordern, wie Big-Data-Workloads oder Medien-Streaming.

## Zusammenfassung
- Objektspeicher ist hochflexibel und ideal für die Speicherung unstrukturierter Daten.
- Blocks-Speicher eignet sich für Anwendungen, die schnellen, beständigen Speicher benötigen.
- Dateispeicher ist nützlich, wenn geteilter Zugriff über mehrere Systeme erforderlich ist.
- Alle Cloud-Speicherlösungen bieten hohe Skalierbarkeit, Sicherheit und Datensicherheit, was sie für eine Vielzahl von Anwendungen geeignet macht.

# Produktabhängige Informationen

## AWS S3 Keys

- Schlüssel ist eindeutig
- Kombination aus: Bucket, Schlüssel- und Versions-ID

Beispiel: https://doc.s3.amazonaws.com/2006-03-01/AmazonS3.wsdl, "doc" ist der Name des Buckets und
"2006-03-01/AmazonS3.wsdl" ist der Schlüssel.

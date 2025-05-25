---
weight: 999
title: "MD5"
description: ""
icon: "article"
date: "2025-05-25T10:29:06+02:00"
lastmod: "2025-05-25T10:29:06+02:00"
draft: false
toc: true
---

# Einleitung

> MD5 (Message-Digest Algorithm 5) ist eine kryptographische Hashfunktion, die 1991 von Ronald Rivest entwickelt wurde. Sie erzeugt aus beliebigen Daten einen 128-Bit-Hashwert, der oft als 32-stellige Hexadezimalzahl dargestellt wird. Ziel war es, eine eindeutige „digitale Fingerabdruck“-Funktion zu schaffen, die Datenintegrität sicherstellt.

## Einsatz von MD5 (früher)

- **Dateiintegritätsprüfung**: Um sicherzustellen, dass Dateien während der Übertragung nicht beschädigt wurden. Beispielsweise kann man nach dem Herunterladen einer Datei den MD5-Hash vergleichen, um die Integrität zu überprüfen.

- **Datenbankindizierung**: In einigen Datenbanksystemen wird MD5 verwendet, um eindeutige Schlüssel für Datensätze zu generieren.

- **Nicht-sicherheitskritische Anwendungen**: In Bereichen, in denen Geschwindigkeit wichtiger ist als Sicherheit, wie z. B. bei der Partitionierung von Daten in verteilten Systemen.

Ausprobieren: [CyberChef MD5 Tool](https://gchq.github.io/CyberChef/#recipe=MD5())

## Sicherheitsaspekte

MD5 ist **nicht** sicher weil:

- Kollisionsanfälligkeit: Es ist möglich, zwei unterschiedliche Eingaben zu finden, die denselben MD5-Hash erzeugen. Dies wurde erstmals 2004 demonstriert und hat gezeigt, dass MD5 nicht kollisionsresistent ist.

- Praktische Angriffe: 2008 gelang es Forschern, mithilfe eines Clusters von PlayStation 3-Konsolen ein gefälschtes SSL-Zertifikat zu erstellen, das von Browsern als vertrauenswürdig angesehen wurde. Dies unterstreicht die realen Sicherheitsrisiken von MD5.

- Schnelle Berechnung: MD5 ist sehr schnell, was es Angreifern erleichtert, durch Brute-Force- oder Wörterbuchangriffe Passwörter zu knacken. Daher ist es für die Passwortspeicherung ungeeignet.

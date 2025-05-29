---
weight: 999
title: "Certificates"
description: ""
icon: "article"
date: "2025-05-29T09:57:26+02:00"
lastmod: "2025-05-29T09:57:26+02:00"
draft: true
toc: true
---

## Einleitung

Zertifikate sind digitale Dokumente, die verwendet werden, um die Identität von Personen, Organisationen oder Geräten zu bestätigen. Sie spielen eine entscheidende Rolle in der Public-Key-Infrastruktur (PKI) und sind ein wesentlicher Bestandteil der sicheren Kommunikation im Internet.

Mithilfe von Zertifikaten können asymmetrische Schlüsselpaare (bestehend aus einem öffentlichen und einem privaten Schlüssel) verifiziert werden. Zertifikate enthalten Informationen über den Inhaber, den Aussteller und die Gültigkeitsdauer des Zertifikats sowie den öffentlichen Schlüssel des Inhabers.

Fragestellung: Wie kann man sicher sein, dass der öffentliche Schlüssel eines Kommunikationspartners tatsächlich zu dieser Person oder Organisation gehört?


## Bindungsproblem

### Begriffserklärungen

- **Schlüsselbindung**:  
  Zuordnung eines öffentlichen Schlüssels zu einem Kommunikationsteilnehmer.

- **Gültige Schlüsselbindung**:  
  Der öffentliche Schlüssel „gehört“ tatsächlich zum angegebenen Teilnehmer.

- **Bindungsproblem**:  
  Das Problem zu entscheiden, **ob eine Schlüsselbindung gültig ist**.

---

### Problemstellung

Alice möchte sicherstellen,  
dass wirklich **Bob** (und nicht ein Angreifer) behauptet,  
dass $k$ sein **öffentlicher Schlüssel** ist.

→ Dazu ist ein **authentischer Kanal** nötig,  
über den Bob **Alice mitteilt**, dass $k$ sein Schlüssel ist.

> Hinweis:  
> Alice kann dann sicher sein, dass Nachrichten über diesen Kanal tatsächlich von Bob stammen.

---

### Vergleich: Austausch geheimer Schlüssel

Haben wir durch asymmetrische Verfahren mit öffentlichen Schlüsseln etwas gewonnen?

✅ **Ja – falls wir das Bindungsproblem auslagern**.

---

### Lösung: Zertifizierungsstellen (CAs)

- Alice prüft die Bindung **nicht selbst**.
- Stattdessen verlässt sie sich auf eine **Zertifizierungsstelle (CA)**.
- Diese stellt ein **Zertifikat** aus, das die **Gültigkeit** einer Schlüsselbindung bestätigt.

---

### Lösungskonzept: Public-Key-Infrastruktur (PKI)

> Die PKI übernimmt die Vertrauenswürdigkeit von Schlüsselbindungen  
> mithilfe von **Zertifikaten** und **Zertifizierungsinstanzen**.








## Zertifikat und Schlüsselbindung

Ein **Zertifikat** ist ein **digital signiertes Dokument**, das eine Schlüsselbindung in Form einer entsprechenden Aussage bezeugt, etwa der Form:

> „Hiermit bestätigt die Zertifikationsstelle $Z$, dass der Person/Firma/Organisation $Y$ der Schlüssel $k$ gehört.“

---

### Voraussetzung

Bevor eine Zertifizierungsstelle $Z$ ein solches Dokument signiert, muss sie sich **von der Gültigkeit der Schlüsselbindung $(Y, k)$ überzeugen**.

Das genaue Verfahren ist im sogenannten  
**Certification Practice Statement** von $Z$ festgelegt.

---

### Anforderungen

Ein Zertifikat sollte:

- bestimmten Standards und gesetzlichen Regelungen entsprechen
- je nach Sicherheitsstufe (mehr oder weniger gründliche Prüfungen)  
  auch **mehrere 100 bis 1.000 Dollar kosten**

---

### Notation

Ein Zertifikat, das die Gültigkeit der Schlüsselbindung $(Y, k)$ bezeugt,  
ausgestellt von der Zertifizierungsstelle $Z$ und mit dem **privaten Schlüssel** $\hat{k}_Z$ von $Z$ signiert wurde,  
bezeichnen wir mit:

$$
\text{Zert}_{\hat{k}_Z}(Y, k)
$$


## PKI-Struktur und Zertifikatskette

Die Struktur einer PKI ist typischerweise hierarchisch aufgebaut und wird oft als Zertifikatskette oder Vertrauenskette (Chain of Trust) bezeichnet. Diese Kette beginnt bei einem Endnutzerzertifikat und führt über ein oder mehrere Zwischenzertifikate bis zu einem Wurzelzertifikat (Root Certificate).

**Certificate Authority (CA)**: Eine Zertifizierungsstelle (**CA**) ist eine vertrauenswürdige Organisation, die digitale Zertifikate ausstellt, signiert und verwaltet. Sie bürgt für die Authentizität der in einem Zertifikat enthaltenen Informationen.

**Root CA** (Stammzertifizierungsstelle): Die Root CA ist die oberste Instanz in der Hierarchie und bildet den Vertrauensanker. Root-Zertifikate sind selbstsigniert, das bedeutet, die CA signiert ihr eigenes Zertifikat. Diese Zertifikate sind in Betriebssystemen und Browsern oft vorinstalliert, wodurch den von dieser Root CA (direkt oder indirekt) ausgestellten Zertifikaten vertraut wird. Root CAs stellen in der Regel keine Zertifikate direkt für Endnutzer aus, um ihr eigenes Risiko zu minimieren.

**Intermediate CA** (Zwischenzertifizierungsstelle): Eine Intermediate CA ist eine untergeordnete Zertifizierungsstelle, deren Zertifikat von der Root CA (oder einer anderen Intermediate CA) signiert wurde. Sie agieren im Auftrag der Root CA und können ihrerseits Zertifikate für andere Intermediate CAs oder für Endnutzer (z. B. Webserver, E-Mail-Nutzer) ausstellen. Die Verwendung von Intermediate CAs erhöht die Sicherheit und Flexibilität der PKI. Wenn eine Intermediate CA kompromittiert wird, können deren Zertifikate widerrufen werden, ohne die gesamte PKI und das Vertrauen in die Root CA zu gefährden.

**Endnutzerzertifikat** (Leaf Certificate): Dies ist das Zertifikat, das einer spezifischen Entität (z. B. einer Webseite, einem Benutzer) ausgestellt wird. Es wird von einer Intermediate CA (oder in selteneren Fällen direkt von einer Root CA in kleineren Setups) signiert.



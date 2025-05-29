---
weight: 999
title: "KRY Involved Protocols"
description: ""
icon: "article"
date: "2025-05-29T11:03:32+02:00"
lastmod: "2025-05-29T11:03:32+02:00"
draft: true
toc: true
---

## Einleitung

In diesem Abschnitt werden Protokolle vorgestellt, die in der Kryptografie eine Rolle spielen. Diese Protokolle sind entscheidend für die sichere Kommunikation und den Austausch von Informationen in verschiedenen Anwendungen.

## Ping Protokoll mit verschlüsselter Nachricht

### Erklärung

Das Ping-Protokoll ist ein einfaches Kommunikationsprotokoll, das verwendet wird, um die Erreichbarkeit eines Hosts zu überprüfen. In diesem Szenario wird eine verschlüsselte Nachricht verwendet, um die Kommunikation zwischen Alice und Bob zu sichern.

### Replay-Angriff

In diesem Szenario versucht Alice, mit Bob zu kommunizieren und sich zu authentifizieren. Die Kommunikation wird jedoch durch einen Angreifer abgefangen und erneut verwendet.

### Ablauf

1. [1. Sitzung] Alice sendet: `"ping", E(N_A, K)` an Bob.
2. [1. Sitzung] Der Angreifer fängt die Nachricht jedoch vorher ab und speichert sie.
3. [2. Sitzung] Der Angreifer erstellt eine zweite Sitzung und sendet die speicherte Nachricht an Alice.
4. [2. Sitzung] Alice entschlüsselt die Nachricht und sendet `N_A` an den Angreifer zurück.
5. [2. Sitzung] Der Angreifer erhält `N_A` und speichert diese.
6. [1. Sitzung] Der Angreifer sendet `N_A` an Alice in der ersten Sitzung zurück.

### Problem

- Alice glaubt, mit Bob gesprochen zu haben.
- Bob war jedoch nie beteiligt.
- Die **einseitige Authentifizierung** ist daher **nicht gewährleistet**.

### Lösung

Es gibt mehrere Lösungsansätze:
- Alice speichert bei der 1. Sitzung `N_A` und wird bei der Entschlüsselung in der 2. Sitzung prüfen, ob `N_A` bereits in einer anderen Sitzung verwendet wurde und ggf. die Entschlüsselung abbrechen.
- Alice könnte auch einen Zeitstempel oder eine Nonce verwenden, um sicherzustellen, dass die Nachricht nicht wiederverwendet wird.
- Eine weitere Möglichkeit ist die Verwendung von **Challenge-Response-Protokollen**, bei denen Alice eine Herausforderung an Bob sendet, die dieser beantworten muss, um seine Identität zu bestätigen.

## Needham-Schroeder Protokoll

### Erklärung

Das Needham-Schroeder Protokoll ist ein bekanntes Authentifizierungsprotokoll, das ursprünglich für die sichere Kommunikation zwischen zwei Parteien entwickelt wurde. Es verwendet asymmetrische Kryptografie, um die Identität der Kommunikationspartner zu überprüfen.

### Funktionsweise

Alice:
- Name: A
- Nachricht: $N_a$
- Schlüsselpaar: $(Priv_a, Pub_a)$

Bob:
- Name: B
- Nachricht: $N_b$
- Schlüsselpaar: $(Priv_b, Pub_b)$

#### Vorgehen

1. Alice sendet an Bob: $E(N_a || A, Pub_b)$.
2. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_a || A$.
3. Bob sendet an Alice: $E(N_a || N_b, Pub_a)$.
4. Alice entschlüsselt die Nachricht mit ihrem privaten Schlüssel und erhält $N_a || N_b$.
5. Alice sendet an Bob: $E(N_b, Pub_b)$.
6. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_b$.

### Problem (Lowe)

Alice:
- Name: A
- Nachricht: $N_a$
- Schlüsselpaar: $(Priv_a, Pub_a)$

Bob:
- Name: B
- Nachricht: $N_b$
- Schlüsselpaar: $(Priv_b, Pub_b)$

Eva:
- Name: E
- Nachricht: $N_e$
- Schlüsselpaar: $(Priv_e, Pub_e)$

#### Vorgehen

1. Alice sendet an Eva (bewusst): $E(N_a || A, Pub_e)$.
2. Eva entschlüsselt die Nachricht mit ihrem privaten Schlüssel und erhält $N_a || A$.
3. Eva sendet an Bob: $E(N_a || A, Pub_b)$.
4. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_a || A$.
5. Bob sendet an Eva (denkt aber es wäre Alice): $E(N_a || N_b, Pub_a)$.
6. Eva leitet die gleiche Nachricht an Alice weiter: $E(N_a || N_b, Pub_a)$.
7. Alice entschlüsselt die Nachricht mit ihrem privaten Schlüssel und erhält $N_a || N_b$.
8. Alice sendet an Eva: $E(N_b, Pub_e)$.
9. Eva entschlüsselt die Nachricht mit ihrem privaten Schlüssel und erhält $N_b$.
10. Eva sendet an Bob: $E(N_b, Pub_b)$.
11. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_b$.

- B glaubt einen geheimen Schlüssel $N_b$ mit A zu teilen.
- Dieser st aber dem Angreifer bekannt.
- Sicherer Schlüsselaustausch ist also nicht gegeben.

### Problem Lösung (Needham-Schroeder-Lowe)

Bob sendet seinen Namen ebenfalls mit:

#### Vorgehen

1. Alice sendet an Bob: $E(N_a || A, Pub_b)$.
2. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_a || A$.
3. Bob sendet an Alice: $E(N_a || N_b || B, Pub_a)$.
4. Alice entschlüsselt die Nachricht mit ihrem privaten Schlüssel und erhält $N_a || N_b || B$.
5. Alice sendet an Bob: $E(N_b, Pub_b)$.
6. Bob entschlüsselt die Nachricht mit seinem privaten Schlüssel und erhält $N_b$.

Falls bei (4) ein anderer Name als 'B' erscheint, sollte Alice das Protokoll abbrechen (falls sie vertrauenswürdig ist).

## SSL TLS

### Erklärung

SSL (Secure Sockets Layer) und TLS (Transport Layer Security) sind Protokolle, die für die sichere Kommunikation über Computernetzwerke entwickelt wurden. Sie bieten Verschlüsselung, Authentifizierung und Integritätsschutz für Daten, die über das Internet übertragen werden.

### Funktionsweise

SSL/TLS verwendet eine Kombination aus symmetrischer und asymmetrischer Kryptografie, um eine sichere Verbindung zwischen Client und Server herzustellen. Der Prozess umfasst mehrere Schritte:

1. **Handshake**: Der Client und der Server tauschen Nachrichten aus, um die Version des Protokolls, die unterstützten Verschlüsselungsmethoden und die Authentifizierungsmethoden zu vereinbaren.

2. **Zertifikate**: Der Server sendet sein digitales Zertifikat, das von einer vertrauenswürdigen Zertifizierungsstelle (CA) signiert ist. Der Client überprüft die Gültigkeit des Zertifikats und stellt sicher, dass es zu dem Server gehört, mit dem er kommunizieren möchte.

3. **Schlüsselaustausch**: Der Client generiert einen Sitzungsschlüssel, der für die symmetrische Verschlüsselung der Daten verwendet wird, und sendet diesen an den Server, verschlüsselt mit dem öffentlichen Schlüssel des Servers.

4. **Verschlüsselung**: Nach dem Handshake verwenden der Client und der Server den Sitzungsschlüssel, um die Daten zu verschlüsseln, die über die Verbindung gesendet werden.

5. **Integritätsschutz**: SSL/TLS verwendet HMAC (Hash-based Message Authentication Code), um die Integrität der übertragenen Daten sicherzustellen.


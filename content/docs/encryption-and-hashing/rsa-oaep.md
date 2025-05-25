---
weight: 999
title: "RSA OAEP"
description: ""
icon: "article"
date: "2025-05-25T13:47:40+02:00"
lastmod: "2025-05-25T13:47:40+02:00"
draft: false
toc: true
katex: true
---

# Einleitung

RSA OAEP (Optimal Asymmetric Encryption Padding) ist eine Methode zur sicheren Verschlüsselung von Daten mit RSA. Es verbessert die Sicherheit der RSA-Verschlüsselung, indem es eine zusätzliche Schicht der Zufälligkeit und Sicherheit hinzufügt.

## Voraussetzungen

- Zwei Hash-Funktionen: `H1` und `H2` mit Hashbreiten `l1` und `l2`.
- RSA Schlüsselpaar `((n,e), (n,d))`
- Klartext x welcher mit einem geeigneten Padding in Binärdarstellung eine Länge von `l1` hat. (Es muss $n \geq 2^{l_1 + l_2}$ gelten.)

## Schritte für RSA-OAEP-E(x, (n, e))

1. Wähle einen Zufallsstring $r$ der Länge $l_2$.

2. Bilde  
   $$
   t = \quad x \oplus H_1(r) \quad \,\|\, \quad r \oplus H_2(x \oplus H_1(r))
   $$

3. Gib $y = \mathrm{RSA}\text{-}E(t, (n, e))$ aus.





## Schritte für RSA-OAEP-D(y, (n, d))

1. $t = D(y, (n, d))$

2. Es sei $t = t_1 \,\|\, t_2$, wobei $t_1$ die ersten $l_1$ Bits und $t_2$ die restlichen $l_2$ Bits darstellen.  
   *(Hierbei hat $t$ die Länge $l_1 + l_2$ in Binärdarstellung, ggf. werden also vorne Nullen eingefügt.)*

3. Berechne $r = t_2 \oplus H_2(t_1)$.

4. Gib $x = t_1 \oplus H_1(r)$ zurück.

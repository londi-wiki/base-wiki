---
weight: 999
title: "Message Authentication Code (MAC)"
description: ""
icon: "article"
date: "2025-05-27T09:18:56+02:00"
lastmod: "2025-05-27T09:18:56+02:00"
draft: false
toc: true
katex: true
---

# Einleitung

Message Authentication Codes (MACs) sind kryptografische Prüfziffern, die verwendet werden, um die **Integrität** und **Authentizität** von Nachrichten zu gewährleisten. Sie kombinieren einen geheimen Schlüssel mit der Nachricht, um eine eindeutige Prüfziffer zu erzeugen, die nur von autorisierten Parteien verifiziert werden kann.

## Definition

Ein **symmetrisches Authentifizierungsverfahren (Message Authentication Code, MAC)** ist ein Tupel  
$$
M = (X, K, Y, T, V)
$$  
mit:

- einer nicht-leeren Menge $X$ von **Klartexten**
- einer nicht-leeren Menge $K$ von **Schlüsseln**
- einer nicht-leeren Menge $Y$ von **Etiketten**
- einem effizienten probabilistischen **Etikettieralgorithmus**  
  $$
  T : X \times K \rightarrow Y
  $$
- einem effizienten deterministischen **Verifikationsalgorithmus**  
  $$
  V : X \times Y \times K \rightarrow \{0,1\}
  $$

sodass gilt (Verifizierung von einem Tag):  
$$
\forall x \in X,\, k \in K: \quad V(x, T(x,k), k) = 1
$$

---

Wir nennen $(x, t)$ ein **gültiges Nachrichten-Etikett-Paar** (bzgl. $k$), falls  
$$
V(x, t, k) = 1
$$

Ist $(x, t)$ ein gültiges Paar, so heisst $t$ ein **gültiges Etikett zu $x$** (bzgl. $k$).

## Arten von MACs

Es gibt verschiedene Arten von MACs, die sich in ihrer Funktionsweise und Sicherheit unterscheiden:
- **HMAC (Hash-based Message Authentication Code)**: Verwendet kryptografische Hash-Funktionen zusammen mit einem geheimen Schlüssel.
- **CMAC (Cipher-based Message Authentication Code)**: Nutzt symmetrische Verschlüsselungsalgorithmen wie AES zur
- **CBC-MAC**: Eine Variante von CMAC, die den Cipher Block Chaining Modus verwendet.

# CBC MAC

## Definition

Es sei  
$$
B = (\{0,1\}^l, \{0,1\}^s, \{0,1\}^l, e, d)
$$  
mit $l, s > 0$ ein Blockkryptosystem.

Der dadurch induzierte **CBC-MAC** $M_{CBC}$ ist wie folgt definiert:

$$
M_{CBC} = (\{0,1\}^{l+}, \{0,1\}^s, \{0,1\}^l, T, V)
$$

mit dem Etikettieralgorithmus $T(x,k)$:

1. Zerlege $x$ in Blöcke $x_0, \dots, x_{n-1}$ mit $x_i \in \{0,1\}^l,\ i = 0, \dots, n-1$  
2. Setze $y_{-1} = 0^l$
3. Berechne  
   $$
   y_i = e(y_{i-1} \oplus x_i, k) \quad \text{für } i = 0, 1, \dots, n-1
   $$
4. Gib $y_{n-1}$ aus

Da $T$ deterministisch ist, ist damit auch $V$ definiert.

---

### Bemerkung

Selbst bei langen Nachrichten besteht der **CBC-MAC** nur aus **einem Block**.

Dies ist bei der **Verschlüsselung** nicht so, da **alle Blöcke** zur Rekonstruktion der Nachricht benötigt werden.

## Beispiel

### Aufgabe 1

Gegeben sei folgendes Blockkryptosystem der Länge $3$ mit Schlüssellänge $2$.  
Die Verschlüsselungsfunktion $e$ ist durch folgende Tabelle gegeben:

|     $e(k, m)$     | 000 | 001 | 010 | 011 | 100 | 101 | 110 | 111 |
|:-----------------:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **00** (k = 00)   | 001 | 010 | 011 | 100 | 101 | 110 | 111 | 000 |
| **01** (k = 01)   | 010 | 011 | 100 | 101 | 110 | 111 | 000 | 001 |
| **10** (k = 10)   | 011 | 100 | 101 | 110 | 111 | 000 | 001 | 010 |
| **11** (k = 11)   | 100 | 101 | 110 | 111 | 000 | 001 | 010 | 011 |

---

1. Berechnen Sie mit dem darauf basierenden **CBC-MAC** das **Etikett zur Nachricht**
   $$
   x = \texttt{000 111 000}
   $$  
   mit dem Schlüssel  
   $$
   k = \texttt{10}.
   $$

2. Überprüfen Sie, ob  
   $$
   (x = \texttt{010 101 000},\ t = \texttt{111})
   $$  
   ein **gültiges Nachrichten-Etikett-Paar** zum Schlüssel  
   $$
   k = \texttt{01}
   $$  
   ist (beim **CBC-MAC**).

#### Lösungsweg Aufgabe 1

**Gegeben:**

- $x = \texttt{000 111 000}$
- $k = \texttt{10}$
- $\text{IV (Initialisierungsvekor)} = y_{-1} = 000$

**Gesucht:**

- $t$

**Vorgehen:**

1. $y_0 = e(000 \oplus 000) = e(000) = 011$
2. $y_1 = e(011 \oplus 111) = e(100) = 111$
3. $y_2 = e(111 \oplus 000) = e(111) = 010$

**Lösung:**

$t = 010$

#### Lösungsweg Aufgabe 2

**Gegeben:**

- $x = \texttt{010 101 000}$
- $t = \texttt{111}$
- $k = \texttt{01}$
- $\text{IV (Initialisierungsvekor)} = y_{-1} = 000$

**Gesucht:**

- $t = t'$

**Vorgehen:**

1. $y_0 = e(000 \oplus 010) = e(010) = 100$
2. $y_1 = e(100 \oplus 101) = e(001) = 011$
3. $y_2 = e(011 \oplus 000) = e(011) = 101$

**Lösung:**

$111 \neq 101 ,\ \text{111 ist somit nicht das passende Etikett}$


## Problem mit Nachrichtenlänge

### Aufgabe 3

Es sei $m = m_0 m_1$ eine Nachricht aus zwei Blöcken der Länge $l$.  
Es sei $I \,\|\, t$ der zugehörige **CBC-MAC**, bei dem $I$ als Initialisierungsvektor verwendet wurde.

Es sei $m' = m_0' m_1$.  
(Der zweite Block stimmt mit dem zweiten Block von $m$ überein.)

---

**Rechnen Sie nach**, dass dann  
$$
I \oplus m_0 \oplus m_0' \,\|\, t
$$  
ein gültiges Etikett zu $m'$ ist.

Rechnen Sie nach, dass dann  
$$
I \oplus m_0 \oplus m_0' \,\|\, t
$$  
ein gültiges Etikett zu $m'$ ist.

---

Das zeigt, dass der CBC-MAC **unsicher ist**, wenn man den Initialisierungsvektor zufällig wählt und **vor** das Etikett hängt.

---

### Lösung:

Wir berechnen:

$$
E\left(m_0' \oplus \left(I \oplus m_0 \oplus m_0'\right), k\right)
= E(m_0 \oplus I, k) = y_0
$$

$$
E(m_1 \oplus y_0, k) = y_1
$$

Nun ist $t = y_1$.

Damit ist  
$$
I \oplus m_0 \oplus m_0' \,\|\, t
$$  
ein **gültiges Etikett** zu $m'$.




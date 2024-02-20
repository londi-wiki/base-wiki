---
weight: 999
title: "Allgemeine Wahrscheinlichkeit"
description: ""
icon: "article"
date: "2023-10-09T19:05:45+02:00"
lastmod: "2023-10-09T19:05:45+02:00"
draft: true
toc: true
katex: true
---

## Allgemeine Wahrscheinlichkeit

### Kolmogoroff

Satz: Es sei P eine Wahrscheinlichkeit auf $\Omega$. Dann gilt:

(1)

$\forall E \subseteq \Omega: P(E^{c}) = 1- P(E)$

$1 = P(\Omega) = P(E \cup E^{c}) = P(E) + P(E^{c}) => P(E^{c}) = 1- P(E)$

(2)

$P(\emptyset) = 0$

(3)

$\forall E_{1},E_{2} \subseteq \Omega : P(E_{1} \cup E_{2}) = P(E_{1}) + P(E_{2}) - P(E_{1} \cap E_{2})$

(4)

Für eine endliche oder abzählbare Menge E = {e1, e2, ...} gilt:

$P(E) = P(\\{e1\\}) + P(\\{e2\\}) + ...$

### Beispiel

Siehe Folie (2.4) Glücksrad

## Bedingte Wahrscheinlichkeit

### Beispiel 1 (ein Würfel)

Gegeben: Ein Würfel: $\Omega = \\{1,2,3,4,5,6\\}$

Wie hoch ist die Wahrscheinlichkeit für $A = \\{2,3\\}$, wenn man weiss, dass eine ungerade Zahl gewürfelt wurde?

Eingeschränkte Menge: $B = \\{1,3,5\\}$ sprich |B| = 3 Ergebnisse möglich.

Davon ist $|A \cap B| = 1$ Ergebnis günstig (die 3).

Gesuchte Wahrscheinlichkeit: $\frac{|A \cap B|}{|B|} = \frac{1}{3}$

Definition lautet allgemein also: $P(A|B) = \frac{P(A \cap B)}{P(B)}$. 

"Bedingte Wahrscheinlichkeit von A _unter_ B"

### Beispiel 2 (zwei Würfel)

Zwei Würfel: Wahrscheinlichkeit für Augensumme 7, wenn das Produkt der Augen 12 ist.

x + y = 7

x * y = 12

$\Omega = \\{1,2,3,4,5,6\\} \times \\{1,2,3,4,5,6\\}$

P = Gleichverteilung (Laplace)

Augensumme 7: $A = \\{ (1,6),(2,5),(3,4),(4,3),(5,2),(6,1) \\}$ sprich |A| = 6 Ergebnisse.

Augenprodukt 12: $B = \\{ (2,6),(3,4),(4,3),(6,2) \\}$ sprich |B| = 4 Ergebnisse.

$P(A|B) = \frac{P(A \cap B)}{P(B)} = \frac{|A \cap B|}{|B|} = $\frac{2}{4} = $\frac{1}{2}$. 

### Beispiel 3 (Karten)

32 Karten: Wie gross ist die Wahrscheinlichkeit einen König zu ziehen, wenn man weiss, eine Herzkarte gezogen zu haben?

Modellierung: $\Omega = \\{ 7_{Kreuz}, 8_{Kreuz}, 9_{Kreuz}, ..., Ass_{Herz} \\}$ (Alle Karten)

P = Gleichverteilung (Laplace)

$A = \\{ K_{Kreuz}, K_{Herz}, K_{Schaufel}, K_{Ecke} \\}$ sprich |A| = 4 Ergebnisse.

$B = \\{ 7_{Herz}, 8_{Herz}, 9_{Herz}, ..., Ass_{Herz} \\}$ sprich |A| = 8 Ergebnisse.

$P(A|B) = \frac{P(A \cap B)}{P(B)} = \frac{|A \cap B|}{|B|} = \frac{1}{8}$. 

$P(A) = \frac{1}{8}= P(A|B)$ => Somit hilft/nützt die Information, dass eine Herzkarte gezogen wurde nichts in Bezug auf die Wahrscheinlichkeit, dass es ein König war.


## Formel von Bayes - Formel der totalen Wahrscheinlichkeit

Es sei $\Omega$ eine nichtleere endliche Menge und P eine Wahrscheinlichkeitsverteilung auf $\Omega$. Ferner seien $A, B \subseteq \Omega > 0 \text{ und } P(B) > 0$

Dann gilt $P(A | B) = \frac{P(A)}{P(B)} * P(B | A)$. 

Beweis: Siehe Folie 2.7

### Beispiel 1

Gegeben: Irgend eine Population:
- 40% sind weiblich
- 60% sind männlich
- weibliche Personen wiegen 10% mehr als 70kg
- männliche Personen wiegen 80% mehr als 70kg

Wie viele total wiegen mehr als 70kg (Anzahl)?

Insgesamt wiegen (0.1 * 0.4) + (0.8 * 0.6) mehr als 70kg.

FORMEL

### Beispiel 2

Eine Krankheit tritt bei 2 von 10'000 Personen auf. Der Sachverhalt K, dass eine Person diese Krankheit bekommt, hat eine Wahrscheinlichkeit P(K) = 0.0002.

Der verwendete Screening-Test hat eine Genauigkeit von 99%, $P(T | K) = 0.99$. Also erkennt bei 99% der erkrankten Personen, 
dass sie die Krankheit haben und ist zu 99% genau, dass eine Person die Krankheit nicht hat, $P( T^{c} | K^{c} ) = 0.99$

Gesucht ist der positive prädiktive Wert P(K | T).

$ P(K | T) = \frac{ P(K) * P(T | K) } { P(T | K) * P(K) + P(T | K^{c}) * P(K^{c}) } = \frac{0.0002 * 0.99}{0.99 * 0.0002 + 0.01 * 0.9998} \approx 0.019 $

K^{c} = 0.1 - 0.0002 = 0.9998

Die Wahrscheinlichkeit, dass eine positiv getestete Person tatsächlich krank ist, beträgt in diesem Beispiel also nur run 1.9 Prozent. 
Das heisst, eine positiv getestete Person hat immer noch eine Chance von über 98 Prozent, gesund zu sein, obwohl der Test sie als krank eingestuft hat.



## Stochastische Unabhängigkeit

Definition: Es sei P eine Wahrscheinlichkeitsverteilung auf $\Omega$

Zwei Ereignisse $A, B \subseteq \Omega$ heissen stochastisch unabhängig, falls:

$P(A \cap B) = P(A) * P(B)$.

Im Falle $P(B) \neq 0$ ist dies äquivalent zu $P(A|B) = \frac{ A \cap B }{P(B)} = P(A)$. 

### Beispiel

Siehe Folie 2.10

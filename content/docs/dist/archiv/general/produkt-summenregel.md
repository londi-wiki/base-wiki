---
title : 'Produkt Summenregel'
date : 2023-10-02T16:43:34+02:00
tags: ["draft"]
author: "Leon"
katex: true
draft: true
---

# Produktregel / Summenregel

> Summenregel: Wenn die Mengen allesamt disjunkt voneinander sind, können diese Zusammengezählt werden.
> Produktregel: Mehrstufige Auswahlprozesse
 
# Urnenmodell

Gegeben ist eine Urne mit n unterschiedlichen Kugeln. Wir ziehen k Kugeln aus den n Kugeln. Auf wie viele Arten geht das, 
wenn:

- (1) wir die Kugeln wieder zurücklegen und die Reihenfolge der gezogenen Kugeln wichtig ist? (Passwort)
- (2) wir die kugeln **nicht** zurücklegen und die Reihenfolge der gezogenen Kugeln wichtig ist? (Möglichkeiten Bücher nebeneinander ins Regal zu stellen)
- (3) wir die kugeln **nicht** zurücklegen und die Reihenfolge der gezogenen Kugeln **nicht** wichtig ist? (Lotto)
- (4) wir die Kugeln wieder zurücklegen und die Reihenfolge der gezogenen Kugeln **nicht** wichtig ist? (Getränke Harasse mit beliebigen Getränkeflaschen füllen)

## (1) Mit Zurücklegen, mit Reihenfolge

- Produktregel: k-mal herausnehmen

Bild Folie 13

Ergebismenge besteht aus mehreren Tuplen weil die Reihenfolge wichtig ist.

|M| = n^k Möglichkeiten

### Beispiel:

- 3 unterschiedliche Bonbons
- 4 Kinder

Auf wie viele Arten kann man die Bonbons auf die Kinder verteilen (Kinder dürfen auch leer ausgehen)?

$Bonbons \in (a, b, c)$ => k = 3

$Kinder \in (1, 2, 3, 4)$ => n = 4

(a, b, c)

$(4,4,4) => n^{k} = 4^{3} = 125$


## (2) nicht Zurücklegen, mit Reihenfolge

- Produktregel: k-mal herausnehmen

Ergebismenge besteht aus mehreren Tuplen weil die Reihenfolge wichtig ist.

Bild Folie 14

- Für die erste Kugel gibt es n Möglichkeiten
- zweite n-1
- dritte n-2
- ...
- k-te Kugel n - (k - 1) = n - k + 1

### Beispiel

- Bilderrahmen mit drei untereinander angeordneten Plätzen
- 5 Fotos

Auf wie viele Arten kann man die Bilderrahmen füllen?

$Bilderrahmen \in (a, b, c)$

$Bilder \in (1, 2, 3, 4, 5)$

(a, b, c)

(5, 4, 3) = 60 Möglichkeiten

### Spezialfall

n = k

$n * (n - 1) * ... * 2 * 1$ Möglichkeiten.

**Definition**

Es sei $n \in N$. Dann heisst n! = n * (n - 1) * (n - 2) * ... * 2 * 1

- Fakultät. => =! = 1
- n! wächst sehr schnell.
- Es gilt (in Bezug auf den Wachstum): n! ~ $\sqrt{2 * \pi * n} * (\frac{n}{e})^{n}$ => Stirlingformel (Stirling's approximation)

=> $\frac{n!}{(n-k)!}$

### Beispiel

- Nebeneinander anordnen von 10 verschiedenen Büchern

10! => 3'628'800

## (3) nicht Zurücklegen, ohne Reihenfolge

- Menge also Additionsverfahren

M = (alle k-elementigen Teilmengen von (1,2,...,n))

### Beispiel

- n = 5
- k = 3

**Reihenfolge egal**

M = {{1,2,3}, {1,2,4}, {1,2,5}, ... }

|M| = 10

Wenn wir die Reihenfolge beachten würden (Mr), dann hätte man alleine für die Kombination aus {1,2,3}, 3! = 6 verschiedene Möglichkeiten.

In diesem Fall würde es in Mr = 5 * 4 * 3 Möglichkeiten geben.

Was ist der Zusammenhang zwischen |M| und |Mr|? 

Es gilt: |M| * k! = |Mr|, also |M| = $\frac{|Mr|}{k!} = \frac{n!}{(n-k)!k!}$

### Beispiel

6 aus 42: Wie viele verschiedene Lotto-Scheine gibt es?

Wir ziehen k = 6 mal aus einer Menge von n = 42 Zahlen. Ohne Zurücklegen, ohne Beachtung der Reihenfolge. 
Es gibt also $\frac{42!}{(42-6)!k!}$ = 5'234'786 Möglichkeiten.

Stichwort: Binomialkoeffizient

Definition: Es sei 0 <= k <= n.

Dann ist der Binomialkoeffizient $\binom{n}{k}$ definiert als $\frac{n!}{(n-k)!k!}$

Für k > n ist $\binom{n}{k}$ := 0

"n über k" => gibt also die Anzahl aller k-elementigen Teilmengen einer n-elementigen Menge an.

### Beispiel (1)

- Aus einer Gruppe von 12 Personen werden 5 gewählt

Wie viele Möglichkeiten gibt es?

Wir ziehen k = 5 mal aus einer Menge von n = 12 Leuten. Ohne Zurücklegen, ohne Beachtung der Reihenfolge. Es gibt also $\binom{12}{5}$ Möglichkeiten.

### Beispiel (2)

- Aus einer gruppe von 8 Frauen und 4 Männern werden 3 Frauen und 2 Männer gewählt.

Wie viele Möglichkeiten gibt es?

Stichwort: Mehrstufiger Auswahlprozess

Schritt 1: Wähle 3 von 8 Frauen aus: $\binom{8}{3}$ Möglichkeiten

Schritt 2: Wähle 2 von 4 Männer aus: $\binom{4}{2}$ Möglichkeiten

Schritt 3: Gesamt (Multiplikation): $\binom{8}{3}$ * $\binom{4}{2}$

Wann wäre es eine Addition? "Wie viele Selektionen gibt es, die **entweder** aus 3 Frauen **oder** 2 Männern bestehen?"

## Allgemeine Beispiele 1 (Lotto)

- Ziehung 6 aus 45
- 6 gezogen, ohne Zurücklegen und Reihenfolge wird nicht beachtet

Wie gross ist die Wahrscheinlichkeit, dass:

- (1) alle Zahlen grösser als 10?
- (2) man 6 Richtige hat?
- (3) **mindestens** 4 Richtige hat?

Ergebnismenge $\Omega$ = {alle 6 elementigen Teilmengen von {1, ..., 45}} => 45 Elemente

p = Gleichverteilung d.h. Laplace (Annahme)

(1)

Ereignismenge E = { alle 6 elementigen Teilmengen von { 11, ..., 45 }} => 35 Elemente

=> P(E) = $\frac{|E|}{|\Omega|} = \frac{\binom{35}{6}}{\binom{45}{6}} \approx 19.93\\%$

(2)

|E| = 1 (Weil es nur eine Möglichkeit gibt, dass 6 aus 6 richtig sind)

=> P(E) = $\frac{|E|}{|\Omega|} = \frac{1}{\binom{45}{6}} \approx 0,0000123\\%$

(3)

|E| = mindestens 4 Richtige

=> "mindestens 4" heisst: 

- "exakt 4 Richtige" $\cup$ 
- "exakt 5 Richtige" $\cup$ 
- "exakt 6 Richtige" <= 1 Möglichkeit

Ähnlich wie das "Gruppe Selektions"-Beispiel.


Bei "exakt 4 Richtige": 4 sind richtig $\binom{6}{4}$, somit kann man aus 39 verbleibenden Kugeln 
noch 2 falsche ziehen und das sind $\binom{39}{2}$

=> $\binom{6}{4}$ * $\binom{39}{2}$

Bei "exakt 5 Richtige": 5 sind richtig $\binom{6}{5}$, somit kann man aus 39 verbleibenden Kugeln 
noch 1 falsche ziehen und das sind $\binom{39}{1}$

=> $\binom{6}{5}$ * $\binom{39}{1}$

Somit: $\frac{\binom{6}{4} * \binom{39}{2} + \binom{6}{5} * \binom{39}{1} + 1}{\binom{45}{6}}$


## Allgemeine Beispiele 2 (Geburtstagsparadoxon)

Wie hoch ist die Wahrscheinlichkeit, dass in einer gruppe von n Leuten, zwei am selben Tag Geburtstag haben?

Modellierung: $\Omega = \\{1,2,...,365\\}^{n}$

Vorstellung: Alle Personen stellen sich in eine Reihe: [1] [2] [3] ... [n]

P = Gleichverteilung (Laplace) - Bemerkung: Nicht ganz realistisch, aber sehr gute Näherung.

Gesuchtes Ereignis: A

Bild von Folie 21

Das Gegenteil ist einfacher aufzustellen: $\Omega$\A 

und somit: P(A) = $1 - \frac{365 * (365-1)* ... * (365 -n + 1)}{365^{n}}$

Für n = 23 ergibt sich P(A) > 50%.

TODO: repertieren!


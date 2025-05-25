---
weight: 999
title: "Hashing"
description: ""
icon: "article"
date: "2025-05-24T15:10:48+02:00"
lastmod: "2025-05-24T15:10:48+02:00"
draft: false
toc: true
katex: true
---

# Einführung in Hashing

Eine Hashfunktion ist eine Funktion, die eine beliebige Eingabe (oder "Nachricht") in eine feste Länge von Bytes umwandelt. Die Ausgabe wird als "Hashwert" oder "Prüfziffer" bezeichnet. Hashfunktionen sind in der Informatik weit verbreitet und haben viele Anwendungen, einschliesslich Datenintegrität, digitale Signaturen und Passwortspeicherung.

Stichwort: MACs

# Hashfunktion


Eine Funktion $h : \{0,1\}^{\leq L} \rightarrow \{0,1\}^l$ mit $L > l > 1$ heisst *(L, l)-beschränkte Hashfunktion*.

Eine Funktion $h : \{0,1\}^* \rightarrow \{0,1\}^l$ mit $l > 1$ heisst *unbeschränkte l-Hashfunktion*.

Die Zahl $l$ heisst **Hashbreite**.

$h(x)$ heisst **Hashwert** von $x$.

## Sicherheitsanforderungen

Folgende Anforderungen sind für die Sicherheit einer Hashfunktion wichtig:
- Zweites Urbild resistent
- kollisionsresistent
- Urbild-resistent

=> Eva wäre eine Angreiferin.

### Zweites Urbild resistent (Second Preimage Resistance)

Eva kann zu $x$ den Hashwert $h(x)$ berechnen und weiss damit, was Alice erwartet.  
Es sollte für Eva deshalb schwer sein, ein $x' \ne x$ zu finden mit $h(x) = h(x')$.

**Erläuterung**

- **Gegeben:** Ein konkreter Eingabewert $x$
- **Schwierig für Angreifer (Eva):** Einen anderen Wert $x' \ne x$ zu finden, sodass  
  $$ h(x) = h(x') $$
- **Beispiel:** Alice sendet $h(x)$, und Eva kennt $x$. Sie soll **nicht** in der Lage sein, ein anderes $x'$ zu finden, das denselben Hashwert erzeugt.
- **Typischer Kontext:** Digitale Signaturen, Integritätsnachweise


### Kollisionsresistent (Collision Resistance)

Stärker und für manche Anwendungen wichtig ist es, dass Eva überhaupt kein Paar $z \ne z'$ angeben kann mit $h(z) = h(z')$.  
Das Paar $(z, z')$ heisst **Kollision**.

**Erläuterung**

- **Gegeben:** **Kein** bestimmter Wert
- **Schwierig für Angreifer:** Zwei beliebige Werte $z \ne z'$ zu finden, mit  
  $$ h(z) = h(z') $$
- **Beispiel:** Eva darf **kein beliebiges Paar** von Werten finden, die denselben Hash ergeben.
- **Strenger als:** Zweites-Urbild-Resistenz
- **Typischer Kontext:** Sicherheitsgarantie der Hashfunktion selbst

### Urbild-resistent

Manchmal ist es nur wichtig, dass Eva zu einem gegebenen Hashwert $v$ kein $x$ finden kann mit $h(x) = v$.

**Erläuterung** (Preimage Resistance)

- **Gegeben:** Ein Hashwert $v$
- **Schwierig für Angreifer (Eva):** Einen Wert $x$ zu finden, sodass  
  $$ h(x) = v $$
- **Beispiel:** Eva kennt nur den Hashwert $v$, aber **nicht**, welcher Input $x$ ihn erzeugt hat. Sie soll $x$ **nicht rekonstruieren können**.
- **Typischer Kontext:** Passwort-Hashing, allgemeiner Datenschutz

### Zusammenfassung

- **Urbild-resistent:** Gegeben $v$, finde **kein** $x$ mit $h(x) = v$  
- **Zweites-Urbild-resistent:** Gegeben $x$, finde **kein anderes** $x' \ne x$ mit $h(x') = h(x)$  
- **Kollisionsresistent:** Finde **kein Paar** $x \ne x'$ mit $h(x) = h(x')$


# Kompressionsfunktion

Eine **Kompressionsfunktion** ist eine Funktion, die eine Eingabe beliebiger Länge in eine Ausgabe fester Länge umwandelt.

**Definition:**

Es sei $l, b > 0$. Eine *$(l, b)$-Kompressionsfunktion* ist eine Funktion  
$$
f : \{0,1\}^l \times \{0,1\}^b \rightarrow \{0,1\}^l
$$  
oder auch  
$$
f : \{0,1\}^{l + b} \rightarrow \{0,1\}^l
$$

---

Die zugehörige *Iterationsfunktion*  
$$
\mathit{i^{f}} : \{0,1\}^l \times \{0,1\}^{b*} \rightarrow \{0,1\}^l
$$  
ist definiert durch:

- Leeres Wort:  
  $$
  \mathit{i^{f}}(u, \epsilon) = u \quad \text{für } u \in \{0,1\}^l
  $$

- Rekursion:  
  $$
  \mathit{i^{f}}(u, xv) = f(\mathit{i^{f}}(u, x), v) \quad \text{für } u \in \{0,1\}^l,\, x \in \{0,1\}^{b*},\, v \in \{0,1\}^b
  $$

---

Es sei $x = x_0 x_1 \dots x_{n-1} \in \{0,1\}^{bn}$ und $u \in \{0,1\}^l$ beliebig.  
Dann gilt:  
$$
\mathit{i^{f}}(u, x) = f(f(\dots f(f(u, x_0), x_1), \dots, x_{n-2}), x_{n-1}) \in \{0,1\}^l
$$

### Beobachtung

**Problem**

$ \mathit{i^{f}} $ lässt sich (bei beliebigem Initialisierungsvektor) nur auf Nachrichten anwenden, deren Länge ein Vielfaches von b ist.

**Lösung**

Fülle die Nachrichten so auf, dass ihre Länge ein Vielaches von b ist. (Geeignetes Auffüllen liefert auch eine "sichere" Hashfunktion.)

**Definition**

Die Funktion  
$$
p_{MD}^{b,r} : \{0,1\}^{< 2^r} \rightarrow \{0,1\}^{b+}
$$  
definiert durch  
$$
p_{MD}^{b,r}(x) = x \,\|\, 1 \,\|\, 0^s \,\|\, (x)_2^r
$$  
heisst **Merkle-Damgård Füllfunktion**.

(||: Konkatenation)

---

Hierbei ist $s \ge 0$ minimal mit  
$$
|x| + 1 + r + s \text{ ein Vielfaches von } b
$$  
und $(x)_2^r$ ist ein $r$-Bit-String, der die Länge von $x$ enthält (gegebenenfalls mit vorangestellten Nullen).


### Beispiel

Die (2,2)-Kompressionsfunktion $f$ sei definiert durch  
$$
f(x_0 x_1 x_2 x_3) = x_0 \oplus x_1 \,\|\, x_1 \oplus x_3,
$$  
wobei $\|$ die Konkatenation (Hintereinanderschreiben) zur besseren Lesbarkeit darstellt.

---

Es sei $u = 10$ und $x = 01\,01\,0$. Berechne:  
$$
h_u^{f, p_{MD}^{2,4}}(x).
$$

---

## Gegeben:

- **Kompressionsfunktion**:  
  $$
  f(x_0 x_1 x_2 x_3) = x_0 \oplus x_1 \,\|\, x_1 \oplus x_3
  $$  
  Diese Funktion verarbeitet **4 Bit auf einmal**: $l = b = 2$ (also je 2 Bit Zustand + 2 Bit Block)
  
- **Eingabe**: $x = 01010$  
- **Initialisierungswert**: $u = 10$  
- **Padding-Funktion**: $p_{MD}^{2,4}$  

---

## Schritt 1: Padding

Die Eingabe $x = 01010$ hat Länge **5**.  
Für Merkle-Damgård-Padding $p_{MD}^{2,4}$ brauchen wir:

- Anhängen von `1`
- Auffüllen mit `0`s (sodass die Länge ein Vielfaches von $b = 2$ ist)
- Dann die Binärdarstellung der ursprünglichen Länge (5 Bit) als 4-Bit-String: $5 = 0101_2$

**Also:**
$$
p_{MD}^{2,4}(01010) = 01010\,1\,0101 = 0101010101
$$

---

## Schritt 2: Iterationsfunktion

Jetzt wird die Iterationsfunktion $\mathit{if}(u, x)$ aufgerufen mit:

- Initialwert $u = 10$
- Padding-Ausgabe $x = 0101010101$

Da die Blockgrösse $b = 2$ ist, teilen wir $x$ in Blöcke zu 2 Bit:

$$
[01], [01], [01], [01], [01]
$$

Dann berechnen wir iterativ:

1. **Start**: $u_0 = 10$

2. **Block 1**: $f(10, 01)$  
   $$
   \Rightarrow f(1001) = 1 \oplus 0 \,\|\, 0 \oplus 1 = 1\,1 \Rightarrow u_1 = 11
   $$

3. **Block 2**: $f(11, 01)$
   $$
   \Rightarrow f(1101) = 1 \oplus 1 \,\|\, 1 \oplus 1 = 0\,0 \Rightarrow u_1 = 00
   $$

4. **Block 3**: $f(00, 01)$
   $$
   \Rightarrow f(0001) = 0 \oplus 0 \,\|\, 0 \oplus 1 = 0\,1 \Rightarrow u_1 = 01
   $$

5. **Block 4**: $f(01, 01)$
    $$
    \Rightarrow f(0101) = 0 \oplus 1 \,\|\, 1 \oplus 1 = 1\,0 \Rightarrow u_1 = 10
    $$

6. **Block 5**: $f(10, 01)$
    $$
    \Rightarrow f(1001) = 1 \oplus 0 \,\|\, 0 \oplus 1 = 1\,1 \Rightarrow u_1 = 11
    $$

**Ergebnis**

$$
   \mathit{i^{f}}(10, 0101010101) = 11 \quad
$$

---


**Beobachtung**

"Kompressionsfunktion ist kollisionsresistent" $ \Rightarrow $ "zugehörige iterierte MD-Hashfunktion ist kollisionsresistent"


Genauer: Man kann aus einer Kollision für die Hashfunktion eine Kollision für die Kompressionsfunktion konstruieren.

Damit muss man sich also nur noch um die Kompressionsfunktion kümmern, und erhält automatisch eine mindestens so sichere Hashfunktion.

Dies ist ein wichtiges Konstruktionsprinzip in der Kryptographie:  

Man baut komplexere Funktionen aus einfachen Bestandteilen zusammen und zeigt, dass die komplexe Funktion sicher ist, **falls die Bausteine sicher sind**.

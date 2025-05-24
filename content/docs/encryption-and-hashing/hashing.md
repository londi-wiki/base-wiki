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


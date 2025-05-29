---
weight: 999
title: "Rainbow Tables"
description: ""
icon: "article"
date: "2025-05-25T14:53:26+02:00"
lastmod: "2025-05-25T14:53:26+02:00"
draft: false
toc: true
katex: true
---

# Einleitung

Rainbow Tables sind eine Methode zur effizienten Umkehrung von kryptographischen Hash-Funktionen. Sie ermöglichen es, Passwörter oder andere Daten, die in Hash-Form gespeichert sind, schnell zu rekonstruieren, indem sie vorberechnete Tabellen verwenden.

Dabei wird nicht viel Speicherplatz benötigt, da die Tabellen nur die Hash-Werte und deren Klartext-Pendants enthalten. Rainbow Tables sind besonders effektiv gegen schwache Passwörter, die häufig verwendet werden.

## Voraussetzung

**Gegeben:**
- Hashfunktion $ h $ und Hashwerte $ h(x_i) $ von Passwörtern $ x_i $

**Gesucht:**

- Möglichst viele Passwörter $ x_i $

# Ansatz: Hellman-Prinzip

- $h(x)$ ist hier deine kryptographische Hash-Funktion (z. B. MD5, SHA1 etc.).
- $R$ ist eine Reduktionsfunktion, die einen Hash-Wert wieder in einen „passwort­ähnlichen“ Klartext umwandelt (z. B. indem sie Bits in erlaubte Zeichenketten übersetzt).

## Schritt 1: Ketten erstellen

Beispielkette:

```
lkwpeter 
  ──h──▶ F3A21 
  ──R──▶ 162haus 
  ──h──▶ DDCA1 
  ──R──▶ aba 
  ──h──▶ DA43F 
  ──R──▶ typ31
```

Nun Speichert man aber nur den Startpunkt `lkwpeter` und den Endpunkt `typ31` in der Tabelle und spart dabei enorm viel Platz anstelle dem Abspeichern aller (Passwort, Hash)-Paare.


## Schritt 2: Hash finden

1. Man hat einen Hash zudem man das Passwort sucht, z. B. `DDCA1`.

2. Nun versucht man diesen Hash in allen möglichen Positionen einer Kette unterzubringen. Zum Beispiel:

    Man nimmt: `DDCA1`, wendet $R$ an und erhält: `aba`

    danach $h$ anwenden und erhält: `DA43F`

    danach wieder $R$ anwenden und erhält `typ31`

3. Nun findet man `typ31` als Endpunkt in der Tabelle. Tada! Das bedeutet, dass die Kette von `lkwpeter` zu `typ31` führt.

4. Jetzt rechnet man die ganze Kette ausgehend von `lkwpeter` noch mal durch, bis man bei `DDCA1` landest – und der Klartext vor diesem Hash ist dann das gesuchte Passwort, hier `162haus`.

Hinweis: Beim Schritt [2] wendet man $h$ und $R$ maximal k-mal an und prüft bei jedem $R$-Schritt ob der Wert einem Endpunkt in der Tabelle entspricht. Somit ist **nicht** garantiert, dass jedes Passwort so gefunden werden kann.

## Problem: Kollision

Ein Problem bei Rainbow Tables ist die Möglichkeit von Kollisionen, d. h. verschiedene Passwörter können den gleichen Hash-Wert erzeugen. Dies kann dazu führen, dass mehrere Passwörter in der Tabelle den gleichen Endpunkt haben, was die Effizienz der Suche verringert. Bei Rainbow-Tables wird deshalb für jede Stufe eine andere Reduktionsfunktion $R_i$ verwendet, um die Kollisionen zu minimieren.

- Statt einer einzigen Reduktionsfunktion R benutzt man für jede Position in der Kette eine eigene Reduktionsfunktion: $R_1, R_1, …, R_k$
- Das verhindert, dass Kollisionen aus unterschiedlichen Kettenteilen gleich zum Verschmelzen aller nachfolgenden Werte führen.
- Beim Knacken muss man dann zwar pro Hash bis zu k-Mal ausprobieren (mit jeweils passender $R_i$), aber im Gegenzug bekommt man eine grössere Abdeckung des Passwortraums mit derselben Tabellen-Grösse.

---

### Vorgehensweise bei gegebenem Hashwert

**Vorgehensweise bei gegebenem Hashwert $\texttt{FAFB3}$**

**Auszug auf der Tabelle:**

$$
\begin{aligned}
123TT &\xrightarrow{h} \texttt{389A3} 
\xrightarrow{R_0} \texttt{pwd11} 
\xrightarrow{h} \texttt{FAFB3} 
\xrightarrow{R_1} \texttt{7qt5} 
\xrightarrow{h} \texttt{76FFF} 
\xrightarrow{R_2} \texttt{treti}
\end{aligned}
$$

**Vorgehen:**

1. **Wende die letzte Reduktionsfunktion $R_2$** auf den Hashwert an:  
   $$
   \texttt{FAFB3} \xrightarrow{R_2} \texttt{hona}
   $$
   → `hona` **kommt nicht als Endwert** in der Tabelle vor.

2. **Wende die vorletzte Reduktionsfunktion $R_1$** auf den Hashwert an, hashe das Resultat und wende $R_2$ an:  
   $$
   \texttt{FAFB3} \xrightarrow{R_1} \texttt{7qt5} \xrightarrow{h} \texttt{76FFF} \xrightarrow{R_2} \texttt{treti}
   $$
   → `treti` **kommt als Endwert** in der Tabelle vor.

3. **Berechne die Kette** ausgehend vom zugehörigen Startwert `123TT`.  
   Wenn **keine Kollisionen in gleichen Stufen auftreten**, kann man das Passwort ablesen.


### Reduktionsfunktion

```text
R(H, Stufe):
    H = H + Stufe
    for i = 1 … L:
        rᵢ = H mod |Z|
        H = H div |Z|
    Gib Z[r_L] … Z[r₁] aus
```

**Beispiel**

- Alphabet $Z = [a, b, c]$, also $|Z| = 3$
- Passwortlänge $L = 2$
- Gegebener Hash $H = 5$

---

**Stufe 0:**

1. $H' = 5 + 0 = 5$

2. **Ziffern:**
   - $r_1 = 5 \bmod 3 = 2 \Rightarrow$ letztes Zeichen `c`
   - $H' = \lfloor 5 / 3 \rfloor = 1$
   - $r_2 = 1 \bmod 3 = 1 \Rightarrow$ erstes Zeichen `b`

3. **Passwort =** `bc`

---

**Stufe 1:**

1. $H' = 5 + 1 = 6$

2. **Ziffern:**
   - $r_1 = 6 \bmod 3 = 0 \Rightarrow$ letztes Zeichen `a`
   - $H' = \lfloor 6 / 3 \rfloor = 2$
   - $r_2 = 2 \bmod 3 = 2 \Rightarrow$ erstes Zeichen `c`

3. **Passwort =** `ca`


**Bemerkung:** 

Die "Stufe" fügt einfach einen kleinen "Shift" zum Hash hinzu, damit jede Ketten-Position eine eigene Reduktions-Version hat. Ohne diesen Shift würden $R_1. R_2, ...$ identisch sein.

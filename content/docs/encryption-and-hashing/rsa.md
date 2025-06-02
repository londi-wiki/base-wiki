---
weight: 999
title: "RSA"
description: ""
icon: "article"
date: "2025-03-20T21:52:53+01:00"
lastmod: "2025-06-02T14:12:53+02:00"
draft: false
toc: true
katex: true
---

## Einleitung

Erfunden von: Ron **R**ivest, Adi **S**hamir Len **A**dleman.

## Aufbau

Formel:

$$
K = \left\{ \left( (n, e), (n, d) \right) : n = p \cdot q \text{ mit Primzahlen } p \ne q, \, e, d \in \mathbb{Z}_{\varphi(n)}^*, \, (e \cdot d) \bmod \varphi(n) = 1 \right\}
$$

Schlüsselraum: 

```
Schlüsselraum: K = {((n,e), (n,d)) : 
    n = p * q mit Primzahlen p != q
    e,d "Elemente von Z-phi(n)-Stern" : (e * d) mod phi(n) = 1 } 
```

**Schlüssel**

Public Key: (n, e)

Private Key: (n, d)

### Verschlüsseln (E)

$ E(x,(n,e)) = x^{e} \bmod n,     (n,e) \in K_{pub}, x \in \mathbb{Z}_{n} $

### Entschlüsseln (E)

$ D(y,(n,d)) = y^{d} \bmod n,     (n,d) \in K_{priv}, y \in \mathbb{Z}_{n} $


## RSA Schlüsselpaar definieren

Vorgehen:

1. Zwei verschiedene Primzahlen $p$ und $q$ wählen.
2. $n = p \cdot q$ berechnen
3. Eulerische phi-Funktion $\varphi(n) = (p -1)(q -1)$ berechnen.
4. $e$ wählen mit $1 < e < \varphi(n)$ so dass $ggt(e, \varphi(n)) = 1$ ist. Sprich: $e \ \text{und} \ \varphi(n)$ sind teilerfremd.
5. Berechne das zu $e$ multiplikativ Inverse $\text{modulo} \ \varphi(n)$, also eine ganze Zahl $d$ mit:

    $(e \cdot d) \mod \varphi(n) = 1$

6. Öffentliches Schlüsselpaar: $(n, e)$, privates Schlüsselpaar: $(n, d)$

### Phi Berechnen

Normalfall:
$$
\varphi(n) = (p - 1)(q - 1)\\
$$

Spezialfall: n ist eine Primzahl:
$$
\varphi(n) = n - 1
$$

Wenn $n = p^k$ eine Primpotenz ist, dann gilt:
$$
\varphi(p^k) = p^k - p^{k-1} = p^{k-1}(p - 1)
$$

Beispiel:
$$
\varphi(7^3) = 7^3 - 7^2 = 343 - 49 = 294
$$


### Beispiel Schlüsselpaar

1. Primzahlen
$$
p = 3\\
q = 11
$$

2. Phi Berechnen
$$
\varphi(n) = (p-1)(q-1) = (3-1)(11-1) = 2 \cdot 10 = 20
$$

3. e definieren
$$
1 < e < \varphi(n) = 20 \\
ggt(e, 20) = 1 (also teilerfremd zu 20)\\
e = 3, 5, 7, 9, ...\\
e = 3, \text{da}\ ggt(3, 20) = 1
$$

4. d definieren
$$
(e \cdot d) \mod \varphi(n) = 1,\ \text{d.h.}\ 3 \cdot d \equiv 1 \pmod{20}\\
\text{=> Erweiterter Euklidischer Algorithmus (EEA) anwenden, siehe unten.}\\
d = 7\\
\text{Prüfung:}\ (3 \cdot 7) \bmod 20 = 1
$$


## Erweiterter Euklidischer Algorithmus (EEA) ggT

Für das Finden des ggT und lieare Diophantische Gleichung: `a * x + b * y = ggT(a, b)`

Beispiel: `7 * d mod 18 = 1`

### Formeln

Folgende Berechnung wird solange durchgeführt bis a' = 1 und b' = 0 sind.
1. **Division**: q = a' / b'
2. **Rest**: r = a' mod b'
3. **Pro Runde**: (x0, y0, x1, y1) = (x1, y1, x0 - qx1, y0 - qy1)

    x0 = x1

    y0 = y1

    x1 = x0 - q*x1

    y1 = y0 - q*y1



### Tabelle
| \(a'\) | \(b'\) | \(x_0\) | \(y_0\) | \(x_1\) | \(y_1\) | \(q\) | \(r\) |
|--------|--------|---------|---------|---------|---------|-------|-------|
| 18     | 7      | 1       | 0       | 0       | 1       | 2     | 4     |
| 7      | 4      | 0       | 1       | 1       | -2      | 1     | 3     |
| 4      | 3      | 1       | -2      | -1      | 3       | 1     | 1     |
| 3      | 1      | -1      | 3       | 2       | -5      | 3     | 0     |
| 1      | 0      | 2       | -5      |         |         |       |       |
| ^      |        | ^       | ^       |         |         |       |       |

```
ggT(18, 7) = 1 = 2 * 18 + (-5) * 7

1 mod 18    = (2 * 18 + (-5) * 7) mod 18, also
       1    = ((-5) * 7) mod 18, also
       1    = (13 * 7) mod 18, also d = 13
       (-5 mod 18 = 13)
```


---
weight: 999
title: "RSA"
description: ""
icon: "article"
date: "2025-03-20T21:52:53+01:00"
lastmod: "2025-03-20T21:52:53+01:00"
draft: false
toc: true
katex: true
---

# Einleitung

Erfunden von: Ron **R**ivest, Adi **S**hamir Len **A**dleman.

# Aufbau

Formel:

$$

K = \left\{ \left( (n, e), (n, d) \right) : 
n = p \cdot q \text{ mit Primzahlen } p \ne q,\ 
e, d \in \mathbb{Z}_{\varphi(n)}^* : 
(e \cdot d) \bmod \varphi(n) = 1
\right\}

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

## Verschlüsseln (E)

$ E(x,(n,e)) = x^{e} \bmod n,     (n,e) \in K_{pub}, x \in \mathbb{Z}_{n} $

## Entschlüsseln (E)

$ D(y,(n,d)) = y^{d} \bmod n,     (n,d) \in K_{priv}, y \in \mathbb{Z}_{n} $


# Erweiterter Euklidischer Algorithmus (EEA) ggT

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


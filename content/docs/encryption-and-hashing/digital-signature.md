---
weight: 999
title: "Digital Signature"
description: ""
icon: "article"
date: "2025-05-27T14:51:30+02:00"
lastmod: "2025-05-27T14:51:30+02:00"
draft: false
toc: true
katex: true
---

# Einleitung

Eine digitale Signatur ist ein kryptografisches Verfahren, das verwendet wird, um die Authentizität und Integrität digitaler Nachrichten oder Dokumente zu gewährleisten. Sie funktioniert ähnlich wie eine handschriftliche Unterschrift, bietet jedoch ein höheres Mass an Sicherheit und Nachweisbarkeit.

# Prinzip

## Signierschema – Übersicht

Ein **Signierschema** ist ein Tupel

$$
S = (X, Y, G, K, T, V)
$$

---

### Bestandteile

- $K$: Menge von Schlüsselpaaren $(k, \hat{k})$
  - $k$: **Verifikationsschlüssel**
  - $\hat{k}$: **Signaturschlüssel**
  - $K_{pub}$: öffentliche Schlüssel
  - $K_{priv}$: private Schlüssel

- $G$: effizienter, probabilistischer **Schlüsselgenerierungsalgorithmus**  
  $$G \to K$$

- $X = (X_k)_{k \in K_{pub}}$: Familie von **Nachrichtenräumen**

- $Y = (Y_k)_{k \in K_{pub}}$: Familie von **Signaturräumen**

- $T$: effizienter, probabilistischer **Signieralgorithmus**  
  $$
  T: \\ 
  Eingabe: \hat{k} \in K_{priv} \ und \ x \in X_k \\
  Ausgabe: y \in Y_k \\
  $$

- $V$: effizienter, deterministischer **Verifikationsalgorithmus**  
  $$
  V: \\ 
  Eingabe: k \in K_{pub},\ x \in X_k \ und \ y \in Y_k \\
  $$

---

### Korrektheitsbedingung

Für alle $(k, \hat{k}) \in K$, $x \in X_k$ gilt:

$$
V(x, T(x, \hat{k}), k) = 1
$$

---

### ✒️ Signieren (Signing)

Der Signieralgorithmus $T$ nimmt als Eingabe:

- die Nachricht $x$
- den privaten Schlüssel $\hat{k}$

und liefert eine Signatur $y = T(x, \hat{k})$.

> T ist oft **probabilistisch**, d.h. es wird Zufall eingebracht, um **unterschiedliche Signaturen** für gleiche Nachrichten zu erzeugen.

---

### Verifizieren (Verification)

Der Verifikationsalgorithmus $V$ erhält:

- die Nachricht $x$
- die Signatur $y$
- den öffentlichen Schlüssel $k$

und gibt zurück:

$$
\begin{cases}
1 & \text{falls gültig (Valid)} \\
0 & \text{sonst (Invalid)}
\end{cases}
$$

---

### Gültigkeit

Ein Paar $(x, s)$ heißt **gültiges Nachrichten-Signatur-Paar** (bzgl. $k$), wenn

$$
V(x, s, k) = 1
$$

Dann heißt $s$ eine **gültige Signatur zu $x$** (bzgl. $k$).

---

### Sicherheitsanforderung (informell)

Ohne Kenntnis des privaten Schlüssels $\hat{k}$ zu einem öffentlichen Schlüssel $k$ soll es (fast) unmöglich sein,

- für eine **neue Nachricht** $x$ (ohne gültige Signatur)
- eine **gültige Signatur** $s$ zu erzeugen.

Selbst wenn man zu vielen anderen Nachrichten gültige Signaturen kennt!

# Angriff auf naives RSA-Signaturschema

Das Problem des naiven Schemas lässt sich sehr schön daran zeigen, dass sich mit Kenntnis des öffentlichen Schlüssels $\text{(n,e)}$ ganz ohne $\text{d}$ gültige (Nachricht, Signatur)-Paare erzeugen lassen.

## 1. Schemaübersicht

- **Signieren**  
  $$ \text{T(x, (n,d))} = s = x^d \bmod n, $$

  wobei $$x \in \mathbb{Z}_n\ $$ die Nachricht ist.

- **Verifizieren**  
  $$
  V(x, s, (n,e)) =
  \begin{cases}
    1, & \text{falls } s^e \bmod n = x, \\
    0, & \text{sonst.}
  \end{cases}
  $$

---

## 2. Angriffsidee

Anstatt $x$ vorzugeben und $s = x^d$ zu berechnen, wählt der Angreifer beliebig ein $s \in \mathbb{Z}_n$ und berechnet

$$
x = s^e \bmod n.
$$

Dann gilt:

$$
s^e \bmod n = x
\quad\Longrightarrow\quad
V(x, s, (n,e)) = 1,
$$

also ist $(x, s)$ ein gültiges Nachrichten-Signatur-Paar, ganz ohne Kenntnis von $d$.

---

## 3. Numerisches Beispiel

1. **Schlüsseldaten**  
   $$
   p = 5,\quad q = 11
   \quad\Longrightarrow\quad
   n = p \cdot q = 55,\quad 
   \varphi(n) = (p-1)(q-1) = 4 \cdot 10 = 40.
   $$  
   Wähle $e = 3$. Dann berechnet man $d$ aus
   $$
     3 \cdot d \equiv 1 \pmod{40},
   $$
   also $d = 27 \quad (3*27 \mod{40} = 1)$.

2. **Angreifer wählt** $s = 2$
   $$
   x = 2^e \bmod 55 = 2^3 \bmod 55 = 8.
   $$

3. **Gültigkeit prüfen**  
   $$
   2^e \bmod 55 = 8 = x
   \quad\Longrightarrow\quad
   V(x=8,\,s=2,\,(n,e)) = 1.
   $$

   Damit ist $(8,2)$ ein gültiges (Nachricht, Signatur)-Paar, obwohl $d$ unbekannt bleibt.

---

## 4. Fazit

Das naive „Umkehren“ von RSA als Signaturschema ist **unsicher**, 
da sich mit dem öffentlichen Schlüssel $(n,e)$ beliebige Signaturen erzeugen lassen.  
Für echte Unforgeability benötigt man zusätzliche Maßnahmen wie  
- Hash-Funktionen,  
- sichere Padding-Schemata (z. B. RSA-PSS).  

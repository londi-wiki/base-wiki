---
weight: 999
title: "Mehrstufige Zufallsexperimente"
description: ""
icon: "article"
date: "2023-10-16T14:56:56+02:00"
lastmod: "2023-10-16T14:56:56+02:00"
draft: false
toc: true
katex: true
---

## Beispiel - ohne Zurücklegen

Gegeben ist ein Topf mit 4 weissen und 2 schwarzen Kugeln. Wir ziehen 3 Mal **ohne** Zurücklegen.

Modellierung: $\Omega$ = {w,s} x {w,s} x {w,s}

```mermaid
graph TB
    A((Start)) -- 4/6 --> B((w))
    A -- 2/6 --> C((s))
    
    B -- 3/5 --> D((w))
    B -- 2/5 --> E((s))
    
    C -- 4/5 --> F((w))
    C -- 1/5 --> G((s))
    
    D -- 2/4 --> H((w))
    D -- 2/4 --> I((s))
    E -- 3/4 --> J((w))
    E -- 1/4 --> K((s))

    F -- 3/4 --> L((w))
    F -- 1/4 --> M((s))
    G -- 4/4 --> N((w))
    G -- 0/4 --> O((s))
```

a) Was ist die Wahrscheinlichkeit für A: "Dritte Kugel weiss"?

Teilmenge von $\Omega$ ist A = {(w,w,w), (w,s,w), (s,w,w), (s,s,w)}

P(A) = f(w,w,w) + f(w,s,w) + f(s,w,w) + f(s,s,w)

$
P(A) = \frac{4}{6} * \frac{3}{5} * \frac{2}{4} + \frac{4}{6} * \frac{2}{5} * \frac{3}{4} + \frac{2}{6} * \frac{4}{5} * \frac{3}{4} + \frac{2}{6} * \frac{1}{5} * \frac{4}{4}
$

## Beispiel - mit Zurücklegen

Gegeben ist ein Topf mit 3 roten und 4 grünen Kugeln. Wir ziehen 2 Mal **mit** Zurücklegen.

Modellierung: $\Omega$ = {w,s} x {w,s} x {w,s}

```mermaid
graph TB
    A((Start)) -- 3/7 --> B((r))
    A -- 4/7 --> C((g))
    
    B -- 3/7 --> D((r))
    B -- 4/7 --> E((g))
    
    C -- 3/7 --> F((r))
    C -- 4/7 --> G((g))
```

Ereignis A: "Erste Kugel rot"

A = {(r,r), (r,g)}

Ereignis B: "Zweite Kugel rot"

A = {(r,r), (g,r)}

$
P(A \cap B) = P(\\{ (r,r) \\}) = \frac{3}{7} * \frac{3}{7}
$

$
P(A) * P(B) = (\frac{3}{7} * \frac{3}{7} + \frac{3}{7} * \frac{4}{7}) * (\frac{3}{7} * \frac{3}{7} + \frac{4}{7} * \frac{3}{7}) = \frac{3}{7} * \frac{3}{7}
$
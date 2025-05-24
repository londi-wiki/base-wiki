---
weight: 999
title: "Mod Calculation"
description: ""
icon: "article"
date: "2025-03-23T11:33:14+01:00"
lastmod: "2025-05-24T11:33:14+01:00"
draft: false
toc: true
katex: true
---

# Allgemein

$ 25 \bmod 11 = 3 $

$ -4 \bmod 11 = -4 + 11 = 7 $


# Schnelle Exponentiation

Der Modus einer grossen Zahl wie die der folgenden kann in mehreren Schritten berechnet werden: 

Ziel: $ (5^{2) ^{ 2 } } \bmod 11 $ 

1. Schritt: mod von $ (5^{2}) $ berechnen

$ 5^{ 2 } \bmod 11 = 25 \bmod 11 = 3 $

2. Schritt: Mod von "3" mit dem übrig gebliebenen Exponent $ (^{2}) $ berechnen 

$ 3^{ 2 } \bmod 11 = 9 $

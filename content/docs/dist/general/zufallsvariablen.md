---
weight: 999
title: "Zufallsvariablen"
description: ""
icon: "article"
date: "2023-10-16T15:28:26+02:00"
lastmod: "2023-10-16T15:28:26+02:00"
draft: false
toc: true
katex: true
---

## Allgemeine Definition

Eine Zufallsvariable ist eine normale mathematische Funktion. 
Da bei jeder Durchführung des Zufallsexperimentes ein zufälliges Ergebnis $\omega$ eintritt, 
ist auch der zugehörige Wert $X(\omega)$ nicht vorhersagbar.


$P^{X}$ heisst Verteilung von X oder Bildmass von X unter P.

## Beispiel

Gegeben: Zweimaliges Würfeln: Man gewinnt i Franken bei Augensumme i.

Gesucht: Wahrscheinlichkeit für "Gewinn ist k"

Modellierung als Kopllung zweier Laplace-Experimente (faire Würfel).

$\Omega$ = {1,2,3,4,5,6} x {1,2,3,4,5,6} fp(i,j) = $\frac{1}{6} * \frac{1}{6}$

Gesucht ist die Verteilung von X: X(i,j) = i + j

Es gilt etwa P(X = 6) = P({(i,j) | i + j = 6}) = P({(1,5),(2,4),(3,3),(4,2),(5,1)}) = $\frac{5}{36}$

## Zähldicht

Die Zähldichte einer diskreten Zufallszahl bestimmt die Verteilung eindeutig, oft wird diese in einer Tabelle oder mithilfe eines Stabdiagramms dargestellt.

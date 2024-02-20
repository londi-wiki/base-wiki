---
title : 'Laplace Experiment'
date : 2023-09-25T17:23:44+02:00
tags: ["draft"]
author: "Leon"
katex: true
draft: true
---

## Laplace [^1] Experiment

#Symmetrie-Annahme

[^1]: Pierre-Simon Laplace (1749 - 1827)

Ein Laplace Experiment ist ein Zufallsexperiment mit n verschiedenen möglichen Ergebnissen,
die alle dieselbe Wahrscheinlichkeit, also 1/n haben.

Die Wahrscheinlichkeit eines Ereignisses E $\subseteq$ $\Omega$ wird für diesen Fall folgendermassen definiert:

$ P(E) = \frac{|E|}{|\Omega|} = \frac{ \text{Anzahl guenstige Ergebnisse} }{ \text{Anzahl aller Ergebnisse} } $

Dieses mathematische Modell für ein Laplace-Experiment, bestehend aus der Menge $\Omega$ mit der Funktion P, nennt man einen Laplace-Raum.

Dieses P heisst auch **Gleichverteilung**.

Beispiel: Würfelwurf

> Ergebnismenge: $\Omega$ = { 1,2,3,4,5,6 }
>
> Wie gross ist die Wahrscheinlichkeit für eine Augenzahl grösser als 4? E = { 5,6 }

Ansatz: Jede Augenzahl tritt mit der Wahrscheinlichkeit $\frac{1}{n}$ auf.
Damit die Aussage wahr ist, muss die Augenzahl 5 oder 6 betragen.
Das wären zusammen $\frac{2}{n}$, also $\frac{1}{3}$ sprich $\approx$ 33.33%.

1. Modellannahme
   Es scheint sinnvoll, dieses Experiment als Laplace-Experiment zu modellieren.

Im Laplace-Raum sind für Mengen M die Anzahl der Elemente, |M|, zu bestimmen.

Die **Kombinatorik** liefert systematische Abzählverfahren.

Die Kombinatorik basiert auf sehr wenigen einfachen Regeln, die aber in Kombination beliebig komplex werden können.


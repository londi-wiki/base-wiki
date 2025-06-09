---
weight: 999
title: "System Evolution"
description: ""
icon: "article"
date: "2024-10-22T13:54:41+02:00"
lastmod: "2024-10-22T13:54:41+02:00"
draft: false
toc: true
---

# System Evolution

![system-evolution](https://wiki.strubli.com/images/system-evolution.png)

Quelle: Stephan Murer et al empirisch

Das Schaubild stellt die Beziehung zwischen Agilität (y-Achse) und Funktionalität (x-Achse) eines Systems dar.

**Agilität:** Die Fähigkeit des Systems,
schnell und effizient auf Veränderungen zu reagieren.
Eine höhere Agilität bedeutet, dass das System flexibler
auf neue Anforderungen oder Umstellungen reagieren kann.

**Funktionalität:** Die Gesamtheit der Funktionen und Fähigkeiten,
die ein System bietet, also die Funktionalität,
die das System für die Nutzer bereitstellt.

**Bedeutung der Pfeile:**
Die Pfeile im Diagramm zeigen den Verlust der Agilität mit
zunehmender Funktionalität des Systems.
Je mehr Funktionalität ein System hinzufügt,
desto weniger agil wird es. Es gibt zwei kritische Punkte im Diagramm:
- C1: Dieser Punkt stellt den Moment dar, in dem der Verlust an Agilität etwa das Fünffache des funktionalen Zugewinns beträgt. Das bedeutet, dass ab diesem Punkt jede Erhöhung der Funktionalität den Verlust an Agilität stark überwiegt.
- C2: Hier wird der Verlust an Agilität so gross, dass der Zugewinn an Funktionalität kaum noch einen positiven Effekt hat. Mit anderen Worten: Jede weitere funktionale Verbesserung macht das System so unflexibel, dass der zusätzliche Nutzen marginal wird.

## Problematik, die Murer et al entdeckt haben:

Murer et al. entdeckten in ihrer empirischen Forschung,
dass viele Softwaresysteme im Laufe ihrer Entwicklung
immer mehr Funktionalität hinzugewinnen,
was jedoch zu einem erheblichen Verlust der Agilität führt.
Dies führt dazu, dass das System weniger anpassungsfähig wird und
zukünftige Änderungen immer aufwendiger und kostspieliger werden.
Ab einem gewissen Punkt (C2) sind die Funktionsgewinne durch das System zu teuer,
weil die Verluste in der Agilität überwiegen.

## Mögliche Massnahmen:

**Kontinuierliche Refaktorierung:** Systeme sollten regelmässig umstrukturiert und optimiert werden,
um ihre Flexibilität zu bewahren. Durch Refaktorierung können unnötige Komplexitäten beseitigt und
die Agilität erhöht werden.

**Modularisierung:** Systeme sollten in kleinere, unabhängige Module zerlegt werden.
Dies ermöglicht es, einzelne Module zu verändern oder zu erweitern,
ohne das gesamte System zu beeinflussen. So bleibt die Gesamtarchitektur flexibel und agil.

**Managed Evolution:** Dies bedeutet, dass Systeme nicht nur nach funktionalen Anforderungen
erweitert werden sollten, sondern dass auch die langfristige Wartbarkeit und Agilität beachtet
werden muss. Änderungen sollten mit Blick auf die zukünftige Entwicklung vorgenommen werden,
um das System anpassungsfähig zu halten.

**Technische Schulden minimieren:** Technische Schulden entstehen, wenn schnelle und unsaubere
Lösungen implementiert werden, um kurzfristige funktionale Anforderungen zu erfüllen.
Murer et al. schlagen vor, technische Schulden frühzeitig anzugehen,
um langfristige Probleme zu vermeiden und die Agilität des Systems zu sichern.

**Starke Governance:** Es sollte eine klare Governance-Struktur geben, die sicherstellt,
dass Entscheidungen zur Erweiterung der Funktionalität immer auch die Auswirkungen
auf die Agilität berücksichtigen.

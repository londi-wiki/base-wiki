---
title : 'Application and Evaluation'
date : 2023-09-08T21:28:01+02:00
tags: ["week1"]
author: "Leon"
---

### Function application / evaluation

Equational reasoning => Gleiches mit Gleichem ersetzen

![equationalreasoning](/fprog/images/equationalreasoning.png)

![equationalreasoning2](/fprog/images/equationalreasoning2.png)

Haskell is a lazy functional language and uses the so-called "call by need" principle.
That means that a sub expression will only be once calculated.

> Wenn die "by value" Strategie terminiert, dann wird die "by name" das selbe Resultat liefern.

### Order

The execution order doesn't matter because they do not rely on each other.
They could be also evaluated parallel.
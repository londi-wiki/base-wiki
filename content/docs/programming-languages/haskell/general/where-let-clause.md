---
weight: 999
title: "Where and let Clause"
description: ""
icon: "article"
date: "2023-10-08T16:32:19+02:00"
lastmod: "2023-10-08T16:32:19+02:00"
draft: false
toc: true
---

[Where vs. let bindings](https://wiki.haskell.org/Let_vs._Where)

## Where

```haskell
cylinder :: Float -> Float -> Float
cylinder r h = 2 * topArea + sideArea
    where sideArea = 2*pi*r*h
          topArea = pi*r^2
```

## Let

```haskell
cylinder :: Float -> Float -> Float
cylinder r h =
    let sideArea = 2*pi*r*h
          topArea = pi*r^2
    in 2 * topArea + sideArea
```

---
weight: 999
title: "WS Pattern Matching"
description: ""
icon: "article"
date: "2023-10-08T15:29:17+02:00"
lastmod: "2023-10-08T15:29:17+02:00"
draft: false
toc: true
---

## WS Pattern Matching

```haskell
Aufgabe 1

> switchFirstTwo :: [a] -> [a]
> switchFirstTwo [] = []
> switchFirstTwo [a] = [a] -- switchFirstTwo' (a:[]) = [a]
> switchFirstTwo (a:b:s) = b:a:s

Aufgabe 2a

> type Vec = (Int, Int)
> addVec :: Vec -> Vec -> Vec
> addVec (a, b) (x, y) = (a + x, b + y)

Aufgabe 2b

> addOpt :: Int -> Int -> Int
> addOpt x 0 = x
> addOpt 0 y = y
> addOpt x y = x + y

> addVecOpt :: Vec -> Vec -> Vec
> addVecOpt (a, b) (x, y) = (addOpt a x, addOpt b y)
```

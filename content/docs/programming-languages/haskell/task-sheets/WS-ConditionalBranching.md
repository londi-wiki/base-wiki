---
weight: 999
title: "WS ConditionalBranching"
description: ""
icon: "article"
date: "2023-10-08T16:19:09+02:00"
lastmod: "2023-10-08T16:19:09+02:00"
draft: false
toc: true
---

```haskell
Aufgabe a

> max_guard :: Int -> Int -> Int
> max_guard a b | a > b = a
>               | otherwise = b

Aufgabe b

> max_if :: Int -> Int -> Int
> max_if a b = if a > b then a else b

Aufgabe c

> max_case :: Int -> Int -> Int
> max_case a b = case a > b of
>                  True -> a
>                  False -> b

Aufgabe d

Geht nicht (also keine saubere Lösung)

```
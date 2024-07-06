---
weight: 999
title: "Custom Operators"
description: ""
icon: "article"
date: "2023-10-09T15:22:58+02:00"
lastmod: "2023-10-09T15:22:58+02:00"
draft: false
toc: true
---

## Custom operators and bindings

```haskell
:i (+) ~> infixl 6 +
:i (*) ~> infixl 7 *
```

```haskell
(|+|) :: Int -> Int -> Int
a |+| b = abs a + abs b
infixl 6 |+|
```

| Operator                         | Präzedenz |
|----------------------------------|-----------|
| ((f a) b) infixl                 | 10        |
| (.) infixr                       | 9         |
| (^) infixr                       | 8         |
| (*), (/) infixl                  | 7         |
| (+), (-) infixl                  | 6         |
| (++), (:) infixr                 | 5         |
| (==), (/=), (<), (<=), ... infix | 4         |
| (&&) infixr                      | 3         |
| (\|\|) infixr                    | 2         |
|                                  | 1         |
|                                  | 0         |


```haskell
-- a
1 + 2 ^ 3 == 6 && 3 / 4 < 12 || snd (1, True)

(((1 + (2 ^ 3)) == 6) && ((3 / 4) < 12)) || (snd (1, True))
```
---
title : 'Tuples'
date : 2023-09-24T17:06:33+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Aggregated Types - Tuples

### Simple tuple

```haskell
> (False, 8, "Hello") :: (Bool, Int, String)
(False,8,"Hello")
it :: (Bool, Int, String)

> (True, False, 'c', 8)
(True,False,'c',8)
it :: Num d => (Bool, Bool, Char, d)
```

### Components

```haskell
> ((True, 'a'), (False, 8, "Hello"))
((True,'a'),(False,8,"Hello"))
it :: Num b => ((Bool, Char), (Bool, b, [Char]))
```

## Accessing components - Pattern matching

```haskell
fstInt :: (Int, Int) -> Int
fstInt (x,y) = x
fstInt :: (Int, Int) -> Int

> fstInt (1, 8)
1
it :: Int


nested :: (Int, (Int, Int)) -> Int
nested (x,(y, z)) = y
fstInt :: (Int, (Int, Int)) -> Int

> nested (2, 4, 8)
4
it :: Int
```

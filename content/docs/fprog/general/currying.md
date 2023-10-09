---
weight: 999
title: "Currying"
description: ""
icon: "article"
date: "2023-10-08T17:21:32+02:00"
lastmod: "2023-10-08T17:21:32+02:00"
draft: false
toc: true
---

```haskell

Aufgabe curry

> add :: Int -> Int -> Int
> add a b = a + b

> add' :: (Int,Int) -> Int
> add' (a,b) = a + b


> curry' :: ((a,b) -> c) -> (a -> b -> c)
> curry' f = \x -> \y -> f (x, y)

:t curry' add' ~> curry' add' :: Int -> Int -> Int
curry' add' 5 8 ~> 13


> uncurry' :: (a -> b -> c) -> ((a,b) -> c)
> uncurry' f = \(x,y) -> f x y

:t uncurry' add ~> uncurry' add :: (Int, Int) -> Int
uncurry' add (1,2) ~> 3


Aufgabe flip

:t replicate ~> replicate :: Int -> a -> [a]

> flip' :: (a -> b -> c) -> (b -> a -> c)
> flip' f = \b a -> f a b

Alternativ: flip' f a b = f b a


Aufgabe 4a

> f :: Int -> Int
> f a = a

> g :: Int -> Bool
> g a = True

> h :: a -> Int
> h a = 0

> i :: Bool -> (Int,Int)
> i True = (0,0)

> a1 = f.f :: Int -> Int
> a2 = g.f :: Int -> Bool
> a3 = h.f :: Int -> Int

> a4 = f.h :: a -> Int
> a5 = g.h :: a -> Bool

> a6 = i.g :: Int -> (Int,Int)

> a7 = h.i :: Bool -> Int
> a8 = h.g :: Int -> Int
> a9 = h.h :: a -> Int


Aufgabe 4b

fst :: (a,b) -> a
snd :: (a,b) -> b

> b1 = f.fst.i :: Bool -> Int
> b2 = f.snd.i :: Bool -> Int
```
@fhnw










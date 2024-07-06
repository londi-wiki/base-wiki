---
weight: 999
title: "Recursion"
description: ""
icon: "article"
date: "2023-10-15T12:03:49+02:00"
lastmod: "2023-10-15T12:03:49+02:00"
draft: false
toc: true
---

## Example

```haskell
factorial :: Integer -> Integer
factorial 0 = 1
factorial n = n * factorial (n-1)
```

## Example 2

```haskell
Aufgabe 2

> countDown :: Int -> [Int]
> countDown 0 = [0]
> countDown n = [n] ++ countDown (n-1)

countDown 10
[10,9,8,7,6,5,4,3,2,1,0]


Aufgabe 3

> countUp :: Int -> [Int]
> countUp 0 = [0]
> countUp n = countUp (n-1) ++ [n]

countUp 10
[0,1,2,3,4,5,6,7,8,9,10]


Aufgabe 4

> countDownUp :: Int -> [Int]
> countDownUp 0 = [0]
> countDownUp n = [n] ++ countDownUp (n-1) ++ [n]

countDownUp 10
[10,9,8,7,6,5,4,3,2,1,0,1,2,3,4,5,6,7,8,9,10]
```

## Tail Recursion

### Normal recursion

```haskell
> mySum1 :: Num a => [a] -> a
> mySum1 [] = 0
> mySum1 (i:is) = i + sum is
```

> ~> 1 + sum([2,3])
> 
> ~> 1 + (2 + sum([3]))
> 
> ~> 1 + (2 + (3 + sum([])))
> 
> ~> 1 + (2 + (3 + 0))
> 
> ~> 6


### tail recursion

```haskell
> mySum2 :: Num a => [a] -> a
> mySum2 l = sum' 0 l
>   where sum' acc [] = acc
>         sum' acc (i:is) = sum' (i+acc) is
```

> ~> sum' 0 [1,2,3]
> 
> ~> sum' (1+0) [2,3] => sum' (1) [2,3]
> 
> ~> sum' (2+1) [3] => sum' (3) [3]
> 
> ~> sum' (3+3) [] => sum' (6) []
> 
> ~> 6


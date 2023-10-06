---
title : 'Deriving'
date : 2023-09-24T18:35:26+02:00
tags: ["draft"]
author: "Leon"
math: false
---

### Deriving Examples

```haskell
> data Person = Person {name :: String, age :: Int } deriving (Show)
> me = Person "Leon" 99
me :: Person

> me
Person {name = "Leon", age = 99}


> data Coord = Coord {x :: Int, y :: Int} deriving (Show, Eq)
> here = Coord 4 8
> here2 = Coord 4 16

> here == here2
False
it :: Bool
```



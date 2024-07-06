---
title : 'Type Synonyms'
date : 2023-09-24T17:34:57+02:00
tags: ["draft"]
author: "Leon"
math: false
---

```haskell
type Coord = (Int, Int) -- this does not create a new type, only a new name
```

> Type synonyms do not prevent the usage of wrong types. e.g.:

```haskell
xCoord :: Coord -> Int
xCoord (x, y) -> x

time :: (Int, Int)
time = (23, 59)

> xCoord time -- compiles
23
```
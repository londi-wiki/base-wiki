---
title : 'Polymorphic Types'
date : 2023-09-24T17:26:30+02:00
tags: ["draft"]
author: "Leon"
math: false
---

The definition `fstInt (False, 'c')` with the type declaration `fstInt (Int, Int) -> Int` strictly expects Ints as inout and output.

A generic way would look like this. 

```haskell
fst :: (a, b) -> a
fst (x, y) = x

> fst (1,2)
1
it :: Num a => a

> fst (1,2) :: Int
1
it :: Int

> fst (True, 'c')
True
it :: Bool

> fst (("Hello", True), 'c')
("Hello",True)
it :: ([Char], Bool)
```


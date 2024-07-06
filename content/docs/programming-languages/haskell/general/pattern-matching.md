---
weight: 999
title: "Pattern Matching"
description: ""
icon: "article"
date: "2023-10-08T15:22:49+02:00"
lastmod: "2023-10-08T15:22:49+02:00"
draft: false
toc: true
---

## Pattern Matching - Constants

Importing: The pattern with 'n' must be at the end of all pattern matching variants.

```haskell
sayNumber :: Int -> String -> String
sayNumber 0 s = "No " ++ s
sayNumber 1 s = "one " ++ s
sayNumber 2 s = "two " ++ s
sayNumber n s = "many " ++ s
```

### Wildcard

```haskell
pwTester :: String -> Bool
pwTester "banana" = True
pwTester _ = False
```

## Pattern Matching - Lists

```haskell
listChecker :: [a] -> String
listChecker [] = "empty list"
listChecker (x:[]) = "one element"
listChecker (x:y:[]) = "two elements"
listChecker _ = "long list"

listFoo :: [a] -> [a]
listFoo [] = []
listFoo (a:as) = as ++ [a]

listToElement :: [Int] -> Int
listToElement [1,2,3] = 1+2+3
listToElement [4,x,7] = 4+x*7
listToElement [] = 0
listToElement z = -1
```

## Pattern Matching - Tuples

```haskell
switchNonZero :: (Int, Int) -> (Int, Int)
switchNonZero (0, y) = (0, y)
switchNonZero (x, 0) = (x, 0)
switchNonZero (x, y) = (y, x)

bar :: (Integer, String) -> String
bar (0, "hello") = "world"
bar (0, x) = x
bar (x, "foo") = "bar"
bar (x, y) = "who cares?"
```

## guards

```haskell
abs :: (Num a, Ord a) => a -> a
abs n
    | n < 0 = -n
    | otherwise = n
      
-- otherwise = True
```






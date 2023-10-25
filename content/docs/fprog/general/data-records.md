---
weight: 999
title: "Data Records"
description: ""
icon: "article"
date: "2023-10-25T21:29:54+02:00"
lastmod: "2023-10-25T21:29:54+02:00"
draft: false
toc: true
---

## Basic example

```haskell
data PersonType = Person {
  firstName :: String,
  lastName :: String,
  age :: Int
} deriving (Show)

-- sepp = Person "Sepp" "Oben" 42
-- sepp :: PersonType
-- firstName sepp
-- "Sepp"
-- it :: String

-- susi = Person {firstName = "Susi", lastName = "Flora", age = 42}
-- susi :: PersonType
-- susi
-- Person {firstName = "Susi", lastName = "Flora", age = 42}
-- it :: PersonType
```

## Polymorphic Data Types

```haskell
safeHead :: [a] -> Maybe a
safeHead [] = Nothing
safeHead a = Just (head a)

-- safeHead [1,2,3]
-- Just 1
-- it :: Num a => Maybe a
-- safeHead []
-- Nothing
-- it :: Maybe a

safeTail :: [a] -> Maybe [a]
safeTail [] = Nothing
safeTail a = Just (tail a)

safeMax :: (Ord a) => [a] -> Maybe a
safeMax [] = Nothing
safeMax [x] = Just x
safeMax (x:y:xs) | x > y = safeMax (x:xs)
                 | otherwise = safeMax (y:xs)
```

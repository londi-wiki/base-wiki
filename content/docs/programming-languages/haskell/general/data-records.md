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

### Example 1
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

### Example 2

```haskell
data PairType a b = PairData a b

-- Already defined in Data.Either
-- data Either a b = Left a | Right b

safeHead :: [a] -> Either String a -- Type of Left var is String, Type of Right var is a
safeHead [] = Left "Head on empty String"
safeHead (x:xs) = Right x

-- safeHead [1,2,3]
-- Right 1
-- it :: Num a => Either String a

-- safeHead []
-- Left "Head on empty String"
-- it :: Either String a
```

### Example 3

```haskell
data FS = Folder String [FS] | File String deriving Show

fs = Folder "tmp" [
    Folder "bla" [
      File "a.txt"],
    File "b.txt"
  ]
  
allFiles :: FS -> [FS]
allFiles (File n) = [File n]
allFiles (Folder _ fs) = concat (map allFiles fs)
```

## Define a list data type

```haskell
data List e = Empty | Cons e (List e)

-- l = Cons 'a' (Cons 'b' (Cons 'c' Empty))
-- :t Cons 'a' (Cons 'b' (Cons 'c' Empty))
-- Cons 'a' (Cons 'b' (Cons 'c' Empty)) :: List Char

listSize :: List a -> Int
listSize Empty = 0
listSize (Cons _ t) = 1 + listSize t

-- listSize l
-- 3
```

## Recursive Natual Numbers

```haskell
data Nat = Z | S Nat deriving Show

-- drei = S (S (S Z))
-- drei :: Nat

add :: Nat -> Nat -> Nat
add Z n = n
add (S m) n = S (add m n)

-- add drei (S Z)
-- S (S (S (S Z)))

mul :: Nat -> Nat -> Nat
mul Z n = n
mul (S m) n = add n (mul m n)

-- mul drei (S Z)
-- S (S (S (S Z)))

toNat :: Int -> Nat
toNat 0 = Z
toNat n = S (toNat (n-1))

toInt :: Nat -> Int
toInt Z = 0
toInt (S n) = 1 + toInt n
```

## Combined expressions

```haskell
ex3 = ((Const 0) `Add` (Const 2)) `Mul` (Const 3)

> simpl :: Expr -> Expr
> simpl (Add (Const 0) (Const a)) = Const a
> simpl (Add (Const a) (Const 0)) = Const a
> simpl (Mul (Const 1) (Const a)) = Const a
> simpl (Mul (Const 0) (Const a)) = Const 0
> simpl (Mul (Const a) (Const 1)) = Const a
> simpl (Mul (Const a) (Const 0)) = Const 0
> simpl (Add e1 e2) = Add (simpl e1) (simpl e2)
> simpl (Mul e1 e2) = Mul (simpl e1) (simpl e2)
> simpl e = e

simpl ex3
Mul (Const 2) (Const 3)
```
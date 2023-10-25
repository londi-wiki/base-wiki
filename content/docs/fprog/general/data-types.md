---
weight: 999
title: "Data Types"
description: ""
icon: "article"
date: "2023-10-24T22:37:45+02:00"
lastmod: "2023-10-24T22:37:45+02:00"
draft: false
toc: true
---

## Simple Example

```haskell
data BookInfo = Book Int String deriving (Show)

:t Book
Book :: Int -> String -> BookInfo

b = Book 1234 "Banana"
b :: BookInfo

b
Book 1234 "Banana"
it :: BookInfo

-- ohne deriving show wuerde der Aufruf "b" einen Fehler produzieren.

isbn :: BookInfo -> Int
isbn (Book isbnnr _) = isbnnr

isbn b
1234
it :: Int
```

## Multiple constructors

```haskell
data BillingInfo = CreditCard Float String String
                  | Invoice Float Int
                   deriving (Show)

cc = CreditCard 123.20 "ABC123" "Sepp"
cc = Invoice 123.20 S123"

anount :: BillingInfo -> Float
amount (CreditCard a _ _) = a
amount (Invoice a _) = a
```
> Data constructors must begin with a capital letter.


## Use datatype in other datatypes

```haskell
data Shape = Circle Float
            | Square Float Float
            deriving (Show)

circumference :: Shape -> Float
circumference (Circle r) = r**2 * pi
circumference (Square w h) = w * h

f = Fig (XY 2 3) (Square 2 4)
f :: Figure
f
Fig (XY 2.0 3.0) (Square 2.0 4.0)
it :: Figure

-- other example

move :: Figure -> Float -> Float -> Figure
move (Fig (XY x y) (s)) nx ny = Fig (XY (x+nx) (y+ny)) s

f = Fig (XY 2 3) (Square 2 4)
f :: Figure
f
Fig (XY 2.0 3.0) (Square 2.0 4.0)
it :: Figure
move f 2 4
Fig (XY 4.0 7.0) (Square 2.0 4.0)
it :: Figure
```
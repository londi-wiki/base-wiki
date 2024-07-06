---
title : 'Week2'
date : 2023-09-19T18:56:12+02:00
tags: ["week2"]
author: "Leon"
---

```haskell
Übung 2 Typen
--------------

In dieser Übung geht es darum einfache Programmieraufgaben mit verschiedenen Basistypen von Haskell zu lösen. 

1. Basis Typen

a) Implementieren Sie folgende Funktion, die nur dann True zurückgibt, falls alle drei Argumente gleich sind. 

> threeEquals :: Int -> Int -> Int -> Bool
> threeEquals a b c = (a == b) && (b == c)

-- threeEquals 2 2 2

b) Nun geht es um die Funktion

> fourEquals :: Int -> Int -> Int -> Int -> Bool
> fourEquals2 :: Int -> Int -> Int -> Int -> Bool

> fourEquals a b c d = (a == b) && (b == c) && (c == d)
> fourEquals2 a b c d = (threeEquals a b c) && (threeEquals b c d)
> -- fourEquals2 a b c d = (a == b) && (threeEquals b c d)

welche nur dann nur dann True zurück gibt, falls alle vier Argumente gleich sind. 
Implementieren Sie die Funktion fourEquals auf zwei verschiedenen Arten:
	- Geben Sie eine Implementation welche analog zur Implementation von threeEquals ist.
	- Geben Sie eine Implementation welche threeEquals aufruft um das Resultat zu berechnen.
Vergleichen Sie die beiden Implementationen.


c) Implementieren Sie eine Funktion, welche den Durchschnitt dreier Ints berechnet und als Double zurück gibt.
Hinweis: Sie benötigen die Funktion fromIntegral

> averageThree :: Int -> Int -> Int -> Double
> -- averageThree a b c = fromIntegral ((a + b + c) :: Int)  / 3
> averageThree a b c = (fromIntegral (a + b + c))  / 3


d)Implementieren Sie die Funktion

> xor :: Bool -> Bool -> Bool
> xor a b = a /= b

die nur dann True zurück gibt, wenn die beiden Argumente unterschiedlich sind. 



2. Aufzählungstypen und Tuples

a) Gegeben ist der Typ Op der für arithmetische Operationen steht:

> data Op = Add | Sub 

Definieren Sie die Funktion 

> calc :: Op -> Int -> Int -> Int
> calc Add a b = a + b
> calc Sub a b = a - b

Der erste Parameter bestimmt mit welcher Operation der zweite und der dritte Parameter verknüpft werden:
Bsp: calc Add 2 3 ~> 5


b) In dieser Aufgabe implementieren Sie eine einfache McDonalds Kasse. In unserer Filiale werden nur zwei Menus angeboten:
BigMac und CheeseRoyal. Die Menus gibt es jeweils in zwei unterschiedlichen Grössen: Small und Large.
Überlegen Sie, wie der Typ einer Bestellung (Order) abgebildet werden könnte unter der Verwendung von Enums und Tupels und
implementieren Sie dann die Funktion  price :: Order -> Int, die den Preis einer Bestellung berechnet.

Ein BigMac Menu kostet 10 CHF und
ein CheeseRoyal Menu kostet 11 CHF.

Die gegebenen Preise gelten für die kleinen Menus, die grossen Menus kosten jeweils 2 CHF mehr.

> data Menu = MkMenu {name :: String, menuPrice :: Int} deriving (Show)
> bigMac = MkMenu "BigMac" 10
> cheeseRoyal = MkMenu "CheeseRoyal" 11

> data Size = Small | Large deriving (Show, Eq)

> data Order = MkOrder {menu :: Menu, size :: Size} deriving (Show)

> -- for testing...
> ord1 = MkOrder bigMac Small
> ord2 = MkOrder bigMac Large
> ord3 = MkOrder cheeseRoyal Small
> ord4 = MkOrder cheeseRoyal Large
> -- ..............

> price :: Order -> Int
> price order = if (size order) == Small then menuPrice (menu order) else menuPrice (menu order) + 2


3. Typen bestimmen
Bestimmen Sie jeweils den allgemeinsten Typen der folgenden Funktionen:

a)	swap (x, y)  = (y, x)

> swap :: (a, b) -> (b, a)
> swap (x, y) = (y, x)

b)	pair x y = (x, y)

> pair :: x -> y -> (x, y)
> pair x y = (x, y)

c)	double x = x * 2

> double :: (Num a) => a -> a -- works for both Integral and Fractional Numbers
> double x = x * 2

d)	crazy (a, '&', (b, True)) = not (a && b)
Hinweis: Was muss der Typ von a und b sein, damit && verwendet werden kann?

> crazy :: (Bool, Char, (Bool, Bool)) -> Bool
> crazy (a, '&', (b, True)) = not (a && b)

e)	twice f x = f (f x)
Hinweis: überlegen Sie sich zuerst was f eigentlich ist. Dann bestimmen Sie den Typ von f!

> twice :: (a -> a) -> a -> a -- Keyword: Higher Order function
> twice f x = f (f x)

4. Funktionen bestimmen
Geben Sie eine beliebige legale Implementierung für folgende Definitionen:
Hinweis: Verzweifeln Sie nicht, wenn Sie eine Funktion nicht implementieren können!

> f1 :: Int -> Int
> f1 x = x

> f2 :: (Int, Bool) -> Int
> f2 (x, y) = x

> f3 :: a -> (a,Int)
> f3 x = (x, 1)

> f4 :: a -> b
> f4 a = f4 a -- not possible to define better...

> f5 :: a -> (a ->  b) -> b -- Return result of a (b is passed as argument to function a)
> f5 x f = f (x)
> f5' x f = f x


> todo = error "TODO"
```
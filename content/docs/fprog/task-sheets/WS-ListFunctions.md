---
title : 'WS ListFunctions'
date : 2023-09-30T12:34:22+02:00
tags: ["draft"]
author: "Leon"
math: false
---

| Signatur     | (++) :: [a] -> [a] -> [a]                                                                 |
| ------------ |-------------------------------------------------------------------------------------------|
| Beispiel     | [1,2] ++ [3,4,5] ~> [1,2,3,4,5]<br> "Hallo " ++ show 12 ~> "Hallo 12"                     |
| Beschreibung | Hängt zwei Listen aneinander.<br>Wird entsprechend verwendet um Strings zu konkatenieren. |
|              |                                                                                           |

#

| Signatur     | take :: Int -> [a] -> [a]                                                                                 |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | take 3 ['a','b','c','d','e'] ~> ['a','b','c']                                                             |
| Beschreibung | Nimmt die ersten n Elemente aus der Liste                                                                                                          |
|              |                                                                                                           |

#

| Signatur     | drop :: Int -> [a] -> [a]                                                                                                       |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | drop 3 [1,2,3,4,5,6] ~> [4,5,6]                                                                                                          |
| Beschreibung | Wirft die ersten n Elemente weg.                                                                          |

#

| Signatur     | (!!) :: [a] -> Int -> a                                                                                   |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |  [1,2,3,4,5,6] !! 2                                                                                                         |
| Beschreibung |  Return the element at the position i.                                                                                                         |

#

| Signatur     |  last [a] -> a  |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |   last [1,2,3,4,5,6] ~> 6                                                                                                        |
| Beschreibung | Gibt das letzte Element zurück.                                                                           |
|              |                                                                                                           |

#

| Signatur     | init [a] -> [a] |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | init ['a','b','c','d'] ~> ['a','b','c']                                                                   |
| Beschreibung | Return all elements of a list except the last one                                                                                                          |
|              |                                                                                                           |

#

| Signatur     | reverse [a] -> [a]  |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |  reverse [1,2,3,4,5,6]                                                                                                         |
| Beschreibung | Dreht eine Liste um.                                                                                      |
|              |                                                                                                           |

#

| Signatur     | elem :: Eq a => a -> [a] -> Bool |
| ------------ |----------------------------------|
| Beispiel     | elem 1 [1,2,3,4,5,6] ~> True, elem 7 [1,2,3,4,5,6] ~> False   |
| Beschreibung | checks if the specified element is in the list                                 |
|              |                                  |

#

| Signatur     | maximum (Ord a) => [a] -> a, minimum (Ord a) => [a] -> a  |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | maximum [1,4,3] ~> 4<br>minimum [1,4,3] ~> 1                                                              |
| Beschreibung | Returns the largest or smallest element of the list                                                                                                          |
|              |                                                                                                           |

#

| Signatur     | sum (Num a) => [a] -> a, product (Num a) => [a] -> a                                                                        |
| ------------ |--------------------------------------------------------------------------------------------------|
| Beispiel     | sum [1,2,3,4,5,6] ~> 21                                                                          |
| Beschreibung | Gibt die Summe/ das Produkt zurück. Die Listenelemente müssen von einem Zahlen Typen sein (Num). |
|              |                                                                                                  |

#

| Signatur     | zip :: [a] -> [b] -> [(a,b)]                                                                |
| ------------ |---------------------------------------------------------------------------------------------|
| Beispiel     | zip [1,2,3] [7,8,9] ~> [(1,7),(2,8),(3,9)], zip [1,2,3] [7,8,9,10] ~> [(1,7),(2,8),(3,9)], zip [1,2,3,4] [7,8,9] ~> [(1,7),(2,8),(3,9)] |
| Beschreibung | 'zip' takes two lists and returns a list of orresponding pairs.                                                                                            |
|              |                                                                                             |

#

| Signatur     |  concat [[a]] -> [a]                                                                                                           |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | concat [[1],[2,3],[4]] ~> [1,2,3,4] concat ["abc","def"] ~> "abcdef"                                      |
| Beschreibung | Concats multiple lists into one.                                                                                                          |

#

| Signatur     | zipWith (a -> b -> c) -> [a] -> [b] -> [c]                                                                |
| ------------ |-----------------------------------------------------------------------------------------------------------|
| Beispiel     | zipWith (+) [1,2,3] [10,11,12] ~> [11,13,15]    zipWith (++) ["Ha","Ec"] ["llo","ho"] ~> ["Hallo","Echo"] |
| Beschreibung | 'zipWith' generalises 'zip' by zipping with the function, given as the first argument, instead of a tupling function.                                                |

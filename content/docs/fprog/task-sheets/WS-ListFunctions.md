---
title : 'WS ListFunctions'
date : 2023-09-30T12:34:22+02:00
tags: ["draft"]
author: "Leon"
math: false
---

| Signatur     | (++) :: [a] -> [a] -> [a]                                                                                 |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | [1,2] ++ [3,4,5] ~> [1,2,3,4,5]<br>"Hallo " ++ show 12 ~> "Hallo 12"                                      |
| Beschreibung | Hängt zwei Listen aneinander.<br>Wird entsprechend verwendet um Strings zu konkatenieren.                 |
|              |                                                                                                           |


| Signatur     | take :: Int -> [a] -> [a]                                                                                 |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | take 3 ['a','b','c','d','e'] ~> ['a','b','c']                                                             |
| Beschreibung |                                                                                                           |
|              |                                                                                                           |



| Signatur     | abc                                                                                                       |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung | Wirft die ersten n Elemente weg.                                                                          |



| Signatur     | (!!) :: [a] -> Int -> a                                                                                   |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung |                                                                                                           |


| Signatur     |    |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung | Gibt das letzte Element zurück.                                                                           |
|              |                                                                                                           |


| Signatur     |  |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | init ['a','b','c','d'] ~> ['a','b','c']                                                                   |
| Beschreibung |                                                                                                           |
|              |                                                                                                           |


| Signatur     |   |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung | Dreht eine Liste um.                                                                                      |
|              |                                                                                                           |


| Signatur     | elem :: Eq a => a -> [a] -> Bool                                                                          |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung |                                                                                                           |
|              |                                                                                                           |


| Signatur     |  |  
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     | maximum [1,4,3] ~> 4<br>minimum [1,4,3] ~> 1                                                              |
| Beschreibung |                                                                                                           |
|              |                                                                                                           |


| Signatur     |                                                                                                           |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung | Gibt die Summe/ das Produkt zurück. Die Listenelemente müssen von einem Zahlen Typen sein (Num).          |
|              |                                                                                                           |


| Signatur     | zip :: [a] -> [b] -> [(a,b)]                                                                              |
| ------------ | --------------------------------------------------------------------------------------------------------- |
| Beispiel     |                                                                                                           |
| Beschreibung |                                                                                                           |
|              |                                                                                                           |


| Signatur     |                                                                                                           |
| Beispiel     | concat [[1],[2,3],[4]] ~> [1,2,3,4] concat ["abc","def"] ~> "abcdef"                                      |
| Beschreibung |                                                                                                           |


| Signatur     |                                                                                                           |
| Beispiel     | zipWith (+) [1,2,3] [10,11,12] ~> [11,13,15]    zipWith (++) ["Ha","Ec"] ["llo","ho"] ~> ["Hallo","Echo"] |
| Beschreibung |                                                                                                           |



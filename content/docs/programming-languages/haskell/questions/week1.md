---
title : 'Week1'
date : 2023-09-08T22:09:52+02:00
tags: ["week1"]
author: "Leon"
---

### Was genau machen die Backticks in einem Befehl?
> lambda \`beside\` (invert lambda)

**Antwort**

Man nennt diese die "infix" Notation. Der Funktionsname wird so in die Mitte der beiden Parameter gestellt:
```haskell
render (lambda `beside` (invert lambda))
-- ist das gleiche wie:
render (beside lambda (invert lambda))
```
Es ist tatsächlich auch möglich, die Infix Schreibweise bei Funktionen mit mehr als zwei Parametern zu verwenden. 
Jedoch wird davon abgeraten:
```haskell
test :: Integer -> Integer -> Integer -> Integer
test a b c = a + b + c

-- Aufruf:
test 1 2 3
 -- mit infix
(1 `test` 2) 3
```

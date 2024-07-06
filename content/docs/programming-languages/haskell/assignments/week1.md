---
title : 'Week1'
date : 2023-09-08T21:41:10+02:00
tags: ["week1"]
author: "Leon"
---

### Task 1

> Finden Sie die Ausdrücke um folgende Bilder zu erzeugen.
 
![week1Task1](/fprog/images/a/week1Task1.png)

a) 

`render (beside lambda (beside lambda lambda))`

b)

`render ( above (beside lambda (invert lambda)) (beside (invert lambda) lambda) )`

c)

`render ( invert ( flipV (flipH lambda) ) )`

### Task 2 - rotate180

> Definieren Sie die Funktion rotate180 :: Picture -> Picture, die das Bild um 180° rotiert. Verwenden Sie
dazu nur die vorgegebenen Funktionen. Sie können die Funktion gleich im File PicturesSVG.hs
implementieren.


```haskell
rotate180 :: Picture -> Picture
rotate180 x = flipH (flipV x)

-- Execute:
rotate190 lambda
```

### Task 3

> Geben Sie die Herleitung der folgenden Ausdrücke

```haskell
times2 :: Integer -> Integer
times2 x = 2 * x -- (t2)

square :: Integer -> Integer
square x = x * x -- (sqr)

pyth :: Integer -> Integer -> Integer
pyth a b = square a + square b -- (py)
```

a) square (times2 3)

```
square (times2 3)
~> square (2 * 3)   -- using (times2)
~> square 6         -- arithmetic
~> 6 * 6            -- using (square)
~> 36               -- arithmetic
```

b) pyth 2 2

```
pyth 2 2                
~> square 2 + square 2  -- using (pyth)
~> 2 * 2 + square 2     -- using (square)
~> 2 * 2 + 2 * 2        -- using (square)
~> 4 + 2 * 2            -- arithmetic
~> 4 + 4                -- arithmetic
~> 8                    -- arithmetic
```

c) pyth (square 2) 3

```
pyth (square 2) 3
~> pyth (2 * 2) 3       -- using (square)
~> pyth 4 3             -- arithmetic
~> square 4 + square 3  -- using (pyth)
~> 4 * 4 + square 3     -- using (square)
~> 4 * 4 + 3 * 3        -- using (square)
~> 16 + 3 * 3           -- arithmetic
~> 16 + 9               -- arithmetic
~> 25                   -- arithmetic
```

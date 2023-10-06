---
title : 'Types'
date : 2023-09-23T13:15:42+02:00
tags: ["types"]
author: "Leon"
math: false
---

> Zur Kompilationszeit haben wir Typen, zur Laufzeit die Werte
 
## Basic Types

### Bool
True, False 

### Char
'a', ...

### Int (primitiv Int)
Fixed precision (-2^62 to 2^63 -1)
```haskell
> maxBound :: Int
92..........

> (maxBound :: Int) + 1
-92.... (overflow)
```


### Integer
Default if entered as standard number:
```haskell
45
-> Integer
```

### Double
Floating point numbers
```haskell
> pi
3.1415926535...

> :t pi
pi :: Floating a => a
```




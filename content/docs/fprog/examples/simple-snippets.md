---
title : 'Simple Snippets'
date : 2023-09-06T23:23:35+02:00
#tags: ["snippets"]
author: "Leon"
---

### a + b function

```haskell
add :: Int -> Int -> Int
add a b = a + b
```

```haskell
size :: Integer
size = (7 - 3) * 2
```

![input output](/fprog/images/inputoutput.png)

```haskell
square :: Integer -> Integer
square n = n * n
```

```haskell
mul:: Integer -> Integer -> Integer
mul x y = x * y

--- Application
square 2
mul 1 size
mul (square 2) 3
```
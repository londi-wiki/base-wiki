---
weight: 999
title: "Io Input Output"
description: ""
icon: "article"
date: "2023-11-18T11:31:02+01:00"
lastmod: "2023-11-18T11:31:02+01:00"
draft: false
toc: true
---

## IO Example

```haskell
-- IOExample.hs
main :: IO ()
main = do putStrLn "Enter name:"
          name <- getLine
          let msg = "Hi " ++ name
          putStrLn msg
```

Execute:
```Bash
ghc IOExample.hs
./IOExample
```

## Read and casting

Cast String to Int:
```haskell
> read "6" :: Int
6
it :: Int
```

Back and forth:
```haskell
> s = show (12, True)
s :: String

> s
"(12, True)"

> read s :: (Int,Bool)
(12, True)
it :: (Int, Bool)
```

## MiniCalc Simple

```haskell
main :: IO ()
main = do putStrLn "Welcome to MiniCalc!\nPlease enter a first number:"
          f1Raw <- getLine
          let f1 = read f1Raw :: Int
          putStrLn "Please enter a second number:"
          f2Raw <- getLine
          let f2 = read f2Raw :: Int
          putStrLn (show (f1) ++ " + " ++ show (f2) ++ " = " ++ show (f1+f2))
          main
```

## MiniCalc Advancde

```haskell
main' :: IO ()
main' = do putStrLn "Welcome to MiniCalc!"
           loop

loop = do putStrLn "Please enter a first number:"
          f1Raw <- getLine
          let f1 = read f1Raw :: Int
          putStrLn "Please enter a second number:"
          f2Raw <- getLine
          let f2 = read f2Raw :: Int
          putStrLn "Please enter a operation (+,-,*,^):"
          opRaw <- getLine
          let op = opMatcher opRaw
          putStrLn (show (f1) ++ " " ++ opRaw ++ " " ++ show (f2) ++ " = " ++ show (op f1 f2))
          loop

opMatcher :: String -> (Int -> Int -> Int)
opMatcher "+" = (+)
opMatcher "-" = (-)
opMatcher "*" = (*)
opMatcher "^" = (^)
```

### Move recursive command outside

```haskell
forever :: IO () -> IO ()
forever a = do a
               forever a

main' = do putStrLn "Welcome to MiniCalc!"
           forever loop
```


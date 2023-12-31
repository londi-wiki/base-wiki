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

## Input Output

```haskell
-- Reading a line
getLine :: IO String

-- Reading a single character
getChar :: IO Char

-- Writing s string
putStr :: String -> IO ()

-- Writing a string followed by a newline
putStrLn :: String -> IO ()
```

## Unit - One Element Type

```haskell
-- putStrLn does not return an interesting value:
putStrLn :: String -> IO ()
```

## Return statement

```haskell
return :: a -> IO a

main :: IO ()
main = do putStrLn "Enter a text"
          input <- getLine
          putStrLn (reverse input)
          putStrLn "continue? y/n"
          continue <- getChar
          putStrLn ""
          if continue == 'y' then main else return ()
```

## Simple File IO

```haskell
-- Identifying a file by a path
type FilePath = String

-- Reading content from a file
readFile :: FilePath -> IO String

-- Writing content to a file
writeFile :: FilePath -> String -> IO ()

-- Example: Copy a text file
main :: IO ()
main = do content <- readFile "in.txt"
          writeFile "out.txt" content
```

### openFile: resource busy (file is locked)

The statement `$!` is used to force the evaluation of the second argument and guarantees that the file is fully loaded before using the content.

```haskell
($!) :: (a -> b) -> a -> b

-- Example
readTasks :: IO TaskList
readTasks = do content <- readFile "TaskListDB.txt"
               let list = read content :: [(Bool,String)]
               return $! list
```

## Command Line Arguments

```haskell
-- Get arguments
getArgs :: IO [String]

-- Example
import System.Environment
import Data.List

main :: IO ()
main = do args <- getArgs
          putStrLn (intercalate "\n" args)
```

## do Notation

```haskell
action = putStrLn "ab" >> putStrLn "cd"
action :: IO ()
ab
cd

action = getLine >>= \s -> (putStr reverse s) >> writeFile "bla.txt" s)
action :: IO ()
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


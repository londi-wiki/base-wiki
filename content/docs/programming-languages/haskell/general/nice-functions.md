---
weight: 999
title: "Nice Functions"
description: ""
icon: "article"
date: "2023-11-22T21:19:47+01:00"
lastmod: "2023-11-22T21:19:47+01:00"
draft: false
toc: true
---

## intercalate

```haskell
:t intercalate
intercalate :: [a] -> [[a]] -> [a]

> intercalate "hello" ["A", "B", "C", "D"]
"AhelloBhelloChelloD"

> putStrLn (intercalate "\n" ["A", "B", "C", "D"])
A
B
C
D
```

## Feature dispatcher

```haskell
dispatch :: String -> String -> IO ()
dispatch "list"  _ = listTaskAction taskFile
dispatch "add"   t = addTaskAction taskFile t
dispatch "done"  i = markDoneAction taskFile i
dispatch _       _ = return ()
```

---

## Siehe auch

- → [Listen](/docs/programming-languages/haskell/general/lists) – Cons, Pattern Matching, filter und map
- → [Higher Order Functions](/docs/programming-languages/haskell/general/higher-order-functions) – Funktionen als Argumente und Rückgabewerte

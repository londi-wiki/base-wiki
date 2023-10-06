---
title : 'Usage'
date : 2023-09-06T23:39:27+02:00
tags: ["howto"]
author: "Leon"
---

### Show type of function

```haskell
:type <something>
```

### Enter function definition in ghci

```haskell
Prelude> :{
Prelude| fstInt :: (Int, Int) -> Int
Prelude| fstInt (x,y) = x
Prelude| :}
fstInt :: (Int, Int) -> Int

> fstInt (1, 8)
1
it :: Int
```

### General functions

| Command      | Description                         |
|--------------|-------------------------------------|
| :?           | Shows help                          |
| :cd /path/to | change directory to /path/to        |
| :l script.hs | loads script.hs                     |
| :r           | reloads the current script          |
| :t expr      | shows the type of the given expression |  
| :q           | exits the current session           |
| :            | repeat last command                 |
| :browse      | list all functions                  |

### Always show type of result

Example (before)
```haskell
> not True
False

> :T not True 
not True :: Bool
```

```bash
nano ~/.ghci
:set +t
```

Example (after)

```haskell
> not True
False
it :: Bool
```

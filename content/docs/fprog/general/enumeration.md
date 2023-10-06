---
title : 'Enumeration'
date : 2023-09-24T16:58:01+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Example Enum

Color
- Red
- Yellow
- Green

```haskell
> data Color = Red | Yellow | Green deriving (Show)
data Color = ...

> Red
Red
it :: Color
```

### deriving (show)
Equivalent to java's toString. It prints/shows the name of the value.
e.g. 
```haskell 
show Red
"Red"
```

This is necessary to show something if entering a value of the enum. Otherwise, an error will occur...

### Funfact

Bool is also an Enum

```haskell
> :info Bool

data Bool = False | True        -- Defined in ‘GHC.Types’
instance Eq Bool -- Defined in ‘GHC.Classes’
instance Ord Bool -- Defined in ‘GHC.Classes’
instance Enum Bool -- Defined in ‘GHC.Enum’
instance Show Bool -- Defined in ‘GHC.Show’
instance Read Bool -- Defined in ‘GHC.Read’
instance Bounded Bool -- Defined in ‘GHC.Enum’
```

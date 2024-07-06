---
title : 'Function Types'
date : 2023-09-24T18:40:06+02:00
tags: ["draft"]
author: "Leon"
math: false
---

### Example

```haskell

> data ToDo = Stop | Wait | Go deriving (Show)
> data Color = Red | Yellow | Green deriving (Show)

:{
atTrafficLight :: Color -> ToDo
atTrafficLight Red = Stop
atTrafficLight Yellow = Wait
atTrafficLight Green = Go
:}

> atTrafficLight Yellow
Wait
it :: ToDo
```


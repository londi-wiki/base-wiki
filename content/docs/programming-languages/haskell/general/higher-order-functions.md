---
title : 'Higher Order Functions'
date : 2023-09-25T16:11:46+02:00
tags: ["draft"]
author: "Leon"
math: false
---

Source: [wiki.haskell](https://wiki.haskell.org/Higher_order_function)

# Definition

A higher-order function is a function that takes other functions as arguments or returns a function as result.

## Example

```haskell
> twice :: (a->a) -> a -> a
> twice f x = f (f x)
```

---

## Siehe auch

- → [Currying](/docs/programming-languages/haskell/general/currying) – warum jede Funktion nur ein Argument hat
- → [Lambda-Ausdrücke](/docs/programming-languages/haskell/general/lambda-expressions) – anonyme Funktionen
- → [Listen](/docs/programming-languages/haskell/general/lists) – Cons, Pattern Matching, filter und map

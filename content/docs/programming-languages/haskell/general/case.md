---
weight: 999
title: "Case"
description: ""
icon: "article"
date: "2023-10-08T16:08:20+02:00"
lastmod: "2023-10-08T16:08:20+02:00"
draft: false
toc: true
---

```haskell
case expression of
  pattern -> result
  pattern -> result
    ...
    
    
f1 :: Int -> Int
f1 x =
    case x of
        0 -> 0
        1 -> 10
        2 -> 20
        _ -> 20 - x
```

---

## Siehe auch

- → [Pattern Matching](/docs/programming-languages/haskell/general/pattern-matching) – Konstanten, Listen, Tupel und Guards
- → [where und let](/docs/programming-languages/haskell/general/where-let-clause) – Hilfsdefinitionen an der richtigen Stelle
- → [if then else](/docs/programming-languages/haskell/general/ternary-operator) – der bedingte Ausdruck

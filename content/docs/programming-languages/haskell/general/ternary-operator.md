---
weight: 999
title: "Ternary Operator"
description: ""
icon: "article"
date: "2023-10-08T16:17:06+02:00"
lastmod: "2023-10-08T16:17:06+02:00"
draft: false
toc: true
---

```haskell
if a == b then "foo" else "bar"
```

```haskell
ite :: Bool -> a -> a -> a
ite True i _ = i
ite False i _ = e

> ite (null []) 5 undefined
```


---
title : 'Week2'
date : 2023-09-26T18:51:37+02:00
tags: ["draft"]
author: "Leon"
math: false
---

### Show warnings

```haskell
-- Non-exhaustive patterns in function
-- Enable all warning messages:
:set -Wall

```

### Prefix for functions of a record

(also look for "haskell lenses")

```haskell
data Person = MkPerson { person_name :: String, person_age :: Int }
data Pet = MkPerson { pet_name :: String, pet_age :: Int }
```


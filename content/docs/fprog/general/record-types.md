---
title : 'Record Types'
date : 2023-09-24T18:11:11+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Format

```haskell
> data Person = Person {name :: String, age :: Int } deriving (Show)
data Person = ...
age :: Person -> Int
name :: Person -> String

> :t Person
Person :: String -> Int -> Person

> Person "Leon" 99
Person {name = "Leon", age = 99}
it :: Person

> age (Person "Leon" 99)
99
it :: Int

-- or named:

> me = Person "Leon" 99
me :: Person

> show me
"Person {name = \"Leon\", age = 99}"
it :: String

> age me
99
it :: Int
```

### Typename and Constructor

```haskell
> data Person = MkPerson {name :: String, age :: Int } deriving (Show)
> bob = MkPerson "Bob" 99

> bob
MkPerson {name = "Bob", age = 99}
it :: Person
```
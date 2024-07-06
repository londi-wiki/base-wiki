---
title : 'WS TypeBasics'
date : 2023-09-23T13:23:13+02:00
tags: ["draft"]
author: "Leon"
math: false
---

## Type Beispiele

| x | Ausdruck                             | Erwartetes (sinnvolles) Resultat | JS     | Python  | Java   | Haskell |
|---|--------------------------------------|----------------------------------|--------|---------|--------|---------|
| a | 5 + 8                                | 13                               | 13     | 13      | 13     | 13      |
| b | 5 + "8"                              | 13                               | 58     | Error   | 58     | Error   |
| b' | 5 + "Hallo"                           | 5Hallo                           | 5Hallo | Error   | 5Hallo | Error   |
| c | 5 + true bzw. 5 + True               | Error                            | 6      | 6       | Error  | Error   |
| d | 5 - "2"                              | Error                            | 3      | Error   | Error  | Error   |
| e | 5 * 1                                | 5                                | 5      | 5       | 5      | 5       |
| f | 5 * "1"                              | 5                                | 5      | "11111" | Error  | Error   |
| g | false * "Hallo" bzw. False * "Hallo" | Error                            | NaN    | ""      | Error  | Error   |

## Typsytem Vergleich

| x                   | JS                                                 | Java                                                      | Haskell                       |
|---------------------|----------------------------------------------------|-----------------------------------------------------------|-------------------------------|
| Discipline          | dynamic (Erst zur Laufzeit wird geprüft (runtime)) | static (wird vom Compiler geprüft (compile time))         | static                        |
| Overloading         | ✅ "a" + "b" oder 1 + 2                             | ✅                                                         | ✅ 1.1 + 0.5 oder 1 + 3        |
| Implicit Conversion | ✅ "5" * 8 = 40 [^1]  (String to int) (weak)        | ✅ "5" * 8 = 40 = 58 (int to String (ascii value)) (weak)  | ❌ striktes typsystem (strong) |

[^1]: Wobei "5" + 8 = 58 ist

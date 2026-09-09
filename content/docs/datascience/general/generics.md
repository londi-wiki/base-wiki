---
weight: 999
title: "Generics"
description: ""
icon: "article"
date: "2023-10-05T15:04:11+02:00"
lastmod: "2023-10-05T15:04:11+02:00"
draft: false
toc: true
katex: true
---

## Beispiel

```python
from typing import Hashable, Iterable, TypeVar

_T = TypeVar("_T", bound=Hashable)


# before
def count(iterable: str, counts: Optional[dict[str, int]] = None) -> dict[str, int]:
    ...

# after
def count(iterable: Iterable[_T], counts: dict[_T, int] = {}) -> dict[_T, int]:
    ...
```

---

## Siehe auch

- → [Klassen und Variablen](/docs/datascience/general/classes-variables) – Format Strings, with, Argumente, Dunder und Dataclass
- → [Generics, Streams und Lambdas](/docs/programming-languages/java/generics) – Typparameter, Wildcards und Stream-Pipelines

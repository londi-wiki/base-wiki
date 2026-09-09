---
weight: 999
title: "Code Smells"
description: ""
icon: "article"
date: "2023-10-05T14:58:31+02:00"
lastmod: "2023-10-05T14:58:31+02:00"
draft: false
toc: true
---

## Mutable Default Arguments

### Beschreibung

[Erläuterung](https://docs.python-guide.org/writing/gotchas/#:~:text=Python's%20default%20arguments%20are%20evaluated,to%20the%20function%20as%20well.)

Python Funktionen werden nur einmal beim ersten Aufruf geladen, danach nicht mehr. Deshalb sind mutable variablen als Argumente nicht empfehlenswert. Besserer Ansatz ist, die Variable mit 'None' zu definieren und dann in der Funktion diese ggf. zu initialisieren.

### Beispiel

```python
def append_to(element, to=None):
    if to is None:
        to = []
    to.append(element)
    return to
```

---

## Siehe auch

- → [Klassen und Variablen](/docs/datascience/general/classes-variables) – Format Strings, with, Argumente, Dunder und Dataclass
- → [Python Tooling](/docs/datascience/general/python-tooling) – black, ruff, mypy, pytest und pre-commit

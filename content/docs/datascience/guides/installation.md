---
title : 'Installation'
date : 2023-09-21T12:13:14+02:00
tags: ["installation"]
author: "Leon"
math: false
draft: false
---

Jupyter Notebook in einem Docker Container ausführen:

```shell
docker run -d --name=jupyter_playground -p 8888:8888 -v "${PWD}":/home/jovyan/work jupyter/scipy-notebook
```

---

## Siehe auch

- → [Jupyter benutzen](/docs/datascience/guides/usage) – Magic Cells, LaTeX und Hilfetexte
- → [Python Tooling](/docs/datascience/general/python-tooling) – black, ruff, mypy, pytest und pre-commit

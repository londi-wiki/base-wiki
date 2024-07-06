---
weight: 999
title: "Plot Data"
description: ""
icon: "article"
date: "2023-10-26T13:31:52+02:00"
lastmod: "2023-10-26T13:31:52+02:00"
draft: false
toc: true
---

# Visualization with Matplotlib

![Matplotlib Cheatsheet](https://matplotlib.org/cheatsheets/_images/cheatsheets-1.png)

![Handsout for beginners](https://matplotlib.org/cheatsheets/_images/handout-beginner.png)

[Links](https://matplotlib.org/cheatsheets/)

## Preparation

```python
# import the pyplot submodule
import matplotlib.pyplot as plt

# set a style (https://matplotlib.org/examples/style_sheets/style_sheets_reference.html)
plt.style.use('seaborn-v0_8-muted')
```

## example

```python
# figsize in inches!
fig, ax = plt.subplots(nrows=1, ncols=1, figsize=(9, 4))
# line plot with added labels
_ = ax.plot(x, np.sin(x), label='sin')
_ = ax.plot(x, np.cos(x), label='cos')
# adding a vertical line at location pi
ymin, ymax = ax.get_ylim()
_ = ax.vlines(np.pi, ymin, ymax, color='red', label=r'$\pi$', lw=3)
# adding a legend for the labels
_ = ax.legend()
# defining the x-ticks
_ = ax.set_xticks(np.linspace(-10,10,21))
# adding labels to the axis (using LaTex notation)
_ = ax.set_ylabel(r'$f(x)$')
_ = ax.set_xlabel(r'$x$')
# add title
_ = ax.set_title(r'The Sine and Cosine Functions')
# adding a grid to the axes
_ = ax.grid()
```

## save figure

```python
fig.canvas.get_supported_filetypes()

fig.savefig('sinus_cosinus.png')
```

---
weight: 999
title: "Diskriptive Statistik"
description: ""
icon: "article"
date: "2023-11-23T13:21:35+01:00"
lastmod: "2023-11-23T13:21:35+01:00"
draft: false
toc: true
katex: true
---

# Theorie

## Skalenniveau

- Kategorische Var
- Ordinale Var
- Intervallskala
- Verhältnisskala

## Lage

- Modus
- Mittelwert
- Median
- Quantil

## Streuung

### Quartilsdifferenz

### Varianz

$\sigma^{2} = \frac{1}{n} * \sum_{i=1}^{n}(x_i - \bar x)^2 $

### Standardabweichung

$ \sigma^{x} = \sqrt[2]{\sigma^{2}} $

## Form

### Symmetrie / Schiefe

- Linksschief
- Rechtsschief
- Flachgipfelig

$$
\gamma_3 = \frac{1}{n}\sum_{i=1}^n z_i^3
$$

### Wölbung / Exszess

$$
\gamma_4 = \frac{1}{n}\sum_{i=1}^n z_i^4
$$

$$
\mathsf{Exzess} = \frac{1}{n}\sum_{i=1}^n z_i^4 - 3
$$

### Modalität



# Anwendung

## Bins

```json
bins = [0,2,4, ...]
bins => [0,2), [2,4), ...
```

Stichwort: freedman diaconis formel

$\mathsf{Bin width} = 2 * \frac{IQR(x)}{\sqrt[3]{}n}$
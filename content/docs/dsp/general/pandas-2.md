---
weight: 999
title: "Pandas 2"
description: ""
icon: "article"
date: "2023-11-09T13:31:03+01:00"
lastmod: "2023-11-09T13:31:03+01:00"
draft: false
toc: true
---

# Handle missing values

- Read a csv file
- Skip NaN values

```python
import pandas as pd
df = pd.read_csv('08-01_haushaltsstruktur_zuerich.csv', skiprows=13, na_values=['.'])

# find rows with missing values
df[df.isna().any(axis=1)]
```

> All pandas methods for descriptive statistics exclude missing values.


### methods for missing values

Zum Finden, Entfernen und Füllen von fehlenden Werten stellt `pandas` die folgenden Methoden zur Verfügung:

| Methode                |  Funktion   |
|------------------------|-------------|
| ``isna``, ``isnull``   | *Boolean indicator* für fehlende Werte.     |
| ``notna``, ``notnull`` | Negation der oberen Funktion.               |
| ``dropna``             | Enfernt fehlende Werte, bzw. Zeilen mit fehlenden Werten. |
| ``fillna``             | Füllt fehlende Werte ein mit einem *default*-Wert oder gemäss einer Interpolationsmethode. |
| ``interpolate``        | Interpoliert fehlende Werte mit einer zu wählenden Interpolationsmethode. |


# Concat datas

In `pandas` gibt es auch hierfür Werkzeuge:

- `pd.concat` : Fügt Werte entlang einer bestimmten 'Achse' (*axis*) zusammen.
- `pd.merge`: Führt eine Datenbank-typische *join*-Operation aus zum Zusammenführen zweier `DataFrame`s.
- `Series.combine_first`: Kann verwendet werden, um aus einer `Series`-Werte in eine andere einzufügen wo diese fehlen.

```python
# merge two dataframes along a given attribute: on
df = df.merge(kq, on='QuarLang')
df.head()
```

## Groupby

```python
# verification of correctnes of merge
df.groupby(by='Kreis')['QuarLang'].unique()
```
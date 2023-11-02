---
weight: 999
title: "Pandas"
description: ""
icon: "article"
date: "2023-11-02T13:18:15+01:00"
lastmod: "2023-11-02T13:18:15+01:00"
draft: false
toc: true
---

# Pandas

[Cheatsheet](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)

## Series

```python
import pandas as pd

s = pd.Series([1., 1., 2., 3., 5., 8., 13., 21., ], name='fib')
# 0     1.0
# 1     1.0
# 2     2.0
# 3     3.0
# 4     5.0
# 5     8.0
# 6    13.0
# 7    21.0
# Name: fib, dtype: float64


s.values
# array([ 1.,  1.,  2.,  3.,  5.,  8., 13., 21.])

s = pd.Series([1., 1., 2., 3., 5., 8., 13., 21., ], index=['a', 'b','c','d','e','f','g','h'], name='fib')
# a     1.0
# b     1.0
# c     2.0
# d     3.0
# e     5.0
# f     8.0
# g    13.0
# h    21.0
# Name: fib, dtype: float64


s.index
# Index(['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h'], dtype='object')
```

## Access elements

```python
s[[1543, 2099, ]]
# 1543    2.0
# 2099    3.0
# Name: fib, dtype: float64


# Slicing with 'loc' is always inclusive the last mentioned element.
s.loc[1543:3459]
# 1543     2.0
# 2099     3.0
# 2433     5.0
# 3333     8.0
# 3459    13.0
# Name: fib, dtype: float64


# Slicing with 'iloc' is always exclusive the last mentioned element.
s.iloc[0:2]
# 1223    1.0
# 1345    1.0
# Name: fib, dtype: float64


# Iterate
for item in s.iteritems():
    print(item)
# (1223, 1.0)
# (1345, 1.0)
# (1543, 2.0)
# (2099, 3.0)
# (2433, 5.0)
# (3333, 8.0)
# (3459, 13.0)
# (3461, 21.0)
```

## DataFrame

```python
population_dict = {'California': 38332521,
                   'Texas': 26448193,
                   'New York': 19651127,
                   'Florida': 19552860,
                   'Illinois': 12882135}

population = pd.Series(population_dict)

# California    38332521
# Texas         26448193
# New York      19651127
# Florida       19552860
# Illinois      12882135
# dtype: int64


states = pd.DataFrame(population, columns=['population'])
# Shows the table:
```

|            | population |
| ---------- | ---------- |
| California | 38332521   |
| Texas      | 26448193   |
| New York   | 19651127   |
| Florida    | 19552860   |
| Illinois   | 12882135   |


```python
area_dict = {'California': 423967, 'Texas': 695662, 'New York': 141297,
             'Florida': 170312, 'Illinois': 149995}
area = pd.Series(area_dict)
# California    423967
# Texas         695662
# New York      141297
# Florida       170312
# Illinois      149995
# dtype: int64

states = pd.DataFrame({'population': population, 'area': area })
```

|  |   population   |    area    |
| ---------- | -------- | ------ |
| California | 38332521 | 423967 |
| Texas      | 26448193 | 695662 |
| New York   | 19651127 | 141297 |
| Florida    | 19552860 | 170312 |
| Illinois   | 12882135 | 149995 |


## Filter

```python
# simple filter
states[states.population > 20000000]

# Combine results of two conditions
states[(states.area < 160000) & (states.population < 20000000)]

# filter function
states.filter(regex=r'or', axis=0) # r makes the String to a raw String

# query
states.query('`area` > 171297')
```

## Reindexing

Change row order

```python
new_index = ['Texas', 'New York', 'Illinois', 'California', 'Florida', ]
states.reindex(new_index)
```

## Sorting

```python
states.sort_index()
states.sort_values(by='population')
```

## DataFrame io

```python
print('\n'.join([method for method in dir(pd) if method.startswith('read')]))
# read_clipboard
# read_csv
# read_excel
# read_feather
# read_fwf
# read_gbq
# read_hdf
# read_html
# read_json
# read_orc
# read_parquet
# read_pickle
# read_sas
# read_spss
# read_sql
# read_sql_query
# read_sql_table
# read_stata
# read_table


print('\n'.join([method for method in dir(states) if method.startswith('to_')]))
# to_clipboard
# to_csv
# to_dict
# to_excel
# to_feather
# to_gbq
# to_hdf
# to_html
# to_json
# to_latex
# to_markdown
# to_numpy
# to_parquet
# to_period
# to_pickle
# to_records
# to_sql
# to_stata
# to_string
# to_timestamp
# to_xarray
```

## Operations on DataFrames

```python
import numpy as np
df = pd.DataFrame(np.random.randint(0, 10, (3, 4)),
                  columns=['A', 'B', 'C', 'D'])
```

|   | A | B | C | D |
| - | - | - | - | - |
| 0 | 1 | 6 | 3 | 3 |
| 1 | 0 | 4 | 3 | 1 |
| 2 | 1 | 1 | 3 | 4 |


```python
np.sin(df) # only affects values not col/row index
```

## Descriptive stats

```python
df.median()
# A    1.0
# B    4.0
# C    3.0
# D    3.0
# dtype: float64
```

## String operations

```python
data = [
    {'state': 'California', 'capital': 'Sacramento', 'population': 38332521, 'area': 423967},
    {'state': 'Texas', 'capital': 'Austin  ', 'population': 26448193, 'area': 695662},
    {'state': 'New York', 'capital': 'New York   ', 'population': 19651127, 'area': 141297},
    {'state': 'Florida', 'capital': 'miami ', 'population': 19552860, 'area': 170312},
    {'state': 'Illinois', 'capital': 'springfield', 'population': 12882135, 'area': 149995}
]

states = pd.DataFrame(data)

states.capital
# 0     Sacramento
# 1       Austin
# 2    New York
# 3         miami
# 4    springfield
# Name: capital, dtype: object


states.capital.str.rstrip().str.capitalize()
# 0     Sacramento
# 1         Austin
# 2       New york
# 3          Miami
# 4    Springfield
# Name: capital, dtype: object
```

## Apply and applymap function

```python
states[['area', 'population']].apply(lambda x: np.sin(x)+np.log(x))
```

|  | area |    population       |
| ---- | ---------- | --------- |
| 0    | 13.303482  | 18.409559 |
| 1    | 13.737766  | 16.275091 |
| 2    | 12.524603  | 16.789728 |
| 3    | 12.024452  | 17.691891 |
| 4    | 12.253018  | 16.602798 |


```python
states.applymap(lambda x: '< {} >'.format(x))
```

|   | state          | capital         | population   | area       |
| - | -------------- | --------------- | ------------ | ---------- |
| 0 | < California > | < Sacramento >  | < 38332521 > | < 423967 > |
| 1 | < Texas >      | < Austin >      | < 26448193 > | < 695662 > |
| 2 | < New York >   | < New york >    | < 19651127 > | < 141297 > |
| 3 | < Florida >    | < Miami >       | < 19552860 > | < 170312 > |
| 4 | < Illinois >   | < Springfield > | < 12882135 > | < 149995 > |

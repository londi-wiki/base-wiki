---
title : 'Classes Variables'
date : 2023-09-28T13:26:51+02:00
tags: ["draft"]
author: "Leon"
math: false
draft: false
---

### Format String

```python
print( "A {}".format("Hello") )

print(f"A {math.sin(60)}")
print(f"A {math.sin(60) = }")
```


### Switch

```python
def add...

def do(a, b, what="add"):
    switch = {
        "add": add,
        
    }
    return switch[what](a, b)
```

### with

```python
with open(...):
    pass
    
# After the with section, the exit() function of the file object will be called.
```

## Arguments of functions



```python
sum([1,2,3], start=20)
> 26
```

Arguments:

1. `arg`
2. `*args`
3. `kwarg`
`**kwargs`

```python
def pos_only_kw_only(a, /, b, *, c):
  pass
```

### return and yield

```python
def banana(multiplicand, upper_bound=100):
  value = 0
  while value < upper_bound:
      yield value
      value += multiplicand
```

### "dunder" functions
```python

class Test:
    def __init__(self, ...) -> None:
        pass
        
    # tosString
    def __str__(self) -> str:
        pass
        
    @property
    def tuple(self) -> (int, int, int):
        '''Returns an RGB tuple.
        '''
        return (self.red, self.green, self.blue)
        
    @staticmethod
    
```

### Dataclass

```shell

```


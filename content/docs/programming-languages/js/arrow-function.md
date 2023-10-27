---
weight: 999
title: "Arrow Function"
description: ""
icon: "article"
date: "2023-10-27T17:24:58+02:00"
lastmod: "2023-10-27T17:24:58+02:00"
draft: false
toc: true
---

## Example

```javascript
const f = n => {
    return n * 2
}

const f2 = n => n * 2

const f3 = (a, b) => a + b
```

## destructing

```javascript
let obj1 = { a: 2, b: 3 }

const q = o => {
    console.log(o.a + o.b)
}
q(obj1)

const p = ({ a, b }) => {
    console.log(a + b)
}
p(obj1)
```

## automatic binding

```javascript
const f = () => { console.log(this) }
f()
// return the window object

class C {
    s = () => { console.log(this) }
}
new C().s()
// returns the class
```
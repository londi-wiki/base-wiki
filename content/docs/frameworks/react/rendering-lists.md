---
weight: 999
title: "Rendering Lists"
description: ""
icon: "article"
date: "2023-11-14T22:19:12+01:00"
lastmod: "2023-11-14T22:19:12+01:00"
draft: false
toc: true
---

## List with map function

```jsx
const people = [
    {id: 1, name: 'Susi'},
    {id: 2, name: 'Sepp'},
    {id: 3, name: 'Lola'}
];

export default function List() {
  const listItems = people.map((person, index) =>
    <li key={person.id}>{person.name}</li>
  );
  return <ul>{listItems}</ul>;
}
```

another example:

```jsx
import { Fragment } from 'react';

// ...

const listItems = people.map(person =>
  <Fragment key={person.id}>
    <h1>{person.name}</h1>
    <p>{person.bio}</p>
  </Fragment>
);
```


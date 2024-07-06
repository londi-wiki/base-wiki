---
weight: 999
title: "Context"
description: ""
icon: "article"
date: "2023-11-14T22:45:25+01:00"
lastmod: "2023-11-14T22:45:25+01:00"
draft: false
toc: true
---

## Use context instead of prop drilling

```jsx
// Define context
import { createContext } from 'react';
// ...
export const LevelContext = createContext(1);


// useContext
import { useContext } from 'react';
import { LevelContext } from './LevelContext.js';
// ...
const level = useContext(LevelContext);


// provide context
import { LevelContext } from './LevelContext.js';

export default function Section({ level, children }) {
    return (
        <section className="section">
            <LevelContext.Provider value={level}>
                {children}
            </LevelContext.Provider>
        </section>
    );
}
```
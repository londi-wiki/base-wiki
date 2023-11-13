---
weight: 999
title: "Ref and State"
description: ""
icon: "article"
date: "2023-11-09T08:28:28+01:00"
lastmod: "2023-11-09T08:28:28+01:00"
draft: false
toc: true
---

[react learning](https://react.dev/learn/referencing-values-with-refs)

## useRef

> When you want a component to “remember” some information, but you don’t want that information to trigger new renders, you can use a ref.
 
## Summary

- Refs are an escape hatch to hold onto values that aren’t used for rendering. You won’t need them often.
- A ref is a plain JavaScript object with a single property called current, which you can read or set.
- You can ask React to give you a ref by calling the useRef Hook.
- Like state, refs let you retain information between re-renders of a component.
- Unlike state, setting the ref’s current value does not trigger a re-render.
- Don’t read or write ref.current during rendering. This makes your component hard to predict.


## Example

```tsx
import { useRef } from 'react';

export default function Counter() {
    let ref = useRef(0);

    function handleClick() {
        ref.current = ref.current + 1;
        alert('You clicked ' + ref.current + ' times!');
    }

    return (
        <button onClick={handleClick}>
            Click me!
        </button>
    );
}
```

> Note that the component doesn’t re-render with every increment. Like state, refs are retained by React between re-renders. However, setting state re-renders a component. Changing a ref does not!

## useState

```tsx
import { useState } from 'react';

export default function Stopwatch() {
  const [startTime, setStartTime] = useState(null);
  const [now, setNow] = useState(null);

  function handleStart() {
    // Start counting.
    setStartTime(Date.now());
    setNow(Date.now());

    setInterval(() => {
      // Update the current time every 10ms.
      setNow(Date.now());
    }, 10);
  }

  let secondsPassed = 0;
  if (startTime != null && now != null) {
    secondsPassed = (now - startTime) / 1000;
  }

  return (
    <>
      <h1>Time passed: {secondsPassed.toFixed(3)}</h1>
      <button onClick={handleStart}>
        Start
      </button>
    </>
  );
}
```

## Ref vs state

| refs                                                                              | state                                                                                                                                                    |
|-----------------------------------------------------------------------------------| -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| useRef(initialValue)returns{ current: initialValue }                              | useState(initialValue)returns the current value of a state variable and a state setter function ([value, setValue])                                    |
| **Doesn’t trigger re-render when you change it.**                                 | Triggers re-render when you change it.                                                                                                                   |
| Mutable—you can modify and updatecurrent’s value outside of the rendering process. | “Immutable”—you must use the state setting function to modify state variables to queue a re-render.                                                      |
| You shouldn’t read (or write) thecurrentvalue during rendering.                   | [You can read state at any time. However, each render has its ownsnapshotof state which does not change.](https://react.dev/learn/state-as-a-snapshot) |


[Deep dive - how useRef works](https://react.dev/learn/referencing-values-with-refs#how-does-use-ref-work-inside)

## When to use refs

Typically, you will use a ref when your component needs to “step outside” React and communicate with external APIs—often a browser API that won’t impact the appearance of the component. Here are a few of these rare situations:

- Storing timeout IDs
- Storing and manipulating DOM elements, which we cover on the next page
- Storing other objects that aren’t necessary to calculate the JSX.

If your component needs to store some value, but it doesn’t impact the rendering logic, choose refs.


## Best practices for refs
Following these principles will make your components more predictable:
- Treat refs as an escape hatch. Refs are useful when you work with external systems or browser APIs. If much of your application logic and data flow relies on refs, you might want to rethink your approach.
- Don’t read or write ref.current during rendering. If some information is needed during rendering, use state instead. Since React doesn’t know when ref.current changes, even reading it while rendering makes your component’s behavior difficult to predict. (The only exception to this is code like if (!ref.current) ref.current = new Thing() which only sets the ref once during the first render.)

Limitations of React state don’t apply to refs. For example, state acts like a snapshot for every render and doesn’t update synchronously. But when you mutate the current value of a ref, it changes immediately.

```tsx
ref.current = 5;
console.log(ref.current); // 5
```

## Refs and the DOM
You can point a ref to any value. However, the most common use case for a ref is to access a DOM element. 
For example, this is handy if you want to focus an input programmatically. 
When you pass a ref to a ref attribute in JSX, like `<div ref={myRef}>`, 
React will put the corresponding DOM element into myRef.current. Once the element is removed from the DOM, React will update myRef.current to be **null**. 
You can read more about this in Manipulating the DOM with Refs.





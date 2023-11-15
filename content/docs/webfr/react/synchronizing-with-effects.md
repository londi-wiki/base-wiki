---
weight: 999
title: "Synchronizing With Effects"
description: ""
icon: "article"
date: "2023-11-15T17:33:48+01:00"
lastmod: "2023-11-15T17:33:48+01:00"
draft: false
toc: true
---

# How to write an Effect 

To write an Effect, follow these three steps:

1. Declare an Effect. By default, your Effect will run after every render.
2. Specify the Effect dependencies. Most Effects should only re-run when needed rather than after every render. For example, a fade-in animation should only trigger when a component appears. Connecting and disconnecting to a chat room should only happen when the component appears and disappears, or when the chat room changes. You will learn how to control this by specifying dependencies.
3. Add cleanup if needed. Some Effects need to specify how to stop, undo, or clean up whatever they were doing. For example, “connect” needs “disconnect”, “subscribe” needs “unsubscribe”, and “fetch” needs either “cancel” or “ignore”. You will learn how to do this by returning a cleanup function.

4. Let’s look at each of these steps in detail.

## Step 1: Declare an Effect 

```jsx
import { useEffect } from 'react';

function MyComponent() {
    useEffect(() => {
        // Code here will run after *every* render
    });
    return <div />;
}
```

Pitfall
By default, Effects run after every render. This is why code like this will produce an infinite loop:

```jsx
const [count, setCount] = useState(0);
    useEffect(() => {
    setCount(count + 1);
});
```


## Step 2: Specify the Effect dependencies

You can tell React to skip unnecessarily re-running the Effect by specifying an array of dependencies as the second argument to the useEffect call.

Example:

```jsx
  useEffect(() => {
    if (isPlaying) {
      console.log('Calling video.play()');
      ref.current.play();
    } else {
      console.log('Calling video.pause()');
      ref.current.pause();
    }
  }, [isPlaying]);
```

Note:

Notice that you can’t “choose” your dependencies. You will get a lint error if the dependencies you specified don’t match what React expects based on the code inside your Effect. This helps catch many bugs in your code. If you don’t want some code to re-run, edit the Effect code itself to not “need” that dependency.


The behaviors without the dependency array and with an empty [] dependency array are different:

```jsx
useEffect(() => {
  // This runs after every render
});

useEffect(() => {
  // This runs only on mount (when the component appears)
}, []);

useEffect(() => {
  // This runs on mount *and also* if either a or b have changed since the last render
}, [a, b]);
```
We’ll take a close look at what “mount” means in the next step.

#### Why was the ref omitted from the dependency array?

This Effect uses both ref and isPlaying, but only isPlaying is declared as a dependency:

```jsx
function VideoPlayer({ src, isPlaying }) {
  const ref = useRef(null);
  useEffect(() => {
    if (isPlaying) {
      ref.current.play();
    } else {
      ref.current.pause();
    }
  }, [isPlaying]);
```

This is because the ref object has a stable identity: React guarantees you’ll always get the same object from the same useRef call on every render. It never changes, so it will never by itself cause the Effect to re-run. Therefore, it does not matter whether you include it or not.



## Step 3: Add cleanup if needed

React will call your cleanup function each time before the Effect runs again, and one final time when the component unmounts (gets removed).

```jsx
useEffect(() => {
    const connection = createConnection();
    connection.connect();
    return () => {
      connection.disconnect(); // <= Cleanup function
    };
  }, []);
```

In production, you would only see "✅ Connecting..." printed once. Remounting components only happens in development to help you find Effects that need cleanup. 
You can turn off Strict Mode to opt out of the development behavior, but we recommend keeping it on. This lets you find many bugs like the one above.




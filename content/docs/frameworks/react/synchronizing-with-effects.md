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

# How to handle the Effect firing twice in development?

## Controlling non-React widgets

```jsx
useEffect(() => {
  const map = mapRef.current;
  map.setZoomLevel(zoomLevel);
}, [zoomLevel]);

useEffect(() => {
    const dialog = dialogRef.current;
    dialog.showModal();
    return () => dialog.close();
}, []);
```

## Subscribing to events

```jsx
useEffect(() => {
  function handleScroll(e) {
    console.log(window.scrollX, window.scrollY);
  }
  window.addEventListener('scroll', handleScroll);
  return () => window.removeEventListener('scroll', handleScroll);
}, []);
```

## Triggering animations

```jsx
useEffect(() => {
  const node = ref.current;
  node.style.opacity = 1; // Trigger the animation
  return () => {
    node.style.opacity = 0; // Reset to the initial value
  };
}, []);
```

## Fetching data

```jsx
useEffect(() => {
  let ignore = false;

  async function startFetching() {
    const json = await fetchTodos(userId);
    if (!ignore) {
      setTodos(json);
    }
  }

  startFetching();

  return () => {
    ignore = true;
  };
}, [userId]);
```

## Sending analytics

In development, logVisit will be called twice for every URL, so you might be tempted to try to fix that. We recommend keeping this code as is. Like with earlier examples, there is no user-visible behavior difference between running it once and running it twice. From a practical point of view, logVisit should not do anything in development because you don’t want the logs from the development machines to skew the production metrics. Your component remounts every time you save its file, so it logs extra visits in development anyway.

```jsx
useEffect(() => {
  logVisit(url); // Sends a POST request
}, [url]);
```

## Not an Effect: Initializing the application

Some logic should only run once when the application starts. You can put it outside your components:

```jsx
if (typeof window !== 'undefined') { // Check if we're running in the browser.
  checkAuthToken();
  loadDataFromLocalStorage();
}

function App() {
  // ...
}
```

## Not an Effect: Buying a product

```jsx
useEffect(() => {
  // 🔴 Wrong: This Effect fires twice in development, exposing a problem in the code.
  fetch('/api/buy', { method: 'POST' });
}, []);
```

```jsx
  function handleClick() {
    // ✅ Buying is an event because it is caused by a particular interaction.
    fetch('/api/buy', { method: 'POST' });
  }
```

# Example

```jsx
import { useState, useEffect } from 'react';

function Playground() {
  const [text, setText] = useState('a');

  useEffect(() => {
    function onTimeout() {
      console.log('⏰ ' + text);
    }

    console.log('🔵 Schedule "' + text + '" log');
    const timeoutId = setTimeout(onTimeout, 3000);

    return () => {
      console.log('🟡 Cancel "' + text + '" log');
      clearTimeout(timeoutId);
    };
  }, [text]);

  return (
    <>
      <label>
        What to log:{' '}
        <input
          value={text}
          onChange={e => setText(e.target.value)}
        />
      </label>
      <h1>{text}</h1>
    </>
  );
}

export default function App() {
  const [show, setShow] = useState(false);
  return (
    <>
      <button onClick={() => setShow(!show)}>
        {show ? 'Unmount' : 'Mount'} the component
      </button>
      {show && <hr />}
      {show && <Playground />}
    </>
  );
}
```


---

## Siehe auch

- → [Ref und State](/docs/frameworks/react/ref-and-state) – useRef und useState und wann welches
- → [Denken in React](/docs/frameworks/react/concept) – UI in Komponenten zerlegen und State richtig platzieren

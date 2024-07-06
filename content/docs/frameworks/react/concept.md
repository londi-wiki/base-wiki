---
weight: 999
title: "Concept"
description: ""
icon: "article"
date: "2023-11-15T15:39:32+01:00"
lastmod: "2023-11-15T15:39:32+01:00"
draft: false
toc: true
---

[thinking-in-react](https://react.dev/learn/thinking-in-react)

## Step 1: Break the UI into a component hierarchy

Depending on your background, you can think about splitting up a design into components in different ways:

- Programming—use the same techniques for deciding if you should create a new function or object. One such technique is the single responsibility principle, that is, a component should ideally only do one thing. If it ends up growing, it should be decomposed into smaller subcomponents.
- CSS—consider what you would make class selectors for. (However, components are a bit less granular.)
- Design—consider how you would organize the design’s layers.

## Step 2: Build a static version in React

To build a static version of your app that renders your data model, you’ll want to build components that reuse other components and pass data using props.

## Step 3: Find the minimal but complete representation of UI state

Which of these are state? Identify the ones that are not:

- Does it remain unchanged over time? If so, it isn’t state.
- Is it passed in from a parent via props? If so, it isn’t state.
- Can you compute it based on existing state or props in your component? If so, it definitely isn’t state!

What’s left is probably state.

### Props vs State

There are two types of “model” data in React: props and state. The two are very different:

- Props are like arguments you pass to a function. They let a parent component pass data to a child component and customize its appearance. For example, a Form can pass a color prop to a Button.
- State is like a component’s memory. It lets a component keep track of some information and change it in response to interactions. For example, a Button might keep track of isHovered state.

Props and state are different, but they work together. A parent component will often keep some information in state (so that it can change it), and pass it down to child components as their props. It’s okay if the difference still feels fuzzy on the first read. It takes a bit of practice for it to really stick!

## Step 4: Identify where your state should live

For each piece of state in your application:

1. Identify every component that renders something based on that state.
2. Find their closest common parent component—a component above them all in the hierarchy.
3. Decide where the state should live:
   1. Often, you can put the state directly into their common parent.
   2. You can also put the state into some component above their common parent.
   3. If you can’t find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common parent component.


## Step 5: Add inverse data flow

Pass functions for state change events like this:

```jsx
// FilterableProductTable
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />
// ...

// Searchbar
    <input
        type="text"
        value={filterText}
        placeholder="Search..."
        onChange={(e) => onFilterTextChange(e.target.value)} />
// ...
```
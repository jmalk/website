---
title: State Management in React
tags: learning
---
# State Management in React

## React itself

React includes some ways to manage state, so depending on what your app does, you might not need any extra state management tools.

### useState

Direct access to state is limited to a single component. If other child components need it, it can be passed down. If other components (parents, siblings or cousins) need it, you'll have to [lift the state up](https://beta.reactjs.org/learn/sharing-state-between-components) until it can be shared between them as props.

### useReducer

Like useState, this hook stores some state for you, and ties that state to a particular component. Like Redux, you update the state by dispatching actions, which in turn a call to a reducer function, which works out how to update state based on that action:

```
(state, action) => newState
```

This is very different to the simple `setState(newState)` call of the `useState` hook.

What's the difference between Redux and useReducer then?

- useReducer is not limited to just one
- useReducer is not global, it's tied to a particular component
- useReducer doesn't support middleware (TODO: check if still true!) and so is not good for when we want side effects either

QUESTION: Is there a Redux DevTools equivalent for this? Also worthy looking into debugging experience of other popular tools.


### useContext

useContext is not a state management tool, but it is often used in conjunction with them.

It allows child components to access state easily, without the need for passing the same piece of data through many layers of components as props (AKA prop drilling).

Using context to hold the state of a reducer in the root of your app makes it global, and so seems very similar to Redux.

QUESTION: What's the difference between useContext + useReducer and Redux?

## Redux

Redux makes a single store for all of your application state, and makes it available to all components in the app.

### State for server data

Redux Toolkit now includes [RTK Query](https://redux-toolkit.js.org/rtk-query/overview). If you're using Redux and also want to handle data fetching and caching, you can use it to take care of that rather than implementing it yourself. If you don't need Redux for other types of state management, and just want the server data taking care of, you might be better off with a tool dedicated only to that, like [Tanstack Query](https://tanstack.com/query/latest).

## Recoil

Key points:

- Share state flexibly
- Derived data
- App-wide observation

Something Recoil handles well that Context does not, is when your app will need some unknown number of blobs of state. If your app needs some known large number of blobs of state, you can use a large number of Context Providers for them all. But if you don't know exactly what that large number is ahead of time, Recoil might be better for you.

Recoil is very flexible. It doesn't impose the same limitations on you as `useState`. Flexibility can allow you to quickly build a ball of mud though, sometimes you may appreciate a more structured framework to code within, even if it does sometimes force you to do things a certain way.

Interdependent state is hard to manage - wherever possible we'd much rather derive values from existing state, rather than introduce new bits of state that must be kept in sync with existing state.

Recoil has selectors, which let you derive state from some of your atoms. This allows you to build up a graph of atoms and selectors, to get values to then display in your UI. But, importantly, the shape of your atoms graph is completely separate to the shape of your component tree.

Atoms and selectors present the same interface, so you can call them interchangeably from your components.

Any selector can be async! Return a promise from a selector and they take care of the rest.

`useTransactionObservation` to watch for any React commit that happens due to a Recoil state change.

## Jotai

## Zustand

Zustand is very lightweight, and kind of nifty. It's API is like:

import { create } from "zustand";

const useMyStoreHook = create((set) => {
  // big object in which you define all your state as properties, and methods to change those properties.
  // The methods to change the properties call `set` to do so.
});

Then in your components you call that useMyStoreHook to get access to the properties and methods. And because it's a hook, you can import it in any component, so the store is global.

Similar to Redux - global state stores subscribed to via selectors.

Question: Stores? Plural?

Creates a custom hook for you to use in your app.

Seems to combine really well with TypeScript because the state and functions to update that state all go into the call to `create<Store>`. You define the type for your store, and TypeScript shouts at you if the call to create isn't matching it.

It's tiny! 1.5kb. Non-trivial userbase. API is tightly defined - you can't do whatever you feel like with the state.

But it is so small that it leaves you with decisions to make, like whether or not to use Immer to enforce not mutating state.

It ships with an optional redux middleware, so if you love the redux API you can use Zustand in a very similar way. It even integrates with Redux Devtools.

## React Query

## State Machines

## References

- [The new wave of React state management](https://frontendmastery.com/posts/the-new-wave-of-react-state-management/)
- [HackerNews discussion of The new wave of React state management](https://news.ycombinator.com/item?id=31959289)
- [Blogged Answers: Why React Context is Not a "State Management" Tool (and Why It Doesn't Replace Redux)](https://blog.isquaredsoftware.com/2021/01/context-redux-differences/) by Mark "acemarke" Erikson
- [Redux vs useReducer](https://www.robinwieruch.de/redux-vs-usereducer/) by Robin Wieruch
- [React Docs Beta](https://beta.reactjs.org/learn)
- Recoil Deep Dive video
- https://tkdodo.eu/blog/working-with-zustand
- [YouTube: Mastering TypeScript State using Zustand](https://www.youtube.com/watch?v=sqTPGMipjHk) by Jack Herrington


# React State Management

## React Hooks

- useState and useReducer hooks both store state with a component
- useState lets you set state directly
- You must define a reducer for useReducer to use: `(currentState, action) => newState`
- If components need to share state, it must be lifted to their nearest common ancestor

## React Context

- Not a state management tool
- Often used with state management
- Store data, put a provider in your tree, any child can access it
- Components that read from it will re-render when it changes, so you might want lots of providers to separate out independent state

## Uni-directional

Events => Actions => State => UI

The UI presents ways for a User to trigger new events, completing a cycle.

### Redux

- Redux Toolkit is strongly recommended
- Put all your state together in a store
- Use slices to make sub-groups within it, if you want
- State is not set directly
- A reducer works out what new state is, based on action, just like in React's useReducer hook
- Handles Async stuff now
- Tangent: The `reduce` function takes a reducer. The current state is the result of all actions being applied to starting state
- This enables time-travel debugging
- Difference between this and React State + Context? It's single and global.

### Zustand

- A bit like redux in that it's single and global
- Can be made a lot like Redux if you want - they supply a way to use it with a reducer
- Extremely flexible and unopinionated
- Plays nicely with TypeScript. You define the Type of your store up front, forcing you to think about what you're storing and how it might be changed

## Atomic

Little blobs of state called "Atoms" which are composed as you wish.

Tangent: Derived state. Wherever possible, you want to _avoid_ storing state. For example, the average high temperature of next week's daily weather forecasts can be calculated from the high temperature of each day. So store the days in state but not the weekly average! (If performance is a concern, `useMemo`.)

If you need to derive some state from two or more atoms, make a selector that depends on them. Then your components can depend on that selector to get the value they care about.

Multiple components can depend on the same atom or selector. This means that if you have two components far apart in your UI Tree that both care about average high temperature, that state doesn't have to be moved to the root of your app.

### Recoil

- Described as "experimental"
- Actively maintained
- Gives a `useRecoilState` hook from both atoms and selectors: Easy to refactor between the two types of value

### Jotai

- "A model inspired by Recoil"
- Everything is Atoms (including what Recoil calls selectors)

TODO: Example of Atomic State code would be nice

## Server State

## State Machines

## Complexities of Next 13 App

## Questions

- Is RTKQuery worth considering against React-Query?

---
title: React Hooks
tags: learning
---
# React Hooks

## Why?

Let you use features that used to be class-based without writing a class. Classes require you to understand `this` and binding.

They let you write reusable stateful logic. They do not need you to change your component hierachy to do this.

Grouping business logic by where it falls in the component lifecycle can result in messy code. Unrelated concepts get bundled together. Hooks allow you to split things into genuinely related functionality.

## General

- Only call hooks at the top level, not inside loops, conditions or nests.
- Call hooks inside function components, or your own custom hooks. Nowhere else!
- `eslint-plugin-react-hooks` takes care of both of the above.

## State

- Add local state to a component, preserved between re-renders.

## Effect

Short for side effect! Data fetching, manually changing the DOM etc.

Effect happens after the DOM changes are done.

The callback to `useEffect` can return a function to be called when the component unmounts. e.g. a subscription can be unsubscribed.

You can skip effects. Pass an array of variables as the second arg to `useEffect`. It will only run the effect when the value of at least one of those variables has changed.

## Custom Hooks

Extract hooks you want to share into a new function. By convention we start custom hooks' names with `use` for readability (once you know that convention) and to enable linter support.


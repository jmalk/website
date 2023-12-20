---
title: Private Class Features in JavaScript and TypeScript
tags: learning
---
# Private Class Features in JavaScript and TypeScript

## Terminology

- Field: A variable on a class.
- Method: A method on a class.
- Member: A field or method on a class.
- Private: Something which cannot be accessed by code outside of the class.
- Public: The opposite of private; something which can be accessed by code outside of the class.

## In JavaScript

JavaScript uses hash names like `#privateField` or `#privateMethod` to mark private members.

## In TypeScript

TypeScript uses keywords to mark members like `private height` or `protected width`. Members are public by default. If you want to be explicit, you can specify that with `public`.

# TypeScript Rules of Thumb

- Don't feel obliged to explicitly type everything. e.g. `const myString: string = "hello"` is unnecessary. (Source: [TS Handbook, Type annotations on variables](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-annotations-on-variables)
- Use interfaces, until you need some specific feature of types. (Source: [TS Handbook, Differences between type aliases and interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)
- Avoid Enums unless you're sure you need one. A union will give you value-checking and auto-completion anyway. (Source: [TS Handbook, Enums](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#enums))

---
title: Mocking and Spies in Jest
tags: learning
---
# Mocking and Spies in Jest

## Questions I have

- What exactly do the different reset functions do?
- How do you mock out the implementation of another function within the project?
- When does stuff in `__mocks__` get used?
- How do you parameterise stuff in `__mocks__`?

## Mocks

Calling `jest.fn()` creates a mock for you.

A mock keeps a record of its calls and the values returned to those calls (`myMock.mock.results`).

You can make a mock return something other than `undefined` using `myMock.mockReturnValue(true)`.

## What's the difference between a mock and a spy?

According to [Jests' Mock Function API docs](https://jestjs.io/docs/mock-function-api), 'Mock functions are also known as "spies"'.

## How do you mock out the implementation of a function from a node module?

You can mock the whole module by importing it, then calling `mock` on the module's name, then providing return values for the functions your code calls.

```
const { getPikachu } = require('./index');
const axios = require('axios').default;

jest.mock('axios');

describe('getPikachu', () => {
  beforeEach(() => {
    axios.get.mockResolvedValue({data: {name: 'blastoise'}});
  });

  it(`actually returns "blastoise" because we've mocked the get request`, async () => {
    const result = await (getPikachu());

    expect(result).toBe('blastoise');
  });
});
```


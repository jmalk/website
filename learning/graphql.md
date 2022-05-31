---
title: GraphQL
tags: learning
---
# GraphQL

- Top Tip: When using a playground, `Ctrl + Space` triggers autocomplete even if you haven't typed anything
- Federation?

## Query syntax

- [Queries and Mutations](https://graphql.org/learn/queries/)

### Fields

Basic object traversal. Note that getting single values and getting arrays looks the same in your query, you have to check what to expect in the Schema of the endpoint you're using.

```
{
  hero {
    name
  }
}
```

returns

```
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```

### Arguments

You can pass arguments to pick particular bits of data, do transforms on values server-side, etc. Note that in the following example `METER` is part of an enumeration. This is one of the data types GraphQL supports.

```
{
  human(id: "1000") {
    name
    height(unit: METER)
  }
}
```

returns

```
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "height": 1.72
    }
  }
}
```

### Aliases

In the above example, you would not be able to query for height in both meters and feet.

```
{
  human(id: "1000") {
    name
    height(unit: METER)
    height(unit: FOOT)
  }
}
```

The name of the property would get used twice in the result and you wouldn't know which was which.

This is where aliases come in, you can query for a property multiple times, and give each one a different name:

```
{
  human(id: "1000") {
    name
    meterHeight: height(unit: METER)
    footHeight: height(unit:FOOT)
  }
}
```

returns

```
{
  "data": {
    "human": {
      "name": "Luke Skywalker",
      "meterHeight": 1.72,
      "footHeight": 5.6430448
    }
  }
}
```

### Fragments

Fragments let you define reusable chunks of query. You can re-use them multiple times within a query, which can be useful for getting data about lots of different items in one request.

For example, we can compare the heroes of two different films like so:

```
{
  empireHero: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  jediHero: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  appearsIn
}
```

Fragments can use variables from the query that is using the fragment.

- [ ] Variables still to come. Maybe could re-order these sections if Variables don't depend on understanding Fragments.

### Operation name

Up until now, we've unknowingly been working with something called "query shorthand syntax". Because we haven't specified, it is assumed that our operation is a query, and it has no name.

But there are other types of operation. And when you are debugging it can be useful to give names to your operations so you can tell them apart quickly.

To improve this, we can specify an operation type of `query`, `mutation` or `subscription`, and give our operation a name:

```
query HeroName {
  hero {
    name
  }
}
```

### Variables

Just like passing arguments to functions, it is useful to be able to pass variables to queries. Defaults can be put after an equals sign, like in JavaScript.

```
query HeroNameAndFriends($episode: Episode = JEDI) {
  hero(episode: $episode) {
    name
  }
}
```

In code, we might pass these GraphQL variables into a function that does the legwork for us. In a GraphQL playground, you get a query variables pane to write JSON into. For the above query that might look like

```
{
  "episode": "EMPIRE"
}
```

All declared variables are either "scalars, enums or input object types".

- [ ] What are scalars, enums and input object types?
- [ ] Exclamation marks indicate that a variable is mandatory, but I can't find out if that's specified in the query string or just the docs?

### Directives

Directives allow you to use a little bit of control flow in your queries. You can make it so that certain fields are only requested if a Boolean is true.

```
query Hero($episode: Episode, $withFriends: Boolean!) {
  hero(episode: $episode) {
    name
    friends @include(if: $withFriends) {
      name
    }
  }
}
```

with variables

```
{
  "episode": "JEDI",
  "withFriends": false
}
```

returns

```
{
  "data": {
    "hero": {
      "name": "R2-D2"
    }
  }
}
```

If you were to set withFriends to true, you'd also get back the following inside the hero value:

```
"friends": [
  {
    "name": "Luke Skywalker"
  },
  {
    "name": "Han Solo"
  },
  {
    "name": "Leia Organa"
  }
]
```

### Mutations

Technically any GraphQL request could write data as well as read it, but by convention we use `mutation` to label requests that are doing writes. If you'd like some data back after the write you can specify it in the query string.

It's important to note that operations are done in series for mutations as opposed to parallel for queries. This prevents race conditions.

### Inline Fragments 

The GraphQL type system lets you define Union and Interface types. This means that if we make a query for a Star Wars `Character` we don't know whether we'll get a `Droid` or a `Human` back. This means we don't know what keys are available to us on the data. To save multiple round trips, we can specify different cases using "Inline Fragments". Here's an example:

```
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
    ... on Human {
      height
    }
  }
}
```

This means: Get me the hero of the episode I've specified. I know that `name` exists on all `Character`s, so give me that regardless. If the hero is a `Droid` give me their `primaryFunction`. If the hero is a `Human` give me their `height`.

#### Meta Fields

Sometimes a client won't be able to tell what type of object the returned data has come from. If the returned data only has a `name`, we can't tell whether it's the name of a Human, Droid, or Starship. To get around this, clients can request the `__typename` of the object being requested. For example

```
{
  search(text: "an") {
    __typename
    ... on Human {
      name
    }
    ... on Droid {
      name
    }
    ... on Starship {
      name
    }
  }
}
```

returns

```
{
  "data": {
    "search": [
      {
        "__typename": "Human",
        "name": "Han Solo"
      },
      {
        "__typename": "Human",
        "name": "Leia Organa"
      },
      {
        "__typename": "Starship",
        "name": "TIE Advanced x1"
      }
    ]
  }
}
```

and as we can see it'd be impossible to tell what type each object was without those `__typename`s. There are other meta fields available in GraphQL.

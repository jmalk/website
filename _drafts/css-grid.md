# CSS Grid

## Resources

- [CSS Tricks: Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Web Dev Simplified: Learn CSS Grid in 20 Minutes (YouTube)](https://www.youtube.com/watch?v=9zBsdzdE4sM)

## Terminology

Grid container wraps all grid items.

Grid gaps sit between items.

Grid tracks are the imaginary lines that define the edges of each item.

## Container

`display: grid;`

Simple as that. This won't make any difference to how things look on its own.

`grid-template-columns` can take a wide range of sizes - pixels, percent, ems etc.

We can use the "fraction" unit `fr` to let our columns be a bit more flexible in size.

We can use repeats like `grid-template-columns: repeat(3, 200px);` to save having to type out `200px 200px 200px`.

The `grid-template-rows` property works in the same way but applies to the rows of our grid, not the columns.

`grid-auto-rows` allows us to define a default value; the size will get used when no value is specified for the row in `grid-template-rows`. And the size will be used for all rows if no `grid-template-rows` is specified at all.

The `minmax` function is a good friend for defining rows and columns.

`grid-row-gap` defines space between rows. `grid-column-gap` defines space between columns. Same for both? Use `grid-gap`.

Finally, `grid-template-areas` lets you name a bunch of areas. Items can then declare which of these they are by saying `grid-area: [area-name];`

## Items

`grid-column-start` and `grid-column-end` let you define how many columns of a grid an item should span. Can use negative numbers to count from end. Can combine them into `grid-column: 1 / 3;` instead of separate properties.

`span` is a keyword you can use like `grid-column: span 2;`.


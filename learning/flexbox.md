---
title: Flexbox
tags: learning
---
# Flexbox

Flexbox allows us to arrange items in one dimension.

## Display Flex

When you set `display: flex;` on an element, it becomes a Flex Container, and its immediate children become Flex Items.

You can also use `display: inline-flex;`. It creates a container that is only as wide as it needs to be for its content, rather than taking up the full width of the page.

## Flex Direction

The default `flex-direction` for a flex container is `row`. You can set it explicitly, or change it to `flex-direction: column;` to display flex items vertically instead of horizontally. You can also set it to `row-reverse` to display items right-to-left, or `column-reverse` to display items bottom-to-top.

The Main Axis is parallel with the flex direction: 

- ➡️ `row`: left-to-right 
- ⬅️ `row-reverse`: right-to-left 
- ⬇️ `column`: top-to-bottom 
- ⬆️ `column-reverse`: bottom-to-top 

The Cross Axis is perpendicular to the main axis.

In a row, the items will expand vertically to fill the height of the container. In a column, they expand horizontally.

- [x] Q: Does the cross axis also have a direction or is it just a line? It does in the sense that if you use `wrap-reverse` (see below) items will be arranged going bottom-to-top or right-to-left.

## Wrapping

Flex items in a row might not be the width you set them to be! If the total width of flex items is wider than their container, they'll be shrunk to fit in it.

This is the default behaviour and it's called `flex-wrap: nowrap;`.

If you set `flex-wrap: wrap;` the items will be allowed to break onto multiple lines, and they'll be allowed to take up the full `width` you set. By default their height will be split up evenly between the number of rows formed by the wrapping. e.g. 100px high, wrapping causes 4 rows, each row will be 25px high.

`wrap-reverse` will actually reverse with respect to the _cross_ axis.

## Flex Flow Shorthand

The `flex-flow` shorthand combines `flex-direction` and `flex-wrap`. For example,

```
flex-flow: row-reverse wrap;
```

is equivalent to

```
flex-direction: row-reverse;
flex-wrap: wrap;
```

## Ordering

You can alter the order items appear in without changing their order in the DOM.

By default every item has `order: 0;`.

If you pick an item and set it to `order: 1;` it will appear after all the other items in the flow. So if you want your third item to appear after your seventh, you'll need something like:

```
.box3 {
  order: 1;
}

.box8 {
  order: 2;
}

.box9 {
  order: 2;
}

/* etc. for all remaining boxes */
```

Negative numbers are valid and work as you might expect.

Selecting something to copy-paste it will get absolutely messed up by re-ordering.

## Alignment and Centering

To define where items should sit along the main axis, we use `justify-content`. By default it's `flex-start`, and that's why all the items are bunched up on the left in a row.

There's a tricky point with `flex-direction` and alignment. A block element automatically takes up the whole width of your page, but will only take up as much height as the elements inside it need. This means that for a `row`, you will more commonly see the effect of whatever `justify-content` you choose to set. That is to say, if you set it as `space-evenly`, there will be some spare space distributed between all the items, and they'll be neatly spaced out across the screen.

If you're working with a column, though, it will only grow as tall as it needs to be to fit all the child elements. There won't be any spare space to distribute. This means that when you change `justify-content` to something interesting like `center` or `space-around`, nothing will change as there's no space to play with. To change this, you would need to set a `min-height` on the column that is greater than the height of all it's children.

One way to vertically center things in CSS is with `justify-content: center;` on a container with `flex-direction: column;`.

Setting `align-items` on a container determines where all the flex items will sit within the container. You can override it for a given item by setting `align-self` on the item.

## Flexbox Sizing with the flex property

How greedy should each flex item be with the amount of space it takes up?

`flex: 1;` makes all items grow to the same size when there's extra space. Giving one item in the container a larger number will make it take up a larger amount of the extra.

Even when there is not enough space for all your items, higher numbers will be 'greedier' in the space they take up.

## Grow, shrink and basis

`flex` is shorthand for setting both `flex-grow` and `flex-shrink`.

`flex-grow` is how extra space gets divided among items.

`flex-shrink` is how much of its space an item should _give up_ when there's not enough space.

`flex-basis` is how big you would make an item (in the main-axis direction) in an ideal world.

The default `flex-grow` is 0. If you don't specify, it'll just stay at it's defined `flex-basis`.

Q: Is the above point generally true, or only in cases where `flex-basis` is specified?

---

## Summary

### Flex Container Properties

- `display: flex | inline-flex;`
- `flex-direction: row (default) | row-reverse | column | column-reverse;`
- `flex-wrap: nowrap (default) | wrap | wrap-reverse;`
- `justify-content: flex-start (default) | flex-end | center | space-between | space-around | space-evenly`
- `align-items: ...`
- `align-content: stretch (default) | flex-start | flex-end | center | space-between | space-around`

### Item Properties

- `order: <number>;`
- `align-self: ...`

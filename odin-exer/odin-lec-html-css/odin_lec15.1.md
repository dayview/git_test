# Introduction to Flexbox

> This is supplementary content to #13, #14, and #15.

CSS is comprised of many different layout algorithms, known officially as *layout modes". Each layout mode is its own little sub-language with CSS.

The default layout mode is ***flow layout***, but we can opt-in to `flexbox` by changing the `display` property on the parent container:

`display: block` is arranged vertically in a column.
`display: flex` is arranged horizontally in a row.

When we flip `display` to `flex`, we create a *flex formatting context*. This means that, by default, all children will be positioned according to the `flexbox` layout algorithm.

> The default *flow* layout is meant to create digital documents; it's essentially the ***Microsoft Word*** layout algorithm. Headings and paragraphs stack *vertically* as blocks, while things like text, links, and images sit inconspicuously within these blocks.

> **So, what problem does `flexbox` solve?** `flexbox` is all about arranging a group of items in a row or column, and giving us a ridiculous amount of control over the distribution and alignment of those items. As the name suggests, `flexbox` is all about *flexibility*. We can control whether items `grow` or `shrink`, how the extra space is `distributed`, and more.

### flex-direction
As mentioned, `flexbox` is all about controlling the distribution of elements in a row or column. By default, items will stack side-by-side in a row, but we can flip to a *column* with the `flex-direction` property: `row` or `column`.

`flex-direction: row` <br>
<s> Hello | to | the | world | </s> <br>
--------------------------> **primary axis**

`flex-direction: column` <br>
| Hello <br>
| to <br>
| the <br>
| world <br>
| <br>
| <br>
V <br> **primary axis**

With `flex-direction: row`, the ***primary axis*** runs horizontally, from left-to-right. When we flip to `flex-direction: column`, the **primary axis** runs *vertically*, from top-to-bottom.

In flexbox, **everything is based on the primary axis**. The algorithm doesn't care about vertical/horizontal, or even rows/columns. All of the rules are structured around this primary axis, and the *cross axis* that runs perpendicularly.

When we learn the rules of flexbox, we can switch seamlessely from *horizontal layouts* to *vertical* ones. All of the rules adapt automatically. This feature is unique to the flexbox layout mode.

The children will be positioned by default according to the following two rules:
1. **Primary axis**: Children will be bunched up at the start of the container
2. **Cross axis**: Children will stretch out to fill the entire container

**FLEX ROW**
```text
┌─────────────────────────────────────────────┐
│                                  ↑          │
│                                  │          │   
│   ←────── Primary Axis (Main Axis) ──────→  │
│                                  │          │
│   ┌────┐  ┌────┐  ┌────┐         │          │
│   │  1 │  │  2 │  │  3 │         │          │
│   └────┘  └────┘  └────┘         │          │
│                              Cross Axis     │
│                                  │          │
│                                  ↓          │
└─────────────────────────────────────────────┘
```
**FLEX COLUMN**
```text
┌────────────────────────────────────────────┐
│                                            │
│                                            │
│                  ┌────────────┐            │
│                  │     1      │            │
│                  └────────────┘            │
│                                            │
│  ←Cross Axis→    ┌────────────┐            │
│                  │     2      │            │
│                  └────────────┘     ↑      │
│                                     │      │
│                  ┌────────────┐     │      │
│                  │     3      │  Primary   │
│                  └────────────┘   Axis     │
│                                     │      │
│                                     ↓      │
└────────────────────────────────────────────┘
```

In flexbox, we decide whether the primary axis runs horizontally or vertically. This is the root that all flexbox calculations are pegged to.

### Alignment
We can change how children are distributed along the primary axis using the `justify-content` property:

```css
flex-direction: row | column;
justify-content: flex-start | center | flex-end | space-between | space-around | space-evenly;
```

When it comes to the primary axis, we don't generally think in terms of aligning a singgle child. Instead, it's all about the *distribution  of the group*.

We can bunch all the items up in a particular spot (with `flex-start`, `center`, and `flex-end`), or we can spread them apart (with `space-between`, `space-around`, and `space-evenly`).

For the cross axis, things are a bit different. We use the `align-items` property:

```css
flex-direction: row | column;
justify-content: flex-start | center | flex-end | space-between | space-around | space-evenly;
align-items: stretch | flex-start | center | flex-end | baseline;
```

With `align-items`, we have some of the same options as `justify-content`, but there isn't a **perfect overlap**.

```css
.container-1 {
    justify-content: /* exclusively has */ space-between, space-around, and space-evenly;
}

.container-2 {
    align-items: /* exclusively has */ stretch, and baseline;
}

.container-3 {
    justify-content: /* and */ flex-start, center, and flex-end;
    align-items: /* have */ flex-start, center, and flex-end;
}
```

Unlike `justify-content` and `align-items`, `align-self` is applied to the **child-element**, not the container. It allows us to change the alignment of a specific child along the cross axis:
```css
flex-direction: row | column;
align-self: stretch | flex-start | center | flex-end | baseline;
```

`align-self` has all the same values as `align-items`. They change the exact same thing, as `align-items` is a convenient shoorthand that automatically sets the alignment on all the children **at once**.

#### Content vs. Items
In flexbox, items are distributed along the primary axis. By default, they're nicely lined up, side-by-side, like a kebab. (A straight horizontal line that **skewers all of the children**).

The cross axis is different, though. A straight vertical line will only ever intersect **one** of the children.

It's less like a kebab, and more like a group of bite-sized hotdogs.

With the bite-sized hotdogs, each item can move along its stick **without interfering** with any of the other items.

By contrast, with our primary axis skewering each sibling, a single item **can't move along** its stick **without bumping into its siblings**!

**This is the fundamental difference between the primary/cross axis**. When we're talking about alignment in the cross axis, **each item can do whatever it wants**. In the primary axis, though, we can only think about how to **distribute the group**.

That's why there's no `justify-self`. What would it mean for that middle piece to set `justify-self: flex-start`? There's already another piece there!

With all of this context in mind, let's give a proper definition to all four terms we've been talking about:

`justify`: to position something along the ***primary axis*** <br>
`align`: to position something along the ***cross axis*** <br>
`content`: a **group of "stuff"** that can be ***distributed*** <br>
`items`: single items that can be positioned ***individually***

And so: we have `justify-content` to ***control the distribution of the group along the primary axis***, and we have `align-items` to ***position each item individually along the cross axis***. These are the two main properties we use to manage layout with Flexbox.

> There's no `justify-items` for the same reason that there's no `justify-self`; when it comes to the primary axis, we *have to think of the items* as a **group**, as **content** that can be **distributed**.

### flex-basis
In a flexbox row, `flex-basis` does the same thing as `width`. In a flexbox column, `flex-basis` does the same thing as `height`.

As we've learned, everything in Flexbox is pegged to the **primary/cross axis**. For example, `justify-content` will distribute the children along the primary axis, and it works exactly the same way whether the primary axis runs horizontally or vertically.

`width` and `height` don't follow this rule, though! `width` will always affect the horizontal size. It doesn't suddenly become `height` when we flip `flex-direction` from `row` to `column`.

And so, the flexbox authors created a generic size property called `flex-basis`. It's like `width` or `height`, but pegged to the primary axis, like everything else. It allows us to set the *hypothetical size* of an element in the primary-axis direction, regardless of whether that's horizontal or vertical.

Like we saw with `width`, `flex-basis` is more of a suggestion than a hard constraint. At a certain point, there just isn't enough space for all of the elements to sit at their assigned size, and so they have to compromise, in order to avoid an overflow.

> **However... they're not exactly the same!** <br>
In general, we can use `width` and `flex-basis` interchangeably in a flexbox row, but there are some exceptions. For example, the `width` property affects replaced elements like images differently than `flex-basis`. Also, `width` can reduce an item below its *minimum* size, while `flex-basis` can't.

### flex-grow
By default, elements in a flexbox content will shrink down to their minimum comfortable size along the primary axis. This often creates extra space.

We can specify how that space should be consumed with the `flex-grow` property:
```css
flex-direction: row | column;
flex-grow: 0 (default) | 1;
```

The default value for `flex-grow` is 0, which means that growing is opt-in. If we want a child to gobble up any extra space in the container, we need to explicitly tell it so.

***What if multiple children set `flex-grow`***? In this case, the extra space is divided proportionally between children based on their `flex-grow` value.

When incremeting/decrementing each child:
1. The first child wants 1 unit of extra space, while the second child wants 1 unit. That means the total # of units is 2 (1 + 1). Each child gets a proportional share of that extra space.

> This accounts for any positive value n of either child. <br><br> The first child wants 2 units of extra space, while the second child wants 1 unit. That means the total # of units is 3 (2 + 1). Each child gets a proportional share of that extra space.

2. When a single child is given a positive `flex-grow` value, it gobbles up all of the extra space. In this case, it doesn't matter what the number is: 1 and 1000 have the same effect.

3. With no `flex-grow`, both children shrink down to their minimum comfortable size, and the extra space isn't distributed.

### flex-shrink
In most of the examples we've seen so far, we've had extra space to work with. But what if our children are *too big* for their container?

```css
.container-1 {
    flex-basis: 300px;
}

.container-2 {
    flex-basis: 150px;
}
```

When the container width shrinks from 600 to 0, both items shrink proportionally. The first child is always 2x the width of the second child.

As a friendly reminder, `flex-basis` serves the same purpose as `width`. We'll use `flex-basis` because it's conventional, but we'd get the exact same result if we used `width`!

`flex-basis` and `width` set the elements' *hypothetical size*. The flexbox algorithm might shrink elements below this desired size, but by default, they'll always scale together, preserving the ratio between both elements.

Now, what if we *don't* want our elements to scale down proportionally? That's where the `flex-shrink` property comes in.

When you shrink a container to `400px` with each two children with a hypothetical size of `250px`, the container needs to be at least `500px` wide to contain these children at their hypothetical size.

In thise case, we can't stuff `500px` worth of content into a `400px` bag! ***We have a deficit of 100px***. Our elements will need to give up `100px` total, in order for them to fit.

**The `flex-shrink` property lets us decide how that balance is paid**.

Like `flex-grow`, it's a ratio. By default, both children have `flex-shrink: 1`, and so each child pays 1/2 of the balance. They each forfeit `50px`, their actual size shrinking from `250px` to `200px`.

Now, let's suppose we crank that first child up to `flex-shrink: 3`.

We have a total deficit of `100px`. Normally, each child would play 1/2, but because we've tinkered with `flex-shrink`, the first element winds up paying 3/4 (`75px`), and the second element pays 1/4 (`25px`).

Note that the absolute values don't matter, **it's all about the ratio**. If both children have flex-shrink: 1, each child will pay 1/2 of the total deficit. If both children are cranked up to `flex-shrink: 1000`, each child will pay 1000/2000 of the total deficit. Either way, it works out to the same thing.

If you think about `flex-shrink`: we can call it as the "inverse" of `flex-grow`. They're two sides of the same coin where:
1. `flex-grow` controls how the *extra space is distributed* when the items are smaller than their container
2. `flex-shrink` controls how *space is removed* when the items are bigger than their container

This means that ***only one of these properties can be active at once***. If there's extra space, `flex-shrink` has no effect, since the items don't need to shrink.

And if the children are too big for their container, `flex-grow` has no effect, because there's no extra space to divvy up.

> Think of it as **two separate realms**.

### Preventing shrinking
Sometimes, we don't want some of our flexbox children to shrink.

When the container gets narrow, our two circles get squashed into gross ovals. What if we want them to stay circular?

We can do this by setting `flex-shrink: 0;`

When we set `flex-shrink` to 0, we essentially "opt out" of the shrinking process altogether. The flexbox algorithm will treat `flex-basis` (or `width`) as a hard minimum limit.

```html
<style>
    .item.ball {
        flex-shrink: 0;
    }
</style>

<div class="wrapper">
    <div class="item ball"></div>
    <div class="item stretch"></div>
    <div class="item ball"></div>
</div>
```
```css
body {
  background: hsl(210deg, 30%, 12%);
  color: hsl(0deg 0% 100%);
}
.wrapper {
  display: flex;
  gap: 8px;
}
.item {
  height: 32px;
  border: 2px solid hsl(210deg 8% 50%);
  background: hsl(210deg 15% 20%);
}
.item.stretch {
  /*
    Because this item is empty, it
    has a default hypothetical width
     of 0px. This isn't realistic,
     though; in a typical case,
     there would be content in here!
     And so we set a width of 300px
     to simulate it containing stuff.
  */
  width: 300px;
  flex-grow: 1;
  border-radius: 16px;
}
.item.ball {
  width: 32px;
  /*
    NOTE: We could prevent the circle
    from squishing into an oval by
    setting border-radius: 16px
    instead. I'm using percentages
    because it makes for a better
    demo. But even with a pixel-based
    radius, we still need
    flex-shrink: 0 to prevent the
    item from shrinking (give it a
    shot and see the difference!).
  */
  border-radius: 50%;
}
```

###  The mminimum size gotcha
When a container shrinks below a certain point, the **content overflows**!

`flex-shrink` has a default value of `1`, and we haven't removed it, so the search input should be able to shrink as much as it needs to! Why is it refusing to shrink?

In addition to the *hypothetical size*, there's another important size that the flexbox algorithm cares about: *the minimum size*.

The flexbox algorithm refuses to shrink a child below its minimum size. The content will overflow rather than shrink further, no matter how high we crank `flex-shrink`!

Text inputs have a default minimum size of `170px-200px` (it varies between browsers). That's the limitation we're running into above.

In other cases, the limiting factor might be the element's content. For example, when resizing a container with one having a larger/longer content vs. the other child, the minimum width is the length of the **longest unbreakable string of characters**.

However, we can redefine the minimum size with the `min-width` property.

By setting `min-width: 0px;` directly on the flexbox child, we tell the flexbox algorithm to overwrite the "built-in" minimum width. Because we've set it to `0px`, the element can shrink as much as necessary.

This same trick can work in flexbox columns with the `min-height` property (although the problem doesn't seem to come up as often).

> Proceed with caution: <br> It's worth noting that the built-in minimum size does serve a purpose. It's meant to act as a guardrail, to prevent something even worse from happening. <br><br> For example: when we apply `min-width: 0px;` to our text-containing flexbox children, things break in an even worse way.

### Gaps
`gap` allows us to create space *in-between* each flexbox child. This is great for things like navigation headers.

`gap` is relatively a new addition to the flexbox language, but it's been implemented across all modern browsers.

### Auto margins
The `margin` property is used to add space around a **specific element**. In some layout modes, like Flow and Positioned, it can even be used to center an element, with `margin: auto;`. Auto margins are much more interesting in flexbox.

Earlier, we saw how the `flex-grow` property can gobble up any extra space, applying it to a child.

**Auto margins will gobble up the extra space, and apply it to the element's margin**. It gives us precise control over where to distribute the extra space.

A common header layout features the logo on one side, and some navigation links on the other side.

Here's how we can build this layout using auto margins:
```html
<style>
  ul {
    display: flex;
    gap: 12px;
  }
  li.logo {
    margin-right: auto;
  }
</style>

<nav>
  <ul>
    <li class="logo">
      <a href="/">
        Corpatech
      </a>
    </li>
    <li>
      <a href="">
        Mission
      </a>
    </li>
    <li>
      <a href="">
        Contact
      </a>
    </li>
  </ul>
</nav>
```

The Corpatech logo is the first list item in the list. By giving it `margin-right; auto`, we gather up all of the extra space, and force it betwenen the 1st and 2nd item.

> There are lots of other ways we could have solved this problem: we could have grouped the navigation links in their own flexbox container, or we could have grown the first list item with `flex-grow`. <br><br> However, the auto-margins' solution treats the extra space as a resource, and deciding exactly where it should go.
```css
body {
  padding: 0;
}

nav {
  padding: 12px;
  border-bottom: 1px dotted
    hsl(0deg 0% 0% / 0.2);
}

ul {
  list-style-type: none;
  align-items: baseline;
  padding: 0px;
  margin: 0;
}

ul a {
  color: inherit;
  text-decoration: none;
  font-size: 0.875rem;
}

.logo a {
  font-size: 1.125rem;
  font-weight: 500;
}
```

### Wrapping
So far, all of our items have sat side-by-side, in a single row/column. The `flex-wrap` property allows us to change that.

Most of the time when we work in two dimensions, we'll want to use CSS Grid, but flexbox + `flex-wrap` definitely has its uses! This particular example showcases the "deconstructed pancake" layout, where 3 items stack into an inverted pyramid on mid-sized screens.

When we set `flex-wrap: wrap`, **items won't shrink below their hypothetical size**. At least, not when wrapping onto the next row/column is an option!

Given the metaphor earlier: with the idea of `flex-wrap: wrap`, we no longer have a single primary axis line that can skewer each item. Effectively, **each row acts as its own mini flex container**.

***Instead of one big skewer, each row gets its own skewer***.

All of the rules we've learned so far continue to apply, within this reduced scope. `justify-content`, for example, will distribute the two pieces on each stick.

But how does `align-items` work, now that we have multiple rows? The cross axis *could* intersect multiple items now!

Each row is its own mini flexbox environment. `align-items` will move each item up or down within the invisible box that wraps around each row.

But what if we want to *align the rows themselves*? We can do that with the `align-content` property.

* Given 4 items in a flex container, `flex-wrap: wrap` gives us two rows of stuff.

* Within each row, `align-items` lets us slide each individual child up or down;

* However, we have these two rows within a single Flexbox content! The cross axis will now intersect *two* rows, not *one*. And so, we can't move the rows individually, we need to distribute them as a *group*.

* Using our definitions from above, we're dealing with *content*, not *items*. But we're also still talking about the cross axis! And so, the property we want is `align-content`.

### Extra Details 
1. flex-start: items are packed at the start of the container
```text
┌─────────────────────────────────┐
│ [A] [B] [C]                     │  ← All extra space on the right
└─────────────────────────────────┘
```
```css
.container {
  display: flex;
  justify-content: flex-start;
}
```

2. center: items are packed in the center of the container

Use case: Centering a navigation menu, centering a card on a page
```text
┌─────────────────────────────────┐
│           [A] [B] [C]           │  ← Equal space on both sides
└─────────────────────────────────┘
```
```css
.container {
    display: flex;
    justify-content: center;
}
```

3. flex-end: items are packed at the end of the container

Use case: Right-align buttons or navigation links
```text
┌─────────────────────────────────┐
│                     [A] [B] [C] │  ← All extra space on the left
└─────────────────────────────────┘
```
```css
.container {
  display: flex;
  justify-content: flex-end;
}
```

4. space-between: items are evenly distributed with:
* first item at the start
* last item at the end
* equal space between items (NO space at edges)

Use case: Navigation bar where first item is a logo (left) and last item is user profile (right)
```text
┌─────────────────────────────────┐
│ [A]          [B]          [C]   │  ← Space BETWEEN items only
└─────────────────────────────────┘
```
```css
.container {
    display: flex;
    justify-content: space-between;
}
```

5. space-around: items are evenly distributed with:
* equal space around each item
* spaces at edges is half the space between items
```text
┌─────────────────────────────────┐
│  [A]       [B]       [C]        │  ← Half-space at edges
└─────────────────────────────────┘
   ↑         ↑         ↑
   1x       2x        2x       1x
```
```css
.container {
    display: flex;
    justify-content: space-around;
}
```

> Why half-space at edges? Each item gets equal space on both sides. The first item has 1 unit of space on its left, 1 unit on its right. The second item has 1 unit on its left (touching the first item's right space = 2 units total).

6. space-evenly: items are evenly distributed with:
* equal space everywhere, including at the edges

Use case: When you want perfectly even spacing, like a gallery or icon grid.
```text
┌─────────────────────────────────┐
│   [A]      [B]      [C]         │  ← Same space everywhere
└─────────────────────────────────┘
    ↑        ↑        ↑        ↑
   Equal   Equal   Equal   Equal
```
```css
.container {
    display: flex;
    justify-content: space-evenly;
}
```

| Value         | Visual              | Description                 |
| ------------- | ------------------- | --------------------------- |
| flex-start    | [A][B][C]           | Packed at start             |
| center        | [A][B][C]           | Packed in center            |
| flex-end      | [A][B][C]           | Packed at end               |
| space-between | [A]     [B]     [C] | Space BETWEEN (edges touch) |
| space-around  | [A]    [B]    [C]   | Half-space at edges         |
| space-evenly  | [A]   [B]   [C]     | Equal space everywhere      |

# Supplementary Materials
https://www.joshwcomeau.com/css/interactive-guide-to-flexbox/ <br>
https://css-tricks.com/snippets/css/a-guide-to-flexbox/#aa-basics-and-terminology (Parts 1-3 and 5) <br>
https://flexboxfroggy.com/
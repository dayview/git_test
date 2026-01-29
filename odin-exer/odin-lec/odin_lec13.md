# Growing and Shrinking

> What was covered last chapter: Positioning elements using flexbox, flex containers, flex items and layouting

> Overview of this chapter: The three properties that are defined by the `flex` shorthand, and how it is individually used

## The flex shorthand
The `flex` declaration is actually a shorthand for 3 properties that you can set on a flex item. These properties affect how flex items size themselves within their container. You've seen some shorthand properties before, but we haven't officially defined them yet.

> "Shorthand properties are CSS properties that let you set the values of multiple other CSS properties simultaneously. Using a shorthand property, you can write more concise (and often more readable) stylesheets, saving time and energy."

In this case, `flex` is actually a shorthand for `flex-grow`, `flex-shrink`, and `flex-basis`.

```css
div {
    flex: 1;
}
```

In the above snippet, `flex: 1` equates to: `flex-grow: 1`, `flex-shrink: 1`, `flex-basis: 0`.

### Flex-grow
`flex-grow` expects a **single number** as its value, and that number is used as the flex-item's "growth factor". When we applied `flex: 1` to every `div` inside our *container*, we were telling every `div` to **grow the same amount**.

The result of this is that every `div` ends up the **exact same size**. If we instead add `flex: 2` to just one of the `div`s, then that `div` would grow to *two times* the size of the others.

```html
<div class="flex-container">
    <div class="one"></div>
    <div class="two"></div>
    <div class="three"></div>
</div>
```
```css
.flex-container {
    display: flex;
}

/* this selector selects all divs inside of .flex-container */

.flex-container div {
    background: peachpuff;
    border: 4px solid brown;
    height: 100px;
    flex: 1 1 0%;
}

/* only div.two is selected here */
.flex-container .two {
    flex: 2 1 0%;
}
```

### Flex-shrink
`flex-shrink` is similar to `flex-grow`, but sets the "shrink factor" of a flex item. `flex-shrink` only ends up being applied if the size of all flex items is larger than their parent *container*.

For example, if our 3 `div`s from above had a width declaration like: `width: 100px`, and `.flex-container` was smaller than `300px`, our `div`s would have to ***shrink to fit***.

The default shrink factor is `flex-shrink: 1`, which means all items will **shrink evenly**. If you do *not* want an item to *shrink*, then you can specify `flex-shrink: 0;`. You can also specify **higher numbers** to make certain items ***shrink at a higher rate than normal***.

Note that we've also changed the `flex-basis` for reasons that will be explained shortly. If you shrink your browser window, you'll notice that `.two` never gets smaller than the given width of `250px`, even though the `flex-grow` rule would otherwise specify that each element should be equally sized.

```html
<div class="flex-container">
    <div class="one"></div>
    <div class="two"></div>
    <div class="three"></div>
</div>
```
```css
.flex-container {
    display: flex;
}

/* this selector selects all divs inside of .flex-container */
.flex-container div {
    background; peachpuff;
    border: 4px solid brown;
    height: 100px;
    width: 250px;
    flex: 1 1 auto;
}

.flex-container .two {
    flex-shrink: 0;
}
```

An important implication to notice here is that when you specify `flex-grow` or `flex-shrink`, flex items do not necessarily respect your given values for `width`. In the above example, all three `div`s are given a width of 250px, but when their parent is big enough, they grow to fill it.

Likewise, when the parent is too small, the default behavior is for them to *shrink to fit*. ***This is not a bug, but it can be confusing behavior if you aren't expecting it***.

### Flex-basis
`flex-basis` sets the initial size of a *flex item*, so any sort of `flex-grow`ing or `flex-shrink`ing starts from that **baseline size**. The shorthand value defaults to `flex-basis: 0%;`. The reason we had to change it to `auto` in the `flex-shrink` example is that with the basis set to `0`, those items would **ignore the item's width**, and everything **would shrink evenly**.

Using `auto` as a flex-basis tells the item to check for a `width` declaration (`width: 250px`).

> There is a difference between the default value of `flex-basis` and the way the `flex` shorthand defines it if no `flex-basis` is given. <br> The actual default value for `flex-basis` is `auto`, but when you specify `flex: 1` on an element, it interprets that as `flex: 1 1 0`. If you want to *only* adjust an item's `flex-grow`, you can do so *directly*, without the shorthand. <br> Or, you can be more *verbose* and use the full three value shorthand `flex: 1 1 auto`, which is also equivalent to using `flex: auto`.

### What is flex: auto?
If you noticed, we mentioned a new flex shorthand, `flex: auto` in the previous note.

`flex: auto` is one of the shorthands of flex. When `auto` is defined as a `flex` keyword, it is *equivalent* to the values of `flex-grow: 1`, `flex-shrink: 1`, and `flex-basis: auto` or to `flex: 1 1 auto` using the flex shorthand.

Note that `flex: auto` is not the default value when using the `flex` shorthand despite the name being `auto` which may be slightly confusing at first.

You will encounter and learn more about `flex: auto` and its potential use-cases when reading through the *further reading* section.

### In practice
You will likely **not** be using complex values for `flex-grow`, `flex-shrink`, or `flex-basis`. Generally, you're most likely to use declarations like `flex: 1;` to make `div`s grow evenly and `flex-shrink: 0` to keep certain `div`s from shrinking.

It is possible to get fancy, and set up layouts where some columns relate to each other in a specific ratio, so it's useful to know that you can use other values, but those are **relatively rare**.

### Knowledge check
1. What are the three values defined in the shorthand `flex` property (e.g. `flex: 1 1 auto`)?
> Three values defined in the shorthand is the `flex-grow`, `flex-shrink`, and `flex-basis`.

2. What are the three defined values for the flex shorthand `flex: auto`?
> The three defined values for the flex shorthand `flex: auto` is `flex: 1 1 auto;`
# Alignment

> What was covered last chapter: The two axes of a flex container, and changing those axes to arrange your content in columns instead of rows

> Overview of this chapter: Align items inside a flex container both vertically and horizontally

### Recap
So far, everything that was discussed with flexbox has used the rule `flex: 1` on all `flex` items, which makes the items **grow** or **shrink** equally to fill all of the available space.

However, this is not the desired effect. `flex` is also very useful for arranging items that have a specific size.

```html
<div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</div>
```
```css
.container {
    height: 140px;
    padding: 16px;
    background: plum;
    border: 4px solid indigo;
    display: flex;
}

.item {
    width: 60px;
    height: 60px;
    border: 4px solid darkslategray;
    background: skyblue;
    flex: 1; /* .item inside .container becomes more accustomed to the space */
}
```

Adding `flex: 1` to `.item` makes each of the items **grow** to fill the available space, but what if we wanted them to stay the same width, but distribute themselves differently inside the container?

We can do this by removing `flex: 1` from .item and add `justify-content: space-between` to `.container`. Doing so should give you something like 3 separate (and spaced) items, in a flex container.

`justify-content` aligns items across the **main axis**. There are a few values that you can use here. If you try changing it to `center`, it should center the boxes along the main axis!

To change the placement of items along the **cross axis** use `align-items`. Try getting the boxes to the center of the container by adding `align-items: center` to `.container`.

The desired result looks like the squares spaced (compact, respecting each border) together inside the flex container.

Because `justify-content` and `align-items` are based on the main and **cross axis** of your container, their behavior changes when you change the `flex-direction` of a `flex-container`.

For example, when you change `flex-direction` to `column`, `justify-content` aligns vertically and `align-items` aligns horizontally.

The most common behavior, however, is the default, i.e. `justify-content` aligns items horizontally (because the **main axis** defaults to **horizontal**), and `align-items` aligns them **vertically**. One of the biggest sticking points that beginners have with `flexbox` is confusion when this behavior changes.

### Gap
One very useful feature of `flex` is the `gap` property. Setting `gap` on a flex container adds a **specified space** between **flex items**, similar to adding a margin to the items themselves.

`gap` is a new property so it doesn't show up in many resources yet, but it works reliably in all modern browsers, so it is safe to use and very handy!

Adding `gap: 8px;` to the centered example above produces the result of a flex container with flex items with a `gap` of `8px`.

```html
<div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
</div>
```
```css
.container {
    height: 140px;
    padding: 16px;
    background: plum;
    border: 4px solid indigo;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.item {
    width: 60px;
    height: 60px;
    border: 4px solid darkslategray;
    background: skyblue;
}
```

Creating a CSS flexbox form for a name and email field input:
```css
form {
    display: flex;
    align-items: flex-end;
    flex-wrap: wrap;
    gap: 16px;
}

.name {
    flex-grow: 1;
    flex-basis: 160px;
}

.email {
    flex-grow: 3;
    flex-basis: 200px;
}

button {
    flex-grow: 1;
    flex-basis: 80px;
}
```

### Knowledge Check
1. What is the difference between `justify-content` and `align-items`?
> `justify-content` controls alignment along the main axis (horizontal when `flex-direction: row`, which is the default). `align-items` controls alignment along the cross axis (vertical when `flex-direction: row`).

2. How do you use flexbox to completely center a div inside a flex container?
> ```css
> .container {
>    display: flex;
>    justify-content: center; /* centers horizontally (main axis) */
>    align-items: center; /* centers vertically (cross axis) */
> }

> You need **both** to center in both directions:
- `justify-content: center` => centers horizontally (main axis)
- `align-items: center` => centers vertically (cross axis)

3. What's the difference between `justify-content: space-between` and `justify-content: space-around`?
> The difference between them is that `justify-content: space-between` matters on the space in between boxes (not respecting the inner edge of the container), whereas `justify-content: space-around` matters on the space around the container, respecting the inner edge. 
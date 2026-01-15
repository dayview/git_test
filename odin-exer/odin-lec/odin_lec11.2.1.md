# Inline vs Inline-Block Dispaly in CSS
`display: inline-block` brought a new way to create side by side boxes that collapse and wrap properly depending on the available space in the containing element.

It makes layouts that were previously accomplished with floats easier to create. *No need to clear floats anymore*.

Compared to `display: inline`, the major difference is that `inline-block` allows to set a width and height on the element. Also, with `display: inline`, top and bottom margins & paddings are not respected, and with `display: inline-block` they are.

Now, the difference between `display: inline-block` and `display: block` is that, with `display: block`, a **line break** happens after the element, so a block element doesn't sit next to other elements.

Here are some examples: <br>
`display: inline`
```css
span.box {
    display: inline; /* the default for span */
    width: 100px;
    height: 160px;
    padding: 18px;
}
```
You cannot see it visually, but the width and height are not respected, and how the padding top and bottom and present, but overlap over the lines, above and under.

`display: inline-block`
```css
span.box {
    display: inline-block;
    width: 100px;
    height: 160px;
    padding: 18px;
}
```
Here, the width, height, and padding are respected, but the two copies of the element can still sit side by side.

`display: block`
```css
span.box {
    display: block;
    width: 100px;
    height: 160px;
    padding: 18px;
}
```
Here, everything is respected, but the elements **don't** sit side by side.
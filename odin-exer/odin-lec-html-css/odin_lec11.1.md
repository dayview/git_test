# Introduction to CSS layout

> This is supplementary content to #11 (Block and Inline).

> Notes overview: Recaps some of the CSS layout features we've already touched upon in previous modules, such as different `display` values

> What will be tackled in this notes: Recognizing the methouds used to implement modern page layouts, understand that **normal flow** is the default way a browser lays out *block* and *inline* content, and know that properties such as `display`, `float`, and `position` are intended to change how the browsers lays out content

CSS page layout techniques allow us to take elements contained in a web page and control where they're positioned relative to the following factors: their default position in **normal layout flow**, the other elements around them, their **parent container**, and the **main viewport/window**.

## Normal layout flow
Elements on a webpage lay out in **normal flow** if you haven't applied any CSS to change the way they behave.

You can change how elements behave either by adjusting their position in normal flow or by removing them from it altogether.

Starting with a solid, well-structured document that's readable in normal flow is the best way to begin any webpage. It ensures that your content is readable even if the usre's using a very limited browser or a device such as a screen reader that reads out the content of the page.

In addition, since **normal flow** is designed to make a readable document, by starting in this way you're working with the document rather than struggling against it as you make changes to the layout.

Before digging deeper into different layout methods, it's worth revisiting some of the things you have studied in previous modules with regard to normal document flow.

## How are elements laid out by default?
The process begins as the boxes of individual elements are laid out in such a way that any `padding`, `border` or `margin`, they happen to have is added to their content.

This is what we call the **box model**.

By default, a block-level element's content fills the available inline space of the parent element containing it, growing along the block dimension to accommodate its content. The size of inline-level elements is just the size of their content. You can set `width` or `height` on some elements that have a default `display` property value of `inline`, like `<img>`, but the `display` value will still remain `inline`.

> From W3Schools: **HTML Block and Inline Elements** <br><br> Every HTML element has a default display value, depending on what type of element it is, and the two most common display values are **block** and **inline**. [See here](odin_lec11.2.md)
# HTML Block and Inline Elements

## Block-level Elements
A block-level element always starts on a **new line**, and **the browsers automatically add some space** (a margin) **before** and **after** the element.

A block-level element always **takes up the full width available** (stretches out to the left and right as far as it can).

Two commonly used block elements are: `<p>` and `<div>`.

The `<p>` element defines a paragraph in an HTML document. <br> The `<div>` element defines a division or a section in an HTML document.

**The `<p>` and `<div>` element is a block-level element.** (bold as an emphasis for the structure)

```html
<p>Hello World</p>
<div>Hello World</div>
```

Here are the *usual* block-level elements in HTML:
```html
<header>
<table>
<article>
<div>
<hr>
<ol>
<footer>
<li>
<p>
<ul>
<form>
<main>
<video>
<canvas>
<h1>-<h6>
<nav>
<section>
```

## Inline Elements
An inline element does not start on a new line. <br> An inline element only takes up as much width as necessary.

This is **a `<span>` element inside** a paragraph. (bold as an emphasis for the structure)

```html
<span>Hello World</span>
```

Here are the *usual* inline elements in HTML:
```html
<a>
<span>
<br>
<em>
<label>
<strong>
<button>
<b>
<img>
<input>
<textarea>
```

> **Note: An inline element cannot contain a block-level element!**

## The `<div>` Element
The `<div>` element is often used as a container for other HTML elements. <br> The `<div>` element has no required attributes, but `style`, `class`, and `id` are common.

When used together with CSS, the `<div>` element can be used to style blocks of content:

Example:
```html
<div style="background-color:black;color:white;padding:20px;">
    <h2>London</h2>
    <p>London is the capital city of England. It is the most populous city in the United Kingdom, with a metropolitan area of over 13 million inhabitants.</p>
</div>
```

## The `<span>` Element
The `<span>` element is an inline container used to mark up a part of a text, or a part of a document.

The `<span>` element has no required attributes, but `style`, `class`, and `id` are common.

When used together with CSS, the `<span>` element can be used to style parts of the text.

Example:
```
<p>My mother has <span style="color:blue;font-weight:bold;">blue</span> eyes and my father has <span style="color:darkolivegreen;font-weight:bold;">dark green</span> eyes.</p>


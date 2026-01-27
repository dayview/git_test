# Block and Inline

> What was covered last chapter: The Box Model and its properties (`margin`, `border`, and `padding`)

> Overview of this chapter: "Normal flow", learn the difference between `block` and `inline` elements, learn which elements default to `block` and `inline`, and what `div`s and `span`s are.

## Block vs Inline
Most of the elements that you have learned about so far are block elements. In other words, their default style is `display: block;`. 

By default, block elements will appear on the page stacked atop each other, each new element starting on a new line.

Inline elements, however, do **NOT** start on a new line. They appear in line with whatever elements they are placed beside.

A clear example of an inline element is a link, or `<a>` tag.

If you stick one of these in the middle of a paragraph of text, [the link will behave like a part of the paragraph](https://www.youtube.com/watch?v=dQw4w9WgXcQ). Additionally, `padding` and `margin` behave differently on inline elements. In general, you do **NOT** want to try to put **extra padding** or **margin** on **inline elements**.

### Inline-block
Inline-block elements behave like *inline elements*, but with *block-style* `padding` and `margin`. `display: inline-block;` is a useful tool to know about, but in practice, you'll probably end up reaching for `flexbox` more often if you're trying to line up a bunch of boxes.

### What are `div` and `span`?
A `div` is a generic **block-level** container:
* It behaves like a big rectangle that takes up the full width of its parent and starts on a new line.

A `span` is a generic **inline** container:
* It behaves like part of a line of text and does not start on a new line.

They exist mainly so you can **group things and style them**.

`div` and `span` exist to (1) attach CSS and JavaScript as oftentimes you want to style or manipulate something that doesn't have its own semantic tag.

If you want one word in a paragraph to be green and bold, there is no special HTML tag for "green bold word", so you wrap it in a `span`:
```html
<p>
    I like <span class="emphasis">CSS</span>.
</p>
```
```css
.emphasis {
    color: green;
    font-weight: bold;
}
```

We will often need an element that serve no other purpose than to be "hook" elements. We can give and `id` or `class` to target them for styling with CSS (or later, JavaScript).

(2) To group elements for layout as sometimes you want to move or style multiple elements **as a unit**.

If you want a card with and image, a title, and a button, you can assign them a class name (e.g. card):
```html
<div class="card">
    <img src="pic.jpg" alt="..." />
    <h2>Card Title </h2>
    <p>Some description text.</p>
    <button>Read more</button>
</div>
```
```css
.card {
    border: 1px solid #ccc;
    padding: 16px;
    width: 300px;
}
```

The `div` in this case does **NOT** mean "card" in HTML; it's just a box that **groups** these elements so you can position and style them together.

#### How do they behave differently?
`div` – block-level
* starts on a **new line**
* expands to fill the **full available width** by default

Common uses are:
* Page sections, cards, sidebars, headers/footers (when a semantic tag doesn't fit or you need an extra wrapper)
* Containers for layout (especially with Flexbox/Grid later)

Example:
```html
<div class="section">
    <h2>About Me</h2>
    <p>Short bio here.</p>
</div>
```

`span` – inline
* sits **inside a line** of text
* only takes up as much **width as its content**

Common uses are:
* style part of a sentence
* wrap a small piece for JS behavior (e.g., highlighting, tooltips)

Example:
```html
<p>
    I'm learning <span class="language">HTML</span>,
    <span class="language">CSS</span>, and <span class="language">JavaScript</span>.
</p>
```

#### When should you not use them?
If there is a **semantic element** that expresses the meaning, prefer that instead:
1. Use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>` for structure.

2. Use `<button>`, `<a>`, `<ul>/<li>`, etc. for their specific purposes.

Use `div`/`span` when:
1. No semantic tag fits, **and**
2. You need a hook for styling, layout, or scripting

#### Sample Code and Their Description
`div` is a block-level element by default. It is commonly used as a container element to group other elements. `div`s allows us to *divide* the page into different blocks and apply styling to those blocks.

```html
<div class="introduction">
    <h2>Introduction</h2>
</div>

<div class="main-content">
    <h2>Main Content</h2>
</div>

<div class="contact-us">
    <h2>Contact Us</h2>
</div>
```
```css
div {
    padding: 30px;
    text-align: center;
    margin-bottom: 10px;
    color: #eeeeee;
}

.introduction {
    background-color: #548ca8;
}

.main-content {
    background-color: #476072;
}

.contact-us {
    background-color: #334257;
}
```

`span` is an inline-level element by default. It can be used to group text content and inline HTML elements for styling and should only be used when no other semantic HTML element is appropriate.

```html
<p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, <span class="highlight">quis nostrud <a href="https://www.dictionary.com/browse/exercitation">exercitation</a>ullamco laboris</span> nisi ut aliquip ex ea commodo consequat.
</p>
```
```css
.highlight {
    background-color: yellow;
}
```

## Knowledge Check
1. What is the difference between a block element and an inline element?

> The difference between a block and an inline element is that a block is more associated with groups/division of a certain section of elements, whereas an inline element is more associated with the text spacing, or specifically an element in paragraphs.

2. What is the difference between an inline element and an inline-block element?

> The difference between an inline element and an inline-block is that an inline element specifies on the text-lining of the paragraph, or any related text, whereas an inline-block specifies on the section/division of a text.

3. Is an `h1` block or inline?
> An `h1` tag is a block element.

4. Is `button` block or inline?
> A button tag is an inline element.

5. Is `div` block or inline?
> A button tag is a block element.

6. Is `span` block or inline?
> A span tag is an inline element.
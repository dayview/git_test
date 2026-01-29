# Introduction to Flexbox

> What was covered last chapter: Block and Inline, learn which elements default to `block` and `inline`, and what `div`s and `span`s

> Overview of this chapter: Position elements using flexbox, flex containers, flex items, and create useful components and layouts that go beyond just stacking and centering items

## Before we get started
If something isn't behaving the way you expect, inspecting in the **developer tools** should be your first step *every time*.

Flexbox isn't necessarily any more difficult than the other concepts that we've covered so far, but it *does* have a few more moving parts. it is going to be somewhat difficult to make use of any of the things you're learning in these first lessons until you get to the end and can put it all together.

As we go, do yourself a favor and *play with all of the code examples*.

### Let's flex!
Flexbox is a way to arrange items into rows or columns. These items will flex (i.e. grow or shrink) based on some rules that you can define.

```html
<div class="flex-container">
    <div class="one"></div>
    <div class="two"></div>
    <div class="three"></div>
</div>
```
```css
.flex-container {
    /* display: flex; */
}

/* This selector selects all divs inside of .flex-container */
.flex-container div {
    background: peachpuff;
    border: 4px solid brown;
    height: 100px;
    /* flex: 1; */
}
```

We'll get into exactly what's going on here soon enough. But for now, let's uncomment the two flex related CSS declarations in the above *Codepen* by removing the `/*` and `*/` tags surrounding them, then check out the result.

> Comments prevent the browser from interpreting lines as code, and are wrapped between specific tags. CSS use `/*` as opening comment tag and `*/` as a closing comment tag, while HTML and JavaScript have their own syntax. Commented out lines of code can be 're-enabled' by removing the comment tags surrounding the code.

All three `div`s should now be arranged horizontally. If you resize the results frame with the `1x`, `.5x`, `.25x` buttons you'll also see that the `div`s will 'flex'. They will fill the available area and will each have equal width.

If you add another `div` to the HTML, inside of `.flex-container`, it will show up alongside the others, and everything will `flex` to fit within the available area.

### Flex containers and flex items
As you've seen, `flexbox` is not just a single CSS property but a whole toolbox of properties that you can use to put things where you need them. Some of these properties belong on the `flex container`, while some go on the `flex items`. This is an important concept.

Somewhat confusingly, any element can be both a `flex container` and a `flex item`. Said another way, you can also put `display: flex` on a flex item and then use flexbox to arrange its children.

Creating and nesting multiple flex containers and items is the primary way we will be building up complex layouts. The following image was achieved using only *flexbox* to arrange, size, and place the various elements. Flexbox is a *very* powerful tool.

### Knowledge Check
1. What's the difference between a flex container and a flex item?
> A flex container is an element with `display: flex` (or `inline-flex`). It controls how its children are laid out. However, flex items are the direct children of a flex container. They automatically become flex items, you don't "create" them separately. <br> Alternatively, a flex container is an element with `display: flex` or `display: inline-flex`. Flex items are the direct chidlren of a flex container. The container controls the layout of its items.

> Container = parent that has "display: flex;" <br> Items = direct children of that parent <br>

Example:
```html
<div class="container"> <!-- Flex container -->
    <div>Item 1</div>   <!-- Flex item -->
    <div>Item 2</div>   <!-- Flex item -->
    <div>Item 3</div>   <!-- Flex item -->
</div>
```
```css
.container {
    display: flex; /* This makes it a flex container */
}
```

Yes, an element can be both:
```html
<div class="outer">         <!-- Flex container -->
    <div class="middle">    <!-- Flex item AND flex container -->
        <div>Nested item</div> <!-- Flex item of .middle -->
    </div>
</div>
```
```css
.outer {
    display: flex; /* .outer is a container */
}

.middle {
    display: flex; /* .middle is BOTH an item (of .outer) and a container */
}
```

2. How do you create a flex item?
> You create flex items automatically by making their parent a flex container. <br> Alternatively, you create flex items by setting `display: flex` on the parent element. All direct children of that parent automatically become flex items.

Example:
1. Give the parent element `display: flex;`
2. All direct children become flex items automatically
```html
<div class="container">
    <div>I'm a flex item!</div>
    <div>I'm also a flex item!</div>
    <p>I'm a flex item too!</p>
</div>
```
```css
.container {
    display: flex; /* this ONE line makes all direct children into flex items */

    /* so, in that case, you don't need to do anything to the children to make them flex items! */
}
```

> Important! Only direct children become flex items. Nested elements do not:
```html
<div class="container"> <!-- Flex container -->
    <div>Flex item</div>
    <div>
        Flex item
        <span>NOT a flex item (it's a grandchild)</span>
    </div>
</div>
```
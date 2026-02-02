# Cascade

> What was covered last chapter: Covered basic CSS syntax and selectors

> Overview of this chapter: What cascading does, the combination and specific use cases of CSS selectors, and how **inheritance** affects certain properties.

## The C of CSS: Cascade

It's important to take note that CSS doesn't just **do** things against our logic, as it only does what we **tell it to do**.


> **Note:** Sometimes different CSS rules try to style the same element, and the browser has to decide which one to apply. <br><br>If a later or more specific rule sets the paragraph color to red, it will override your earlier rule that set it to blue, so the paragraphs appear red even though you expected them to be blue.

Browsers come with their own built-in styles (called user-agent stylesheets or browser default styles) that apply to HTML elements even when you haven't written any CSS.

These defaults are why headings appear larger and bold, why buttons have a specific appearance, and why elements have default margins and padding creating gaps between them.

Since each browser has slightly different default styles, the same HTML can look different across Google Chrome, Mozilla Firefox, Apple Safari, and other browsers.

This is also why many developers use CSS resets to remove or normalize these defaults and start with a consistent baseline across all browsers.

> **Note:** So, if you end up with some unexpected behavior relative to this, it's either because of the default styles given by each browser, not understanding how a property works, or the general idea of the cascade.

The cascade is what determines which rules *actually* get applied to the HTML. There are different factors that the cascade uses to determine this.

In this lesson, we will examine three of these factors.

## Specificity
A CSS declaration that is more specific will take precedence over less specific ones. Inline styles, which we went over in the previous lesson, have the highest specificity compared to selectors, while each type of selector has its own specificity level that contributes to how specific a declaration is.

Other selectors contribute to specificity, but we're focusing only on the ones we've gone over so far:
1. ID Selectors (most specific selector)
2. Class selectors
3. Type selectors

**Specificity** will only be taken into account when an element has multiple, conflicting declarations targeting it, sort of like a tie-breaker. <br>

> So, an **ID selector** will always beat *any number* of **class selectors**; <br> A **class selector** will always beat *any number* of **type selectors**; <br>and a **type selector** will always beat *any number* of **less specific selectors**. 

When there is no declaration with a number of selectors of the same type, it will take precedence over another rule with fewer selectors of the same type. <br><br> This means that when **specificity is equal** (for example, all selectors are classes, or all are element selectors), the browser looks at **how many** of those selectors you're using. <br><br> If two rules both use only class selectors (same type, same specificity level), the one with **more class selectors** gets rendered.

```css
.button {
    background: red;
}

.button.primary {
    background: blue;
}
```

With element selectors:
```css
p {
    color: black;
}

div p {
    color: green;
}
```

> Both use element selectors, but `div p` has **two** (one for `div`, one for `p`), so it's more specific than just `p` alone. <br><br> Therefore, paragraphs inside a `div` will be green.
#### in index.html: <br> 
```html
<div class="main">
    <div class="list subsection">Red text</div>
 </div>
```

#### in styles.css: <br>
```css
/* rule 1 */
.subsection {
    color: blue;
}

/* rule 2 */
.main .list {
    color: red;
}
```

In the example above, both rules are using only class selectors, but **rule 2** is more specific because it is **using more class selectors**, so the `color: red;` declaration would take precedence.

If we change things a little bit:
```html
<div class="main">
    <div class="list" id="subsection">Blue text</div>
</div>
```
```css
/* rule 1 */
#subsection {
    color: blue;
}

/* rule 2 */
.main .list {
    color: red;
}
```

In the example above, despite **rule 2** having **more class selectors** than **ID selectors**, **rule 1** is more specific because **ID beats class**. In this case, the `color: blue;` declaration would take precedence.

And a bit more complex:
```html
<div class="main">
    <div class="list" id="subsection">Red text on yellow background</div>
</div>
```
```css
/* rule 1 */
#subsection {
    background-color: yellow;
    color: blue;
}

/* rule 2 */
.main #subsection {
    color: red;
}
```

In this final example, the **first rule** uses an **ID selector**, while the **second rule** combines and **ID selector** with a **class selector**. Therefore, neither rule is using a more specific selector than the other.

The cascade then checks the **number** of each **selector type**. Both rules have only **one ID selector**, but **rule 2** has a **class selector** in addition to the **ID selector**, so **rule 2** has a higher **specificity**!

**TAKE NOTE!** While the `color: red;` declaration would take precendence, the `background-color: yellow;` declaration would still be applied since there's no conflicting declaration for it.

#### Not everything adds to Specificity
When comparing selectors, you may come across special symbols for the universal selector (`*`) as well as combinators (`+`, `~`, `>`, and an empty space).

> **Module Notes:** The ones you have not yet seen, we wil cover these later in the curriculum, so there is no need to dive into them yet. The core concept is that these symbols do not inherently convey any additional **specificity**.

```css
/* rule 1 */
.class.second-class {
    font-size: 12px;
}

/* rule 2 */
.class .second-class {
    font-size: 24px;
}
```

Here, both rules 1 and 2 have the same **specificity**. **Rule 1** uses a **chaining selector** (no space), and **Rule 2** uses a **descendant combinator** (the empty space). But both rules have **two classes** and the **combinator symbol** itself does not add to the **specificity**.

```css
/* rule 1 */
.class.second-class {
    font-size: 12px;
}

/* rule 2 */
.class > .second-class {
    font-size: 24px;
}
```

This example shows the same thing (as earlier). Even though **Rule 2** is using a **child combinator** (`>`), this does **not** change the **specificity value**. Both rules still have **two classes**, so they have the same specificity values.

```css
/* rule 1 */
* {
    color: black;
}

/* rule 2 */
h1 {
    color: orange;
}
```

In this example, **Rule 2** would have higher specificity and the `orange` value would take precedence for this element. **Rule 2** uses a **type selector**, which has the **lowest specificity value**. But, **Rule 1** uses the universal selector (`*`), which has **no specificity value**.


## Inheritance
Inheritance refers to certain CSS properties that, when applied to an element, are inherited by that element's descendants, even if we don't explicitly write a rule for those descendants.

Typography-based properties (`color`, `font-size`, `font-family`, etc.) are usually inhertied, while most other properties aren't.

You can find out if a property is inherited or not by going to its docs on MDN and heading to the <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/color#formal_definition" target="_blank">**Formal Definition**</a> section.

> For example, the CSS `color` property's formal definition indicates that `color` is an inherited property, while the `display` property's <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/display#formal_definition" target="_blank">formal defintion</a> indicates that `display` is not. <br><br> The exception to this is when directly targeting an element, as this always beats inheritance:

```html
<div id="parent">
    <div class="child"></div>
</div>
```
```css
#parent {
    color: red;
}

.child {
    color: blue;
}
```

Despite the `parent` element having a higher specificity with an ID, the `child` element would have the `color: blue;` style applied since that declaration directly targetrs it, while `color: red;` from the parent is only inherited.

### Rule Order
The final factor, the end of the line, the *tie-breaker of the tie-breakers*.

Let's say that after every other factor has been taken into account, there are still multiple conflicting rules targeting an element.

How does the cascade determien which rule to apply?

**Whichever rule was *last* defined is the winner**.

```css
.alert {
    color: red;
}

.warning {
    color: yellow;
}
```

For an element that has both the `alert` and `warning` classes, the cascade would run through every factor, including inheritance (none here) and specificity (neither rule is more specific than the other).

Since the `.warning` rule was the last one defined, and no other factor was able to determine which rule to apply, it's the one that gets applied to the element.
___

### Knowledge Check

1. Between a rule that uses one class selector and a rule that uses three type selectors, which rule has the higher specificity? <br> > One class selector has the higher specificity since it's higher than type selectors.
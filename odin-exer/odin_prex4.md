# Cascade Practice Drills
For each scenario, predict:
1. What color will the text be?
2. Why? (specificity? inheritance? rule order?)

Scenario 1:
```html
<div class="container">
    <p class="text highlight">What color am I?</p>
```
```css
/* Rule A */
.text {
    color: green;
}

/* Rule B */
.container .text {
    color: purple;
}
```

**Color & Reason:** Purple due to specificity (.container .text has 2 class selectors versus `.text`, which has 1).
<br>
**Explanation:** Rule B uses two class selectors (`.container` and `.text`), while Rule A uses only one (`.text`). <br>

> **More selectors of the same type = higher specificity.**
___
Scenario 2:
```html
<div class="box" id="special">What color am I?</div>
```
```css
/* Rule A */
.box {
    color: blue;
}

/* Rule B */
#special {
    color: red;
}

/* Rule C */
.box.box.box {
    color: orange;
}
```

**Color & Reason:** Red, since ID beats class selectors.
<br>
**Explanation:** `#special` (ID selector) always wins over any number of class selectors, even `.box.box.box` with three classes. ID is the highest specificity (after inline styles).
___
Scenario 3:
```html
<h1 class="title">What color am I?</h1>
```
```css
/* Rule A */
.title {
    color: pink;
}

/* Rule B */
h1 {
    color: yellow;
}

/* Rule C */
.title {
    color: teal;
}
```

**Color & Reason:** Teal, order of implementation (last rule wins).
<br>
**Explanation:** Both Rule A and Rule C use `.title` (same specificity). Rule B uses `h1` (lower specificity, so it loses). Between A and C, Rule C comes last, so it wins.
___
Scenario 4:
```html
<div id="parent">
    <p class="child">What color am I?</p>
</div>
```
```css
/* Rule A */
#parent {
    color: red;
}

/* Rule B */
.child {
    color: blue;
}
```

**Color & Reason:** Blue, ***direct targeting always beats inheritance***.
<br>
**Explanation:** Even though `#parent` has higher specificity (ID > class), the `color: red;` is only inherited by the `<p>` child. But Rule B **directly targets** the child with:
```css
.child {
    color: blue;
}
```

***Direct targeting always wins over inherited styles, no matter the parent's specificity.***
___
Scenario 5:
```html
<div class="wrapper">
    <div class="box inner">What color am I?</div>
</div>
```
```css
/* Rule A */
.box.inner {
    font-size: 16px;
    color: green;
}

/* Rule B */
.wrapper .box {
    font-size: 20px;
    color: orange;
}
```

**Color & Reason:** Orange, because specificity was equal, but order is different.
<br>
**Font Size:** 20px
<br>
**Explanation:** Both rules have the **same specificity**:
* Rule A: `.box.inner` = 2 class selectors (chaining, no space)
* Rule B: `.wrapper .box` = 2 class selectors (descendant combinator with space)

> Combinators (spaces, `>`, `+`, `~`) do **NOT** add specificity. So, both rules have equal specificity (2 classes each). <br><br> Since they're equal, **order matters**, as Rule B comes **last**, so it wins for both `color` and `font-size`.
___
Scenario 6:
```html
<div class="parent" id="container">
    <p>What color am I?</p>
</div>
```
```css
/* Rule A */
#container {
    color: purple;
}

/* Rule B */
p {
    color: yellow;
}
```

**Color & Reason:** Yellow, check explanation
<br>
**Explanation:** Yes, `#container` has higher specificity than `p`. **BUT**, the `color: purple;` from `#container` is only **inherited** by the `<p>`, it's not directly targeting it. Rule B **directly targets** `p` with:
```css
p {
    color: yellow;
}
___
Scenario 7:
```html
<div id="grandparent">
    <div class="parent">
        <span class="child">What color am I?</span>
    </div>
</div>
```
```css
/* Rule A */
#grandparent {
    color: red;
}

/* Rule B */
.parent {
    color: blue;
}

/* Rule C */
span {
    color: green;
}
```

**Color & Reason:** Green, even though the ID selector from the grandparent wins over to both the parent and the child, a direct modification to the span (or child) will always win no matter the inheritance hierarchy is.
<br>
**Explanation:** Even though `#grandparent` (ID) has the highest specificty and `.parent` (class) is higher than `span` (element), the `span` rule **directly targets** the element, so it wins. Inherited styles (from grandparent or parent) lose to any direct rule.
___
Scenario 8:
```html
<div class="outer">
    <div class="inner">
        <p class="text">What color am I?</p>
    </div>
</div>
```
```css
/* Rule A */
.outer > .inner > .text {
    color: orange;
}

/* Rule B */
.outer .text {
    color: pink;
}
```

**Color & Reason:** Orange, since it has three points of specificity (`.outer`, `.inner`, and `.text`), however, the `>` symbol does not count.
<br>
**Explanation:** <br>Rule A: `.outer > .inner > .text` = 3 class selectors (child combinators `>` add no specificity), whereas, <br>Rule B: `.outer .text` = 2 class selectors. 3 is greater than 2, so Rule A wins!
___
Scenario 9:
```html
<div class="wrapper">
    <button class="btn primary">What color am I?</button>
</div>
```
```css
/* Rule A */
.btn.primary {
    color: teal;
}

/* Rule B */
.wrapper .btn {
    color: coral;
}

/* Rule C */
.btn.primary {
    color: navy;
}
```

**Color & Reason:** Navy, since the Rule C implementation was first before the Rule A (same chain) and Rule B (descendant with same count).
<br>
**Explanation:** <br>Rule A: `.btn.primary` = 2 classes (chaining), <br>Rule B: `.wrapper .btn` = 2 classes (descendant), <br>Rule C: `.btn.primary` = 2 classes (chaining) <br> All three have equal specificity (2 classes each). When specificity is tied, the **last rule wins**. Rule C is last, so **navy** wins!
___
Scenario 10:
```html
<section id="main">
    <article class="post">
        <h2>What color am I?</h2>
    </article>
</section>
```
```css
/* Rule A */
#main {
    color: red;
}

/* Rule B */
.post {
    color: blue;
}
```
**No rule directly targets h2.**

**Color & Reason:** Blue, check explanation
<br>
**Explanation:** Think about what the `<h2>` actually inherits from. <br> The `<h2>` has **no direct rule** targeting it. So, it will inherit `color` from its closest parent. <br>
* #main sets `color: red;` (on the `<section>`)
* .post sets `color: blue;` (on the `<article>`)

The `<h2>` is **inside** the `<article>`, so it inherits from `.post` (its immediate parent), not from `#main` (its grandparent).

> When inheriting, elements inherit from their **closest ancestor** that has the property set, regardless of specificity.
___
Scenario 11:
```html
<div id="container" class="box">
    <p class="text">What color am I?</p>
</div>
```
```css
/* Rule A */
#container .text {
    color: red;
}

/* Rule B */
.box p {
    color: blue;
}

/* Rule C */
div.box .text {
    color: green;
}
```

**Color & Reason:** Red, since the ID selector takes priority over div.box .text (still counts as two, but only uses class selector).
<br>
**Explanation:** <br>
* Rule A: #container .text = 1 ID + 1 Class
* Rule B: .box p = 1 class + 1 element
* Rule C: div.box .text = 1 element + 2 classes  <br>
**ID beats everything, so Rule A wins!**
___

Scenario 12:
```html
<div class="wrapper">
    <h1 id="title" class="heading" style="color: orange;">What color am I?</h1>
</div>
```
```css
/* Rule A */
#title {
    color: purple;
}

/* Rule B */
.wrapper #title.heading {
    color: teal;
}
```

**Color & Reason:** Orange, since the inline takes priority despite Rule B having three mixed selectors (`.wrapper #title.heading`).
<br>
**Explanation:** Inline styles (using the `style=""` attribute) have the **highest specificity**, even higher than **ID**s. No matter how many selectors **Rule B** uses, inline always wins!
___

Scenario 13:
```html
<div class="container">
    <p>What color am I?</p>
</div>
```
```css
/* Rule A */
* {
    color: gray;
}

/* Rule B */
.container * {
    color: pink;
}

/* Rule C */
p {
    color: navy;
}
```

**Color & Reason:** Navy, since Rule B only has one selector (`.container`), and the `*` does not count, therefore Rule C being the winner for the cascading logic.
<br>
**Explanation:** <br>
* Rule A = `*` = 0 specificity (universal selector has no value)
* Rule B = `.container *` = 1 class + 0 (universal still adds nothing)
* Rule C = `p` = 1 element selector <br>
**Element selector beats universal, so Rule C wins!**
___

Scenario 14:
```html
<div class="wrapper">
    <h2 class="title">Heading</h2>
    <p class="text special">What color am I?</p>
</div>
```
```css
/* Rule A */
.text {
    color: red;
}

/* Rule B */
.title + .text {
    color: blue;
}

/* Rule C */
.text.special {
    color: green;
}
```

**Color & Reason:** Green, since `.text.special` counts as two selectors as the same as `.title + .text`, however, Rule C (`.text.special`) due to it being implemented lastly in the code.
<br>
**Explanation:** <br>
* Rule A: `.text.` = 1 class
* Rule B: `.title + .text` = 2 classes (adjacent sibling `+` doesn't add specificity, but both `.title` and `.text` count!)
* Rule C: `.text.special` = 2 classes (chaining) <br>
**Rules B** and **C** both have 2 classes (tied specificity). When tied, the **last rule wins**! <br> **Rule C** comes **last** (after **Rule B**), so it wins with green!
___

Scenario 15:
```html
<section id="main" style="color: purple;">
    <div class="content">
        <article class="post">
            <p>What color am I?</p>
        </article>
    </div>
</section>
```
```css
/* Rule A */
.content {
    color: blue;
}

/* Rule B */
.post {
    color: green;
}

/* Rule C */
#main p {
    color: red;
}
```

**Color & Reason:** Red, since (`#main p`) counts as two values of specificity. Even though the section would override it with `color: purple;`, Rule C would take more in precedence due to specificity value and the order of implementation.
<br>
**Explanation:** <br>
* Inline on `<section>`: `color: purple;` (would be inherited by `<p>`)
* Rule A: `.content` = 1 class (would be inherited)
* Rule B: `.post` = 1 class (would be inherited)
* Rule C: `#main p` = 1 ID + 1 element = **directly targets** `<p>` <br>
**Rule C** ***directly targets*** the `<p>` element, so it beats all the inherited colors from ancestors. The inline style on `<section>` doesn't matter because **Rule C** is ***directly targeting*** the `<p>`, not inheriting from the section.
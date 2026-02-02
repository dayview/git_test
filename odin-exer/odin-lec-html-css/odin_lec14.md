# Axes

> What was covered last chapter: The three properties that are defined by the `flex` shorthand, and how it is individually used

> Overview of this chapter: The two axes of a flex container, and changing those axes to arrange your content in columns instead of rows

## Axes
The most confusing thing about `flexbox` is that it can work either **horizontally** or **vertically**, and some rules change a bit depending on which direction you are working with.

The default direction for a flex container is **horizontal**, or `row`, but you can change the direction to **vertical**, or `column`. The direction can be specified in CSS like so:
```css
.flex-container {
    flex-direction: column;
}
```

No matter which direction you're using, you need to think of your `flex-containers` as having **2 axes**: the **main axis** and the **cross axis**. It is the direction of these axes that changes when the `flex-direction` is changed.

In most circumstances, `flex-direction: row` puts the **main axis horizontal** (left-to-right), and `column` puts the **main axis vertical** (top-to-bottom).

In other words, in our very first example, we put `display: flex` on a `div` and it arranged its children **horizontally**. This is a demonstration of `flex-direction: row`, the default setting.

The following example is very similar. If you look at the code snippet that says `flex-direction: column`, those `div`s will stack **vertically**.

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
    /* flex-direction: column; */
}

/* this selector selects all divs inside of .flex-container */
.flex-container div {
    background: peachpuff;
    border: 4px solid brown;
    height: 80px;
    flex: 1 1 auto;
}
```

One thing to note is that in this example, `flex-direction: column` would not work as expected if we used the shorthand `flex: 1`

Try to change the flex value on the `flex: 1 1 auto;` to `flex: 1`.

Can you figure out why it does not work if `flex: 1` is used? The `div`s collapse, even though they *clearly* have a `height` defined there.

> The reason for this is that the `flex` shorthand expands `flex-basis` to `0`, which means that all `flex-grow`ing and `flex-shrink`ing would begin their calculations from `0`. Empty `div`s by default have `0` height, so for our `flex` items to fill up the height of their container, they don't actually need to have any `height` at all.

The example above fixed this by specifying `flex: 1 1 auto`, telling the `flex` items to default to their given `height`. We could also have fixed it by putting a `height` on the parent `.flex-container`, or by using `flex-grow: 1` instead of the shorthand.

Another detail to notice: when we changed the `flex-direction` to `column`, `flex-basis` refers to `height` instead of `width`. Given the context this may be obvious, but it's something to be aware of.

To bring it back home, the default behavior is `flex-direction: row;` which arranges things **horizontally**. This reason this often works well without changing other details in the CSS is because block-level elements default to the full width of their parent. Changing this to **vertical** using `flex-direction: column` adds complexity because block-level elements default to the **ful width** of their parent.

Changing things to `vertical` using `flex-direction: column` adds complexity because block-level elements default to the `height` of their content, and in this case there *is* no content.

There are situations where the behavior of `flex-direction` could change if you are using a language that is written right-to-left or even **vertically**, but you should not worry about that until you are ready to start making a website in Arabic or Manchu.

### Knowledge Check
1. How do you make flex items arrange themselves vertically instead of horizontally?
> You make flex items arrange themselves vertically by declaring `flex-direction: column`.

2. In a `column` flex-container, what does `flex-basis` refer to?
> `flex-basis` refer to height in a column flex-container.

3. In a `row` flex-container, what does `flex-basis` refer to?
> `flex-basis` refer to width in a row flex-container.

4. Why do the previous two questions have different answers?
> `flex-basis` always refers to the size along the main axis. When `flex-direction: row`, the main axis is horizontal (so `flex-basis` = width). When `flex-direction: column`, the main axis is vertical (so `flex-basis` = height).
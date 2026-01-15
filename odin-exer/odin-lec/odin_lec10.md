# The Box Model

> What was covered last chapter: Inspecting HTML and CSS via Chrome DevTools or Firefox Inspector

> Overview of this chapter: Mastering CSS with positioning and layout (specifically, the box model + properties: `margin:`, `padding:`, and `borders:`).

Changing fonts and colors is a crucial skill, but being able to put things *exactly* where you want them on a webpage is even more crucial. After all, how many webpages can you find where absolutely every element is just stacked one on top of another?

## The (actual) Box Model
Every single thing on a webpage is a rectangular box. These boxes can have other boxes in them and can sit alongside one another.

You can get a rough idea of how this works by applying an outline to every element on the page like this:

```css
* {
    outline: 2px solid red;
}
```

[Box Model - Sample Image](https://cdn.statically.io/gh/TheOdinProject/curriculum/c547923a86efaccb0fc71adf70fda2ea340b4cb1/foundations/html_css/css_foundations/the_box_model/imgs/boxes.png)

The idea here is that there are many ways to manipulate the size of these boxes, and the space between them, using `padding`, `border`, and `margin`. The assigned articles go into more depth into this concept, but to sum it briefly:
* `padding` increases the space between the border of a box and the content of the box
* `border` adds space (even if it's only a pixel or two) between the margin and the padding
* `margin` increases the space between the borders of a box and the borders of adjacent boxes

[Box Model Diagram](https://cdn.statically.io/gh/TheOdinProject/curriculum/c547923a86efaccb0fc71adf70fda2ea340b4cb1/foundations/html_css/css_foundations/the_box_model/imgs/box-model.png)

### Mnemonic & Tips
Mothers bake perfect cookies (out-inside) <br>
**Can pandas be moody? (inside-out)**

Imagine a framed picture on a wall:
1. Content = the artwork/photo itself
2. Padding = the white mat board around the artwork
3. Border = the picture frame
4. Margin = the space between this frame and other frames on the wall

Alternatively, **c**ontent **p**acked in **b**oxes, **m**ailed:
1. Content = the item you're shipping
2. Padding = bubble wrap protecting it
3. Border = the box itself
4. Margin = the space between your box and other boxes on the delivery truck

## Knowledge Check
1. From inside to outside, what is the order of box-model properties?
content box -> padding -> border -> margin

2. What does the `box-sizing` CSS property do?
Changes how the sizing of the content box would be, either respecting the default boundary (border-exclusive) or an alternate boundary (border-inclusive).

> Note for #2: `box-sizing` controls whether the `width` and `height` include only the content (`content-box`, default) or include content + padding + border (`border-box`, alternate).

3. What is the difference between the standard and alternative box model?
As mentioned earlier, standard is border-exclusive from the content box, whereas the alternate one is border-inclusive.

> Note for #3: <br> Standard (`content-box`): width/height = content only <br> Alternative (`border-box`): width/height = content + padding + border.

4. Would you use `margin` or `padding` to create more space between 2 elements?
I would use `margin`.

> Note for #4: Margin creates space **outside** an element, pushing other elements away.

5. Would you use `margin` or `padding` to create more space between the contents of an elements and its border?
I would use `padding`.

> Note for #5: Padding creates space **inside** an element, between the content and the border.

6. Would you use `margin` or `padding` if you wanted two elements to overlap each other?
I would use `margin`.

> Note for #6: You can use **negative margins** (e.g., `margin-top: 20px;`) to pull elements on top of each other and create overlap.

7. How do you set the alternative box model for all your elements?
```css
* {
    box-sizing: border-box;
}
```

> Note for #7: You need the **universal selector (*)** to target **all elements**. Just writing `box-sizing: border-box;` by itself doesn't apply to anything, you need a selector.

8. How do you center an element horizontally?
`margin: 0px auto;`

> Note for #8: Alternatively, you can use `margin: 0 auto;` (vertical auto, horizontal auto) as it centers a block element horizontally when it has a defined width. <br> You can also drop the `px` on `0` since zero is zero in any unit, but `0px` works fine too!
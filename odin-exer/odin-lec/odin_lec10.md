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
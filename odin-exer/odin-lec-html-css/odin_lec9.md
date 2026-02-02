# Inspecting HTML and CSS

> What was covered last chapter: Cascading logic, selector precedence, and inheritance

> Overview of this chapter: Accessing the element inspector, select and inspecting specific elements, testing out HTML and CSS in the inspector.

## Inspector
If you want to open the inspector, you can right-click on any element of a website and click "Inspect" or press `F12`.

> **Note:** Focus only on the Elements and Styles panels.

### Inspecting Elements
In the `Elements` (in Chrome) / `Inspector` (in Firefox) panel, you can see the entire HTML structure of your page.

You can click on any of the elements in this panel (referring to the TOP module) to select that specific element.

> Alternatively, you can click on the upper-left "element select" icon (dashed square with an arrow pointing to the top left), then hover over any element on the page.

When an element is selected, the `Styles` tab will show all the currently applied styles, as well as any styles that are being overwritten (indicated by a strikethrough of the text).

For example, if you use the inspector to click on the `Your` in the `Your Career in Web Development Starts Here` header on the TOP homepage, on the right-hand side, you'll see all the styles that are currently affecting the element, as seen below (don't worry about the `var()` syntax as that's irrelevant to this point).

### Testing Styles in the Inspector
The `Styles` panel also allows you to edit styles directly in the browser.

You can click inside of any individual selector to add a new rule or click on an existing attribute or value to alter it. When doing so, the webpage responds with the changes in real-time.

This won't affect the source code in your text editor, but it is extremely useful for quickly testing out various attributes and values without needing to reload the page over and over again.

### Knowledge Check
1. How do you select a specific element on your page with your browser's developer tools? <br> > You select by using the inspector tool (the dashed square with an arrow pointing to the top left), then select any element in the web page.

> This is the element picker/selector tool that lets you click directly on any part of a webpage to inspect it. You can also right-click any element and choose "Inspect" or "Inspect Element".

2. What does a strikethrough in a CSS declaration mean in your browser's developer tools? <br> >
A strikethrough in a CSS declaration means it has been overriden by a certain class in either HTML or CSS.

> A strikethrough indicates that the CSS property was applied but then **overriden by a more specific selector, a rule that comes later in the cascade, or by `!important`. It helps us understand why our styles aren't showing up as the browser is telling us "this rule exists, but something else won."

3. How do you change CSS in real time on specific elements of a web page with your browser's developer tools? <br> > You can change it by using the Styles tab (below the Inspector tab + if you're using Firefox).

> In the **Styles** (or **Rules**) panel, you can click on any CSS property value and edit it directly, add new properties, toggle properties on/off using checkboxes, or add entire new rules. Changes apply instantly to the page but **aren't saved to your actual CSS files** as they're just for testing;.
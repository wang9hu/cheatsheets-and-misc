For element tag

```
<div>
    <a class='className' id='idName' href='url' >Click me</a>
    <p>Text 1</p>
    <section>
        <p>Text 2</p>
    </section>
</div>

<p>Text 3</p>

<code>Some code</code>

<p>Text 4</p>

<form>
    <input type='text' name='firstname'><br>
</form>
```

### CSS selectors:

1. Simple:

   - by tag name: `a { color: red }`
   - by class name: `.className { color: red }`
   - by id: `#idName { color: red }`
   - universal: `* { color: red }`
   - grouping: `a, p { color: red }`
     <br>

1. Combinators:

   - descendant (space): `div p { color: red }` **Text 1** and **Text 2** will change
   - child (>): `div > p { color: red }` only **Text 1** will change
   - adjacent sibling (+): `div + p { color: red }` only **Text 3** will change
   - general sibling (~): `div ~ p { color: red }` **Text 3** and **Text 4** will change
     <br>

1. Pseudo-classes selector (**:**) style an element when it is (commonly used):

   - mouse hovered: `div:hover { background-color: green }`
   - being clicked: `a:active { background-color: green }`
   - focused: ` input:focus { background-color: green }`
   - first-child of another element: `p:first-child { color: red }`
   - last-child of another element: `p:last-child { color: red }`
     ...
     <br>

1. Pseudo-elements selector (**::**) style specified parts of an element:

   - first letter: `p::first-letter { color: #ff0000 }`
   - first line: `p::first-line { color: #ff0000 }`
   - insert before: `p::before { content: url }`
   - inser after: `p::after { content: url }`
   - highlighted parts: `p::selection { color: red }`
   - marker of list items: `::marker { color: red }`
     <br>

1. Attribute selector style elements with specific attributes or attribute values:
   - attribute: `a[id] { background-color: yellow }`
   - attribute value: `a[id='idName'] { background-color: yellow }`
     ... atrribute value variants
     <br>

---

### The CSS Box Model

- Everything in CSS has a box around it, there are mainly two types of boxes: ==Block== vs ==Inline==, and boxes have an **outer display type** and **inner display type**:

  - ==Outer display type==: how is the **contents** of the element are displayed

    - Block box:
      - The box will **break onto a new line**.
      - The width and height properties are **respected**.
      - **Padding, margin and border** will cause other elements to be **pushed away** from the box.
      - If **not specified**, the box width will extend in the inline direction to **fill** the space available in its container. In most cases, the box will become as wide as its container, filling up 100% of the space available.
        <br>
    - Inline box:
      - The box will **not break** onto a new line.
      - The width and height properties will **not apply** (except for image).
      - **Vertical padding, margins, and borders** will **apply but will not cause other inline boxes to move away** from the box.
      - **Horizontal padding, margins, and borders** will **apply and will cause other inline boxes to move away** from the box.
        <br>

  - ==Inner display type==: how does the element display **within its parent container**.

    - By default and without any other instruction, the elements inside a box are also laid out in normal flow and behave as block or inline boxes.
      - Block elements: content within fills the available inline space of the element, and the element grows along the block dimension to accommodate its content.
      - Inline elements: The size of inline elements is just the size of their content.
        <br>

- common block box elements:
  |`<address>`|`<article>`|`<aside>`|`<blockquote>`|`<canvas>`|`<dd>`|`<div>`|
  |`<dl>`|`<dt>`|`<fieldset>`|`<figcaption>`|`<figure>`|`<footer>`|`<form>`|
  |`<h1>-<h6>`|`<header>`|`<hr>`|`<li>`|`<main>`|`<nav>`|`<noscript>`|
  |`<ol>`|`<p>`|`<pre>`|`<section>`|`<table>`|`<tfoot>`|`<ul>`|`<video>`|

In general, you can set various values for the display type using the `display` property, which can have various values:

- `display: flex`:

<br>

---

### Things that are Good to Know

1. Precedence of style:
   1. Inline style (in HTML style attribute)
   1. ID selector
   1. Class selector
   1. Element selector
      <br>
1. Block-element-modifier ( ==BEM== ) class naming rule:
   - Names are written in **lowercase** Latin letters.
   - Words are separated by a hyphen (-).
   - The **block name** defines the namespace for its elements and modifiers.
   - The **element name** is separated from the block name by a double underscore (\_\_)
     - `block-name__elem-name`
     - ==Elements don't have hierarchy, parent and child html tags should be on the same level when naming class==
   - The **modifier name** is separated from the block or element name by a single underscore (\_).
     - `block-name__elem-name_elem-mod-name`
     - `block-name_block-mod-name__elem-name`
     - ==Modifier should never be used alone, only add modifiers with the original class==
   - The **modifier value** is separated from the modifier name by a single underscore (\_).
     - `block-name__elem-name_mod-name_mod-val`
   - For boolean modifiers, the value is not included in the name.
     <br>
1. ==At-rules== (@idnetifier (RULE)): instruct CSS how to behave.
   - Regular: `@charset`, `@import`, `@namespace`
   - Nested: A subset of nested statements, which can be used as a statement of a style sheet as well as inside of conditional group rules: `@media`, `@keyframe`, `@supports`, `@document`, `@page`, `@font-face`, `@viewport`, `@counter-style`, `@font-feature-values`, `@layer`
   - Conditional group rules: statements that share a common syntax and each can include nested statements, conveying a common semantic meaning which evaluates to either true or false, and the statements will apply under true condition: `@media`, `@supports`, `@document`.
     <br>
1. Use ==Media Queries== when
   - conditionally apply styles with CSS `@media` and `@import` at-rules
   - target specific media for the `<style>`, `<link>`, `<source>`, and other HTML element with the `meida=` attribute
   - test and monitor media states using the `Window.matchMedia()` and `MediaQueryList.addListener()` JavaScript methods
     <br>
1. Some attributes can be ==inherited== from parent element. See `inherited: Yes/no`
   in MDN
   <br>

1. `<script>` should be put right before the end tag of `<body>`, which is `</body>`, so that DOM could be ready when executing script.

   <br>

1. `position: absolute` is positioned relative to its closest positioned ancestor (whose `position` value is not `static`)

   <br>

1. `box-sizing`: sets how the total width and height of an element is calculated
   - `content-box`: (default) content width/height is fixed as element's `width`/`height`, border width and paddings are added upon content width/height
   - `border-box`: element's `width`/`height` includes border width and padding, content width will adapt accordingly.
     <br>
1. `white-space` attribute controls if text could be wrapped.
   <br>

1. `auto` is not a valid value for `padding` attribute;
   <br>
1. To change element color in `<svg>`, add `fill = 'currentColor'` attribute in its tag and change the font color in CSS.
   <br>
1. `transition` defines the transition between two states of an ==element==,
   - only works for ==number value== attribute
   - it is a shorthand property for:
     - `transition-property`
     - `transition-duration`
     - `transition-timing-function`
     - `transition-delay`
       <br>
1. To make the `height` of an element change with `tansition` by toggle classname, don't use `height`, use `max-height` in the transition and set a value on `max-height` to something bigger than your box will ever get.

```

.item-base {
max-height: 0;
transition: all 1s ease;
}

.item-changes {
max-height: 300px; /_ this is way larger than it should reach _/
}

```

<br>

1. `display: flex`

   1. defaults:

      - `flex-direction: row`
      - `justify-content: flex-start`
      - `align-items`: stretch`
      - `flex-wrap: nowrap`
      - `flex-grow: 0`
      - `flex-shrink: 1`
        <br>

   1. `flex-basis` vs `width` / `height`:

      - `flex-basis` only applies to flex items, sets the initial main size of a flex item - can be specific value or percentage: `10em` / `3px` / `50%`
      - can be intrinsic sizing keywords: `max-content` / `min-content` / `fit-content` - `flex-basis` only works with main axis:
      - when `flex-direction` is `row` or `row-reverse`: `flex-basis` control `width`
      - when `flex-direction` is `column` or `column-reverse`: `flex-basis` control `height` - when applied, has higher priority than `width` / `height`, but not higher than `max/min-width/heigth`
      - `flex-basis` has no effect on absolutely-positioned flex items, of which `width` and `height` properties would be necessary
      - `flex` is a shorthand property for `flex-grow`, `flex-shrink` and `flex-basis`.
        <br>

1. `text-align: center`

   - inherited: true
   - horizontal alignment of the **inline box** inside a **block box** or table-cell box
   - this will make all the inline boxes to be centeralized in their parent block boxes
     <br>

1. Margin collapsing:

   - If two ==vertically adjacent== elements both have a margin set on them and their margins touch, the larger of the two margins remains and the smaller one disappears.
     <br>

   - Margins of **floating** and **absolutely** positioned elements never collapse.
   - Margins don't collapse in a container with display set to `flex`.
     <br>

   - 3 basic cases:

     1. Adjacent siblings
     1. No content separating parent and descendants
     1. Empty blocks
        <br>

   - To prevent parent-child element margin collapsing, style the parent element with `overflow` to `hidden` or `auto`.

   - setting `overflow` property establishes a new `block formatting context`, which suppresses margin collapsing
   - `overflow` will not cause content to be hidden or scroll bars to appear as long as the parent element doesn't have a set `height`.
   - margin collapsing only happens within vertical-block margins and flex container's margin doesn't collapse at all.
     <br>

1. ==Bootstrap==:
1. **Content delivery network** ( ==CDN== ) is a quick and easy way of applying css framework, like bootstrap e.g.
   ```
   <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-iYQeCzEYFbKjA/T2uDLTpkwGzCiq6soy8tYaI1GyVh/UjpbCx/TYkiZhlZB6+fzT" crossorigin="anonymous">
   <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-u1OknCvxWvY5kfmNBILK2hRnQC3Pr17a+RTT6rIHI7NnikvbZlHgTPOOmMi466C8" crossorigin="anonymous"></script>
   ```
   - pros: simple & convenient
   - cons: can't customize bootstrap css
1. another way to use bootstrap is to download bootstrap source file (sass source files) and make customized sass and compile it in sass compiler
1. bootstrap 5 doesn't require jquery as a dependency
   <br>

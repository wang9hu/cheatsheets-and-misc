1. `<!DOCTYPE html>`: declaration, meet the industry-wide specifications.
1. `<html>`: represents the root (top-level element) of an HTML document
   - lang= "en"
1. `<head>`: machine-readable information about the document
   1. `<title>`: documents's title shown in a browser's title bar
   1. `<script>`: executable code or data or external resource (e.g. JS files)
   1. `<style>`: style info, just like in CSS
   1. `<link>`: relationships between the current document and an external resource (e.g. CSS files)
      - self-closing tag
      - e.g., `<link rel="stylesheet" href="./css/index.css" />`
   1. `<meta>`: metadata (data about data) that cannot be represented by other elements.
      - self-closing tag
      - can have multiple `<meta>` for one doc
      - attributes:
        - charset= "utf-8"
        - name= "metadata_name" - commonly used together with `content` attribute
        - content= "metadata_content" - e.g. name= "viewpoint" content= "width=device-width"
1. `<body>`:

   1. `<!-- TODO: -->`: comments in html
   1. `<main>`: main content
      - only one `<main>` in doc
      - doesn't contribute to outline
   1. `<header>`: introductory or navigational aids.
      - may contain headings, logo, search from, author name, etc.
   1. `<footer>`: information about the author of the section, copyright data or links to related documents.
   1. `<h1>` to `<h6>`: heading elements
   1. `<p>`: a paragraph of text
   1. `<ul>`: unordered list
      - `<li>`: list item
   1. `<ol>`: ordered list
      - `<li>`: list item
   1. `<br>`: produces a line break in text
      - inline (although its function is to create a new line)
   1. `<em>`: make _italics_
      - inline
   1. `<strong>`: make **bold**
      - inline
   1. `<img>`: add a pic
      - self-closing tag
      - inline
      - attributes:
        - `src` "pic_url"
        - `alt` "text_for_screen_reader"
   1. `<a>`: anchor element, link to another page
      - inline
      - attributes:
        - `target` "where_to_display"
        - `href` "url"
          - "url": could be the following values:
            - a absolute URL (like `http://www.example.com`)
            - a relative URL (like `default.html`)
            - an element with an id within the page (like "#section2")
            - a script
            - other protocols
   1. `<span>`: inline container for phrasing content
      - inline
   1. `<form>`: for submitting information
      - attributes:
        - `action` "where_to_send_data"
        - `method` "get | post | ...": how to send the data
        - `target` "where to display the response that is received after submitting the form."
        - `autocomplete`"on | off": whether a form should have autocomplete on or off
          ...
      - `<form>` elements:
        - `<input>`: interactive controls for web-based forms
          - self-closing tag
          - attributes:
            - `type` "input_type"
            - `name` "represent_data_when_submitted"
            - `value` "input_initial_value" - optional
            - `id` "identification"
              - must be unique
            - `placeholder` "hint for `text` type input"
            - `required`(bool): must fill before submitting for `text` type input
            - `checked`(bool): for `checkbox` type input
        - `<label>`: a caption for an item
          - usually used with `<input>`
          - can be used as
          - `<label><input>LABEL</label>`
          - `<input><label for= "input_id">LABEL</label>`
          - attributes:
            - `for` "item_id"
        - `<fieldset>`: group related elements together
        - `<legend>`: a caption for the `<fieldset>` content
        - `<button>`: interactive element activated by "pressing"
          - inline
          - attributes:
            - `type` "default_behavior"
        - `<textarea>`: defines a multi-line input field
        - `<select>`: defines a drop-down list
          - `<option>`: defines an option that can be selected
   1. `<section>`: generic standalone section with no specific semantic element to represent
      - always have a heading
   1. `<figure>`: large figure with optional caption element
      - `<figcaption>`: optional - a caption or legend describing the rest of the contents
   1. `<article>`: article contents
      - can have multiple `<article>` in doc
      - usually include a heading
      - can have nested elements like `<artilcle>`, `<section>` or `<p>`
      - paralell `<article>` contain same type of info, or different part of info
   1. `<hr>`: thematic break between paragraph-level elements
      - self-closing tag
      - attributes:
        - `height` "height_of_the_line"
        - `background-color`= "color_of_the_line"
   1. `<audio>`: embed sound content in a document, such as music or other audio streams.

      - attributes:

        - `src`"audio_url"
        - `controls`(bool): Specifies that audio controls should be displayed
        - `autoplay`(bool): Specifies that the audio will start playing as soon as it is ready
        - `loop`(bool): Specifies that the audio will start over again, every time it is finished
        - `muted`(bool): Specifies that the audio output should be muted
        - `preload`= "auto | metadata | none" : Specifies if and how the author thinks the audio should be loaded when the page loads

          <br>

    1. `<svg>`: scallable vector graph (**No pixelation**)

---

## Miscellaneous

- HTML tag bool attribute: only two values (true | false), therefore only include its attribute name without value.
  - `<input type="checkbox" checked>` is the same as `<input type="checkbox" checked="checked">`
    <br>
- Element `id` and `name` must **start with letter**, can have numbers, hypens (`-`), underscores (`_`), colons (`:`) and period (`.`)
  <br>

- <span>Emmet abbreviation</span> + enter: (use Tab to jump to next edit position)

  - `!` =>

    ```
    <!DOCTYPE html>
    <html lang="en">
       <head>
          <meta charset="UTF-8">
          <meta http-equiv="X-UA-Compatible" content="IE=edge">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Document</title>
       </head>
       <body>

       </body>
    </html>
    ```

  - `div` => `<div></div>`
  - `div.className` => `<div class="className"></div>`
  - `div#idName` => `<div id="idName"></div>`
  - since `div` is the mostly used element tag, the "div" start can be omitted for `div`:
    - `.className` => `<div class="className"></div>`
    - `#idName` => `<div id="idName"></div>`
    - `[style]` => `<div style=""></div>`
      ...
  - `p[attribute]` => `<p attribute=""></p>`
  - `p[attribute="value"]` => `<p attribute="value"></p>`
  - all chainable:
    - `[style="color: blue"].class-1.class-2#id-1` =>
      `<div style="color: blue" class="class-1 class-2" id="id-1"></div>`
      <br>
  - Children tags: `header>nav>ul` =>

    ```
    <header>
       <nav>
          <ul></ul>
       </nav>
    </header>
    ```

  - Multiple tags `*` with content `{}` and numbering `$`:
    - `li*3.class-${content with number $$}` =>
      ```
      <li class="class-1">content with number 01</li>
      <li class="class-2">content with number 02</li>
      <li class="class-3">content with number 03</li>
      ```
      multiple `$` will pad zeron upfront
    - `lorem`: an abbreviation for generating "Lorem Ipsum" placeholder text, no need for `{}`, default 30 words, add number of word to the end
      - `p>lorem5` => `<p>Lorem ipsum dolor sit amet.</p>`
      - `span*3>lorem3` => `<span>Lorem, ipsum dolor.</span><span>Quod, rem. Velit!</span><span>Esse, nam laudantium!</span>`
        <br>
  - Sibling `+`: `header+main+footer` =>

    ```
    <header></header>
    <main></main>
    <footer></footer>
    ```

  - Grouping `()`: `(header>nav)+main+footer` =>

    ```
    <header>
       <nav></nav>
    </header>
    <main></main>
    <footer></footer>
    ```

    <br>

  - Climb up `^`: `header>nav^footer` =>

    ```
    <header>
      <nav></nav>
    </header>
    <footer></footer>
    ```

    <br>

  - Tag with different categories `:`:
    - `form:post` => `<form action="" method="post"></form>`
    - `input:b|btn|button` => `<input type="button" value="">`
      <br>

- For `<input type="radio">`, a **radio group** is defined by giving each of radio buttons in the group the same `name`, so that a radio group is established, selecting any radio button in that group **automatically deselects** any currently-selected radio button in the same group.
  <br>

- <span>HTML entities</span>: reserved characters in HTML (use HTML reference chart)
  a piece of text ("string") that begins with an ampersand `&` and ends with a semicolon `;`

  - `&_entity_name_;`: &amp; => `&amp;` | &num; => `&num;`
  - `&#_entity_number_;` : &#38; => `&#38;` | &#35; => `&#35;`
  - `&#x_entity_number_;`(hex nubmer) : &#x26; => `&#x26;` | &#x23; => `&#x23;`
    <br>

- <span>MouseEvent</span> `clientX` vs `pageX` vs `screenX` vs `offsetX`
  - `clientX`: visible area on the page
  - `pageX`: entire page area, scrolling doesn't matter
  - `screenX`: entire screen area (window usually not take the whole screen, e.g. browser interface)
  - `offsetX`: relative to the position of the padding edge of the target node
    <br>
- Difference between <span>node</span> and <span>element</span> in DOM

  - a DOM document consists of a hierarchy of **nodes**, each node can have a parent and/or children.
  - There are several types of nodes, which can be represented in `Node.nodetype` property:
    - `Node.ELEMENT_NODE`
    - `Node.ATTRIBUTE_NODE`
    - `Node.TEXT_NODE`
    - `Node.CDATA_SECTION_NODE`
    - `Node.PROCESSING_INSTRUCTION_NODE`
    - `Node.COMMENT_NODE`
    - `Node.DOCUMENT_NODE`
    - `Node.DOCUMENT_TYPE_NODE`
    - `Node.DOCUMENT_FRAGMENT_NODE`

  ```
  <p>Thank you for visiting my web page!</p>

  const paragraph = document.querySelector('p');
  paragraph.nodeType === Node.ELEMENT_NODE; // => true

  // This p tag also has one child node, which is the text 'Thank you for visiting my web page!'
  paragraph.firstChild.nodeType === Node.TEXT_NODE // => true
  ```

  - An **element** is just a node that's written using a tag in the HTML document.
  <br>

- <span>className vs classList</span>:
  - `Element.className`: a string representing the class(s) of the element, seperated by space.
  - `Element.classList`: (read-only) returns a live `DOMTokenList` collection of the class attribute of the element.
  ```
  const div = document.createElement('div');
  div.className = 'col border text-center'; // A string.
  div.classList = ['col', 'border', 'text-center'] // A DOMTokenList, not an array
  ```
    - To turn `DOMTokenList` into an `array`, use `const elementArray = Array.from(DOMTokenList)`
      <br>
- <span>srollHeight vs clientHeight vs offsetHeight</span>:
  - `Element.scrollHeight`: (read-only) returns the minimum height the element would require in order to fit all the content in the viewport without using a vertical scrollbar, including content not visible on the screen due to overflow.
  - `Element.clientHeigth`: (read-only) returns the height of an element's content.
    - both including padding but excludes borders, margins, and horizontal scrollbars.
    - `scrollHeight` doesn't care about the text content if `Element` is a `textarea`, if no content inside `textarea`, it will just show the rendered `height`.
    - If the element's content can fit without a need for a vertical scrollbar, its `scrollHeight` equal to its `clientHeight`
  - `Element.offsetHeight`: (read-only) returns the viewable height of an element (in pixels), including padding, border and scrollbar, but not the margin.
    <br>
- <span>innerHTML vs innerText vs textContent</span>

  - `Element.innerHTML`: The text content of the element, including all spacing and inner HTML tags.
  - `Element.innerText`: Just the text content of the element and all its children, without CSS hidden text spacing and tags, except `<script>` and `<style>` elements.
  - `Element.textContent`: The text content of the element and all descendaces, with spacing and CSS hidden text, but without tags.

  ```
  // HTML
  <div id="mylinks">
    This is my <b>link collection</b>:
    <ul>
      <li><a href="www.borland.com">Bye bye <b>Borland</b> </a></li>
      <li><a href="www.microfocus.com">Welcome to <b>Micro Focus</b></a></li>
    </ul>
  </div>
  ```

  ```
  // JS
  const div = document.getElementById('mylinks');

  console.log(div.textContent) // This is my link collection:

  console.log(div.innerText) // This is my link collection:Bye bye Borland Welcome to Micro Focus

  console.log(div.innerHTML)
  // This is my <b>link collection</b>:
  // <ul>
  //   <li><a href="www.borland.com">Bye bye <b>Borland</b></a></li>
  //   <li><a href="www.microfocus.com">Welcome to <b>Micro Focus</b></a></li>
  // </ul>
  ```

    <br>

- <span>querySelector</span>:

  - `Element.querySelector(selector(s))`: returns the first Element within the document that matches the specified CSS `selector`, or group of `selectors`. If no matches are found, null is returned.
    - `selector(s)`:
      - Universal selector: `*`
      - Type selector: `tagname`
      - Class selector: `.classname`
      - ID seletor: `#id`
      - Attribute selector:
        - `[attr]`: has attribute
        - `[attr=value]`: equal to value
        - `[attr~=value]`: contain and space-separated
        - `[attr|=value]`: contain and as a whole or be followed by `-`
        - `[attr^=value]`: contain and starts with value, not necessarily have to be a whole word
        - `[attr$=value]`: contain and ends with value, not necessarily have to be a whole word
        - `[attr*=value]`: contain, no other limits.
    - Grouping selectors:
      - Selector list: `,`
    - Combinators:
      - Descendant combinator: space '` `'
      - Child combinator: `>`
      - General sibling combinator: `~`
      - Adjacent sibling combinator: `+`
      - Column combinator: `||`
    - Pseudo-classes and pseudo-elements: `:` / `::`
      <br>

- <span>Event Listener</span>: `addEventListener(type, listener, options/capture?)`:

  - By default, event listeners are executed in a process known as <span>bubbling</span>, where the event starts at the target element, then <span>propagates</span> up the DOM tree to its parent elements, executing event listeners on each element along the way, until it reaches the root element.
    <br>
  - `listener`: The object that receives a notification (an object that implements the Event interface) when an event of the specified type occurs.
    - can be a callback function ro an object whose `handeEvent()` method servers as the callback function
    - `e.preventDefault()`: if the event does not get explicitly handled, its default action should not be taken as it normally would be
    - `e.stopPropagation()`: prevents further propagation of the current event in the capturing and bubbling phases (to parent or other element)
      <br>
  - `options`: _optional_ An object that specifies characteristics about the event listener `{...}`

    - `capture` (bool): _optional_ If `true`, the event listeners are executed in the opposite order, starting at the root element and propagating down the DOM tree to the target element, before finally reaching the end of the propagation phase. Default `false`
    - `once` (bool): If `true`, the `listener` would be automatically removed when invoked. Default `false`
    - `passive` (bool): If `true`, `listener` will never call `preventDefault()`. Default `false`
    - `signal`: The listener will be removed when the given `AbortSignal` object's `abort()` method is called (Same as `removeEventListener(type, listerner, options/useCapture?)`). If not specified, no `AbortSignal` is associated with the listener.

      ```
      const controller = new AbortController();
      const signal = controller.signal;
      document.getElementById('myButton').addEventListener('click', handleClick, { signal});

      setTimeout(() => {
        controller.abort();
      }, 5000);
      ```
      <br>

  
- Event Propagation: <span>Capturing</span> vs <span>Bubbling</span>
  - <span>Propagation</span>: how events travel through the DOM tree.
    - `event.stopPropagation()`: doesn't propagate the event;
  <br>
  - When an <span>event</span> is triggered on a child element, and its parent element and root element also have the same eventlistener:
    - <span>Bubbling</span>: event trigger order is: <span>child</span> -> <span>parent</span> -> <span>root</span>
    - <span>Capturing</span>: event trigger order is : <span>root</span> -> <span>parent</span> -> <span>child</span>
    <br>
  - <span>W3C model</span>:  first **captured** until it reaches the **target element** and then **bubbles up** again.
    ```
    root             | |  / \
    -----------------| |--| |-----------------
    | element1       |1|  |2|                |
    |   -------------| |--| |-----------     |
    |   |element2    \ /  | |          |     |
    |   --------------------------------     |
    |        W3C event model                 |
    ------------------------------------------
    ```
    - use `addEventListener(event, callback, useCapture)` to handle propagation.
      - `useCapture`: default `false` is bubbling phase, if `true` is capturing phase
      - e.g. If:
        `root.addEventListener('click',doSomethingR,false) &&
        element1.addEventListener('click',doSomething1,true) &&
        element2.addEventListener('click',doSomething2,false);`
        1. Click `element2`, event propagation starts
        2. event starts capturing phase: `root`->`element2`->`element2`
        3. `root` is in bubbling phase, pass
        4. `element1` is in capturing phase, `doSomething1` trigger 
        5. `element2` is the target element, `doSomething2` trigger
        6. event starts bubbling phase: `element2`->`element1`->`root`
        7. `element1` is in capturing phase, pass
        8. `root` is in bubbling phase, `doSomethingR` trigger
        9. event propagation finishes.
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
        - _src_= "pic_url"
        - _alt_= "text_for_screen_reader"
   1. `<a>`: anchor element, link to another page
      - inline
      - attributes:
        - _target_= "where_to_display"
        - _href_= "url"
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
        - _action_= "where_to_send_data"
        - _method_= "get | post | ...": how to send the data
        - _target_= "where to display the response that is received after submitting the form."
        - _autocomplete_="on | off": whether a form should have autocomplete on or off
          ...
      - `<form>` elements:
        - `<input>`: interactive controls for web-based forms
          - self-closing tag
          - attributes:
            - _type_= "input_type"
            - _name_= "represent_data_when_submitted"
            - _value_= "input_initial_value" - optional
            - _id_= "identification"
              - must be unique
            - _placeholder_= "hint _for_ `text`\_type_input"
            - _required_ (bool): must fill before submitting for `text` type input
            - _checked_ (bool): for `checkbox` type input
        - `<label>`: a caption for an item
          - usually used with `<input>`
          - can be used as
          - `<label><input>LABEL</label>`
          - `<input><label for= "input_id">LABEL</label>`
          - attributes:
            - _for_= "item_id"
        - `<fieldset>`: group related elements together
        - `<legend>`: a caption for the `<fieldset>` content
        - `<button>`: interactive element activated by "pressing"
          - inline
          - attributes:
            - _type_= "default_behavior"
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
        - _height_= "height_of_the_line"
        - _background-color_= "color_of_the_line"
   1. `<audio>`: embed sound content in a document, such as music or other audio streams.

      - attributes:

        - _src_="audio_url"
        - _controls_ (bool): Specifies that audio controls should be displayed
        - _autoplay_ (bool): Specifies that the audio will start playing as soon as it is ready
        - _loop_ (bool): Specifies that the audio will start over again, every time it is finished
        - _muted_ (bool): Specifies that the audio output should be muted
        - _preload_ = "auto | metadata | none" : Specifies if and how the author thinks the audio should be loaded when the page loads

          <br>

---

## Miscellaneous

- HTML tag bool attribute: only two values (true | false), therefore only include its attribute name without value.
  - `<input type="checkbox" checked>` is the same as `<input type="checkbox" checked="checked">`
    <br>
- Element `id` and `name` must **start with letter**, can have numbers, hypens (`-`), underscores (`_`), colons (`:`) and period (`.`)
  <br>

- ==Emmet abbreviation== + enter: (use Tab to jump to next edit position)

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

  - Tag with different categories `:`:
    - `form:post` => `<form action="" method="post"></form>`
    - `input:b|btn|button` => `<input type="button" value="">`
      <br>

- For `<input type="radio">`, a **radio group** is defined by giving each of radio buttons in the group the same `name`, so that a radio group is established, selecting any radio button in that group **automatically deselects** any currently-selected radio button in the same group.
  <br>

- ==HTML entities==: reserved characters in HTML (use HTML reference chart)
  a piece of text ("string") that begins with an ampersand `&` and ends with a semicolon `;`

  - `&_entity_name_;`: &amp; => `&amp;` | &num; => `&num;`
  - `&#_entity_number_;` : &#38; => `&#38;` | &#35; => `&#35;`
  - `&#x_entity_number_;`(hex nubmer) : &#x26; => `&#x26;` | &#x23; => `&#x23;`
    <br>

- ==MouseEvent==: `clientX` vs `pageX` vs `screenX` vs `offsetX`
  - `clientX`: visible area on the page
  - `pageX`: entire page area, scrolling doesn't matter
  - `screenX`: entire screen area (window usually not take the whole screen, e.g. browser interface)
  - `offsetX`: relative to the position of the padding edge of the target node
    <br>
- Difference between ==node== and ==element== in DOM

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

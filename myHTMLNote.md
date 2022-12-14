1. `<!DOCTYPE html>`: declaration, meet the industry-wide specifications.
1. `<html>`: represents the root (top-level element) of an HTML document
   - lang= "en"
1. `<head>`: machine-readable information about the document
   1. `<title>`: documents's title shown in a browser's title bar
   1. `<script>`: executable code or data or external resource (e.g. JS files)
   1. `<style>`: style info, just like in CSS
   1. `<link>`: relationships between the current document and an external resource (e.g. CSS files)
      - self-closing tag
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
        - _href_= "url"
        - _target_= "where_to_display"
        - "url": could be the following values:
          - a absolute URL (like "http://www.example.com")
          - a relative URL (like "default.html")
          - an element with an id within the page (like "#section2")
          - a script
          - other protocols
   1. `<span>`: inline container for phrasing content
      - inline
   1. `<form>`: for submitting information
      - attributes:
        - _action_= "where_to_send_data"
        - _method_= "how to send the data": get / post
        - _target_= "where to display the response that is received after submitting the form."
        - _autocomplete_="whether a form should have autocomplete on or off": on / off
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
            - _placeholder_= "hint *for* `text`\_type_input"
            - _required_: must fill before submitting for `text` type input
            - _checked_: for `checkbox` type input
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

<br>

---

## Miscellaneous

- Element `id` and `name` must **start with letter**, can have numbers, hypens (`-`), underscores (`_`), colons (`:`) and period (`.`)
<br>
- For `<input type="radio">`, a **radio group** is defined by giving each of radio buttons in the group the same `name`, so that a radio group is established, selecting any radio button in that group **automatically deselects** any currently-selected radio button in the same group.
<br>
- ==inline-level== elements: do not force a new line to begin
  - on seperate lines in `html` code creates an extra space to the right of the first elements
- ==block-level== elements: take up entire widith of parent element
  - in this file, elements that not labeled as inline elements are block-level elements
    <br>
- To prevent parent-child element margin collapsing, style the parent element with `overflow` to `hidden` or `auto`.

  - setting `overflow` property establishes a new `block formatting context`, which suppresses margin collapsing
  - `overflow` will not cause content to be hidden or scroll bars to appear as long as the parent element doesn't have a set `height`.
  - margin collapsing only happens within vertical-block margins and flex container's margin doesn't collapse at all.

  <br>

- HTML entities: reserved characters in HTML
  - &_entity_name_
  - &#_entity_number_ (decimal)
  - &#==x==_entity_number_ (hex)
  <br>

- MouseEvent: clientX vs pageX vs screenX vs offsetX
   - clientX: visible area on the page
   - pageX: entire page area, scrolling doesn't matter
   - screenX: entire screen area
   - offsetX: relative to the position of the padding edge of the target node
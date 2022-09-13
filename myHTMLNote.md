1. `<!DOCTYPE html>`: declaration, meet the industry-wide specifications.
1. `<html>`: represents the root (top-level element) of an HTML document
   - lang="en"
1. `<head>`: machine-readable information about the document
   1. `<title>`: documents's title shown in a browser's title bar
   1. `<script>`: executable code or data or external resource (e.g. JS files)
   1. `<style>`: style info
   1. `<link>`: relationships between the current document and an external resource (e.g. CSS files)
      - self-closing
   1. `<meta>`: metadata (data about data) that cannot be represented by other elements.
      - self-closing
      - can have multiple `<meta>` for one doc
      - attributes:
        - charset="utf-8"
        - name="metadata_name" - commonly used together with `content` attribute
        - content="metadata_content" - e.g. name="viewpoint" content="width=device-width"
1. `<body>`:
   1. `<!-- TODO: -->`: comments in html
   1. `<h1>` to `<h6>`: heading elements
   1. `<p>`: a paragraph of text
      - block-level: take up entire widith of parent element
   1. `<ul>`: unordered list
      - `<li>`: list item
   1. `<ol>`: ordered list
      - `<li>`: list item
   1. `<em>`: make _italics_
   1. `<strong>`: make **bold**
   1. `<img>`: add a pic
      - self-closing
      - attributes:
        - src="pic_url"
        - alt="text_for_screen_reader"
   1. `<a>`: anchor element, link to another page
      - inline: do not force a new line to begin
      - attributes:
        - href="url"
        - target="where_to_display"
   1. `<form>`: for submitting information
      - attributes:
        - action="where_to_send_data"
   1. `<input>`: interactive controls for web-based forms
      - self-closing
      - attributes:
        - type="input_type"
        - name="represent_data_when_submitted"
        - value="input_initial_value" - optional
        - id="identification"
          - must be unique
        - placeholder="hint*for*`text`\_type_input"
        - required: must fill before submitting for `text` type input
        - checked: for `checkbox` type input
   1. `<label>`: a caption for an item
      - usually used with `<input>`
      - can be used as
        - `<label><input>LABEL</label>`
        - `<input><label for="input_id">LABEL</label>`
      - attributes:
        - for="item_id"
   1. `<button>`: interactive element activated by "pressing"
      - inline element
      - attributes:
        - type="default_behavior"
   1. `<fieldset>`: group related elements together
      - `<legend>`: a caption for the `<fieldset>` content
   1. `<section>`: generic standalone section with no specific semantic element to represent
      - always have a heading
   1. `<main>`: main content
      - only one `<main>` in doc
      - doesn't contribute to outline
   1. `<figure>`: large figure with optional caption element
      - `<figcaption>`: optional - a caption or legend describing the rest of the contents
   1. `<article>`: article contents
      - can have multiple `<article>` in doc
      - usually include a heading
      - can have nested elements like `<artilcle>`, `<section>` or `<p>`
      - paralell `<article>` contain same type of info, or different part of info
   1. `<footer>`: information about the author of the section, copyright data or links to related documents.
   1. `<hr>`: thematic break between paragraph-level elements
      - self-closing
      - attributes:
        - height="height_of_the_line"
        - background-color="color_of_the_line"

<br>

---

## Miscellaneous

- `inline` elements on seperate lines in `html` code creates an extra space to the right of the first elements

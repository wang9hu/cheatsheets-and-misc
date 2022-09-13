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

CSS selectors:

1. Simple:

   - by element: `a { color: red }`
   - by class: `.className { color: red }`
   - by id: `#idName { color: red }`
   - universal: `* { color: red }`
   - grouping: `a, p { color: red }`
     <br>

2. Combinators:

   - descendant(space): `div p { color: red }` **Text 1** and **Text 2** will change
   - child(>): `div > p { color: red }` only **Text 1** will change
   - adjacent sibling(+): `div + p { color: red }` only **Text 3** will change
   - general sibling(~): `div ~ p { color: red }` **Text 3** and **Text 4** will change
     <br>

3. Pseudo-classes selector (**:**) style an element when it is (commonly used):

   - mouse hovered: `div:hover { background-color: green }`
   - being clicked: `a:active { background-color: green }`
   - focused: ` input:focus { background-color: green }`
   - first-child of another element: `p:first-child { color: red }`
   - last-child of another element: `p:last-child { color: red }`
     ...
     <br>

4. Pseudo-elements selector (**::**) style specified parts of an element:

   - first letter: `p::first-letter { color: #ff0000 }`
   - first line: `p::first-line { color: #ff0000 }`
   - insert before: `p::before { content: url }`
   - inser after: `p::after { content: url }`
   - highlighted parts: `p::selection { color: red }`
   - marker of list items: `::marker { color: red }`
     <br>

5. Attribute selector style elements with specific attributes or attribute values:
   - attribute: `a[id] { background-color: yellow }`
   - attribute value: `a[id='idName'] { background-color: yellow }`
     ... atrribute value variants
     <br>

# DOM

- [DOM](#dom)
  - [Accessing some topmost level tags on a webpage](#accessing-some-topmost-level-tags-on-a-webpage)
  - [Checking if an element or node has child nodes](#checking-if-an-element-or-node-has-child-nodes)
  - [Retrieving the collection of child nodes](#retrieving-the-collection-of-child-nodes)
  - [Accessing the child nodes](#accessing-the-child-nodes)
  - [Accessing the sibling nodes](#accessing-the-sibling-nodes)
  - [Accessing the parent node](#accessing-the-parent-node)
  - [Working with child elements](#working-with-child-elements)
  - [Accessing the child elements](#accessing-the-child-elements)
  - [Accessing the sibling elements](#accessing-the-sibling-elements)
  - [Accessing the parent element](#accessing-the-parent-element)
  - [Accessing the element by its `id`](#accessing-the-element-by-its-id)
  - [Table properties](#table-properties)
  - [Select elements using CSS selectors](#select-elements-using-css-selectors)
  - [Check if an element matches a CSS selector](#check-if-an-element-matches-a-css-selector)
  - [Select the nearest ancestor that matches a CSS selector](#select-the-nearest-ancestor-that-matches-a-css-selector)
  - [Select the HTML of an element](#select-the-html-of-an-element)
  - [Select the text of an element](#select-the-text-of-an-element)
  - [Retrieving the name of an HTML tag or node](#retrieving-the-name-of-an-html-tag-or-node)
  - [Hiding an HTML element](#hiding-an-html-element)
  - [Input properties](#input-properties)
  - [Anchor element's `href` property](#anchor-elements-href-property)
  - [Working with HTML tag attributes](#working-with-html-tag-attributes)
  - [The `style` object](#the-style-object)
  - [Retrieving the style information of an element](#retrieving-the-style-information-of-an-element)
  - [Working with Attributes starting with `data-`](#working-with-attributes-starting-with-data-)
  - [Creating an HTML element](#creating-an-html-element)
  - [Creating a text node](#creating-a-text-node)
  - [Adding elements to the DOM](#adding-elements-to-the-dom)
  - [Insert an HTML string with `<element>.insertAdjacentHTML(<where>, <html>)`](#insert-an-html-string-with-elementinsertadjacenthtmlwhere-html)
  - [Insert Text with `<element>.insertAdjacentText(<where>, <text>)`](#insert-text-with-elementinsertadjacenttextwhere-text)
  - [Remove a node from the DOM](#remove-a-node-from-the-dom)
  - [Copy a node](#copy-a-node)
  - [Dealing with HTML Classes](#dealing-with-html-classes)
  - [Accessing the positioned ancestor of HTML element](#accessing-the-positioned-ancestor-of-html-element)
  - [Retrieving the coordinates of an element relative to `<element>.offsetParent`](#retrieving-the-coordinates-of-an-element-relative-to-elementoffsetparent)
  - [Retrieving the width and height of an element](#retrieving-the-width-and-height-of-an-element)
  - [Deal with scrolling on a screen](#deal-with-scrolling-on-a-screen)
  - [Retrieve the element size and coordinates with `getBoundingClientRect`](#retrieve-the-element-size-and-coordinates-with-getboundingclientrect)
  - [Retrieving the element coordinates with `elementFromPoint`](#retrieving-the-element-coordinates-with-elementfrompoint)

---

---

## Accessing some topmost level tags on a webpage

- To get the topmost document node - the `<html>` tag, we can use the `document.documentElement`.
- To get the `head` element, we can use `document.head`.
- For the `body` element, we can use `document.body`.

```js
console.log(document); // HTMLDocument
console.log(document.head); // <head>
console.log(document.body); // <body>
console.log(document.documentElement); // <html lang="en">
```

<hr>

## Checking if an element or node has child nodes

If we want to check if a node has child nodes, we can use `<node>.hasChildNodes()`. It returns `true` or `false`.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.hasChildNodes()); // true
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(document.body.childNodes[0]); // #text "\n  "
    console.log(document.body.childNodes[0].hasChildNodes()); // false
    console.log(document.body.childNodes[0].childNodes); // NodeList []
  </script>
</body>
```

## Retrieving the collection of child nodes

To get collection of (immediate) child nodes of an element, we use `<node>.childNodes`.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.documentElement.childNodes); // NodeList(3) [ head, #text, body ]
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]
  </script>
</body>
```

We can use `for..of` to iterate over `childNodes`. But array methods won't work on it, because `childNodes` is not an array. It's a collection, and we can use `Array.from()` to create an array from it.

Here is an example of using `for..of` with `childNodes`:

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    for (let node of document.documentElement.childNodes) {
      console.log(node);
      // head, #text "\n", body
    }

    for (let node of document.body.childNodes) {
      console.log(node);
      // #text "\n", h1, #text "\n  ", p, #text "\n  ", script, #text "\n  ", script
    }
  </script>
</body>
```

Here is an example of using `Array.from()` with `childNodes`:

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(Array.from(document.body.childNodes));
    // Array(8) [ #text, h1, #text, p, #text, script, #text, script ]
  </script>
</body>
```

<hr>

## Accessing the child nodes

`<node>.firstChild` gets the first child node. It's the same as `document.<node>.childNodes[0]`.

`<node>.lastChild` gets the last child. It's the same as `document.<node>.childNodes[document.<node>.childNodes.length-1]`.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(document.body.firstChild); // #text "\n  "
    console.log(document.body.lastChild); // <script>

    // same as above
    console.log(document.body.childNodes[0]); // #text "\n  "
    console.log(document.body.childNodes[document.body.childNodes.length - 1]); // <script>
  </script>
</body>
```

<hr>

## Accessing the sibling nodes

To get the sibling nodes we can use `<node>.nextSibling` and `<node>.previousSibling`

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(document.body.childNodes[1]); // <h1>

    console.log(document.body.childNodes[1].previousSibling); // #text "\n  "
    console.log(document.body.childNodes[0]); // #text "\n  ", this is the same node as the above one

    console.log(document.body.childNodes[1].nextSibling.nextSibling); // <p>
    console.log(document.body.childNodes[3]); // <p>, this is the same node as the above one
  </script>
</body>
```

<hr>

## Accessing the parent node

`<node>.parentNode` helps to get the parent node.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(document.body.childNodes[0]); // #text
    console.log(document.body.childNodes[0].parentNode); // <body>

    console.log(document.body.childNodes[1]); // <h1>
    console.log(document.body.childNodes[1].parentNode); // <body>
  </script>
</body>
```

<hr>

## Working with child elements

Navigation properties listed above refer to all nodes. For instance, in `childNodes` we can see text nodes, element nodes, and even comment nodes, if they exist. But for many tasks, we don’t want text or comment nodes. We want to manipulate element nodes that represent tags and form the structure of the page.

To get the element nodes of an element, we can use `<node>.children`.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes);
    // NodeList(8) [ #text, h1, #text, p, #text, script, #text, script ]

    console.log(document.body.children);
    // HTMLCollection(4) [h1, p, script, script]
  </script>
</body>
```

<hr>

## Accessing the child elements

- `<node>.firstElementChild` helps to get the first child element.
- `<node>.lastElementChild` helps to get the last child element.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.firstElementChild); // <h1>
    console.log(document.body.lastElementChild); // <script>

    console.log(document.body.children[0]); // <h1>
    console.log(document.body.children[document.body.children.length - 1]); // <script>
  </script>
</body>
```

<hr>

## Accessing the sibling elements

`<node>.previousElementSibling` and `<node>.nextElementSibling` help to get neighboring elements.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.children);
    // HTMLCollection { 0: h1, 1: p, 2: script, 3: script, length: 4 }

    console.log(document.body.children[1]); // <p>

    console.log(document.body.children[1].previousElementSibling); // <h1>
    console.log(document.body.children[0]); // <h1>, this is the same node as the above one

    console.log(document.body.children[1].nextElementSibling); // <script src="./index.js">
    console.log(document.body.children[2]); // <script src="./index.js">, this is the same node as the above one
  </script>
</body>
```

<hr>

## Accessing the parent element

`<node>.parentElement` helps to get the parent element.

```html
<body>
  <h1>Heading</h1>
  <p>Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.children);
    // HTMLCollection { 0: h1, 1: p, 2: script, 3: script, length: 4 }

    console.log(document.body.children[0]); // <h1>
    console.log(document.body.children[0].parentElement); // <body>

    console.log(document.body.children[1]); // <p>
    console.log(document.body.children[1].parentElement); // <body>
  </script>
</body>
```

<hr>

## Accessing the element by its `id`

`document.getElementById("<Id>")` gets the element with the specific Id. Also, `window.<Id>`, `window[<Id>]` and even `<Id>` alone work but they are not advisable.

```html
<body>
  <h1 id="heading">Heading</h1>
  <p id="paragraph">Paragraph</p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.children);
    // HTMLCollection { 0: h1#heading, 1: p#paragraph, 2: script, 3: script, length: 4, … }

    const headingElem = document.getElementById("heading");
    console.log(headingElem); // <h1 id="heading">

    // These are not preferred, but possible
    console.log(window.heading); // <h1 id="heading">
    console.log(window["heading"]); // <h1 id="heading">
    console.log(heading); // <h1 id="heading">
  </script>
</body>
```

<hr>

## Table properties

There are also some element-specific properties. For example, `<table>` tag has its own properties that helps to access and manipulate table-related tags.

- `<table>.caption` - reference to the `<caption>` element.
- `<table>.tHead` - reference to the `<thead>` element.
- `<table>.tBodies` - the collection of `<tbody>` elements
- `<table>.tFoot` - reference to the `<tfoot>` element.

These properties help to select different parts of a table:

```html
<style>
  table {
    border: 1px solid black;
    border-collapse: collapse;
  }

  th,
  td {
    border: 1px solid black;
  }
</style>
<body>
  <table id="tableId">
    <caption>
      Title for the Table
    </caption>
    <thead>
      <tr>
        <th scope="col" rowspan="2">Header 1</th>
        <th scope="col" colspan="2">Header 2</th>
        <th scope="col" rowspan="2">Header 3</th>
      </tr>
      <tr>
        <th scope="col">Subheader 2.1</th>
        <th scope="col">Subheader 2.2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Cell 1.1</th>
        <td>Cell 1.2</td>
        <td>Cell 1.3</td>
        <td>Cell 1.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 2.1</th>
        <td>Cell 2.2</td>
        <td>Cell 2.3</td>
        <td>Cell 2.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 3.1</th>
        <td>Cell 3.2</td>
        <td>Cell 3.3</td>
        <td>Cell 3.4</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <th colspan="3">Footer Header</th>
        <td>Footer cell</td>
      </tr>
    </tfoot>
  </table>

  <script src="./index.js"></script>
  <script>
    const table = document.getElementById("tableId");
    console.log(table); // <table id="tableId">

    // different parts of the table
    console.log(table.caption); // <caption>
    console.log(table.tHead); // <thead>
    console.log(table.tBodies); // HTMLCollection { 0: tbody, length: 1 }
    console.log(table.tBodies[0]); // <tbody>
    console.log(table.tFoot); // <tfoot>
  </script>
</body>
```

The rows of the table as a whole or the rows within different parts of the table could be selected as well, using the `rows` property:

- `<table>.rows` - the collection of `<tr>` elements of the table.
- `<thead>.rows` - the collection of `<tr>` inside `<thead>`.
- `<tbody>.rows` - the collection of `<tr>` inside `<tbody>`.
- `<tfoot>.rows` - the collection of `<tr>` inside `<tfoot>`.

```html
<body>
  <table id="tableId">
    <caption>
      Title for the Table
    </caption>
    <thead>
      <tr>
        <th scope="col" rowspan="2">Header 1</th>
        <th scope="col" colspan="2">Header 2</th>
        <th scope="col" rowspan="2">Header 3</th>
      </tr>
      <tr>
        <th scope="col">Subheader 2.1</th>
        <th scope="col">Subheader 2.2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Cell 1.1</th>
        <td>Cell 1.2</td>
        <td>Cell 1.3</td>
        <td>Cell 1.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 2.1</th>
        <td>Cell 2.2</td>
        <td>Cell 2.3</td>
        <td>Cell 2.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 3.1</th>
        <td>Cell 3.2</td>
        <td>Cell 3.3</td>
        <td>Cell 3.4</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <th colspan="3">Footer Header</th>
        <td>Footer cell</td>
      </tr>
    </tfoot>
  </table>

  <script src="./index.js"></script>
  <script>
    const table = document.getElementById("tableId");
    console.log(table); // <table id="tableId">

    // collection of rows
    console.log(table.rows);
    // HTMLCollection { 0: tr, 1: tr, 2: tr, 3: tr, 4: tr, 5: tr, length: 6 }

    console.log(table.tHead.rows); // HTMLCollection { 0: tr, 1: tr, length: 2 }
    console.log(table.tBodies[0].rows); // HTMLCollection { 0: tr, 1: tr, 2: tr, length: 3 }
    console.log(table.tFoot.rows); // HTMLCollection { 0: tr, length: 1 }
  </script>
</body>
```

We can also retrieve the row number of a `<tr>` tag:

- `<tr>.sectionRowIndex` - the position (index) of the given `<tr>` inside the enclosing `<thead>`/`<tbody>`/`<tfoot>`.
- `<tr>.rowIndex` - the number of the `<tr>` in the table as a whole (including all table rows).

```html
<body>
  <table id="tableId">
    <caption>
      Title for the Table
    </caption>
    <thead>
      <tr>
        <th scope="col" rowspan="2">Header 1</th>
        <th scope="col" colspan="2">Header 2</th>
        <th scope="col" rowspan="2">Header 3</th>
      </tr>
      <tr>
        <th scope="col">Subheader 2.1</th>
        <th scope="col">Subheader 2.2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Cell 1.1</th>
        <td>Cell 1.2</td>
        <td>Cell 1.3</td>
        <td>Cell 1.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 2.1</th>
        <td>Cell 2.2</td>
        <td>Cell 2.3</td>
        <td>Cell 2.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 3.1</th>
        <td>Cell 3.2</td>
        <td>Cell 3.3</td>
        <td>Cell 3.4</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <th colspan="3">Footer Header</th>
        <td>Footer cell</td>
      </tr>
    </tfoot>
  </table>

  <script src="./index.js"></script>
  <script>
    const table = document.getElementById("tableId");
    console.log(table); // <table id="tableId">

    // collection of rows
    console.log(table.rows);
    // HTMLCollection { 0: tr, 1: tr, 2: tr, 3: tr, 4: tr, 5: tr, length: 6 }

    // The row number of `<tr>` inside the enclosing `<thead>`/`<tbody>`/`<tfoot>`
    console.log(table.tHead.rows[0].sectionRowIndex); // 0
    console.log(table.tHead.rows[1].sectionRowIndex); // 1

    // the row number of the `<tr>` in the table as a whole
    console.log(table.tHead.rows[0].rowIndex); // 0

    // the difference between sectionRowIndex and rowIndex
    console.log(table.tFoot.rows[0].sectionRowIndex); // 0
    console.log(table.tFoot.rows[0].rowIndex); // 5
  </script>
</body>
```

We can also select the individual cells, and retrieve the number of a cell within the row:

- `<tr>.cells` - the collection of `<td>` and `<th>` cells inside the given `<tr>`.
- `td.cellIndex` - the number of a cell inside the enclosing `<tr>`.

```html
<body>
  <table id="tableId">
    <caption>
      Title for the Table
    </caption>
    <thead>
      <tr>
        <th scope="col" rowspan="2">Header 1</th>
        <th scope="col" colspan="2">Header 2</th>
        <th scope="col" rowspan="2">Header 3</th>
      </tr>
      <tr>
        <th scope="col">Subheader 2.1</th>
        <th scope="col">Subheader 2.2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">Cell 1.1</th>
        <td>Cell 1.2</td>
        <td>Cell 1.3</td>
        <td>Cell 1.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 2.1</th>
        <td>Cell 2.2</td>
        <td>Cell 2.3</td>
        <td>Cell 2.4</td>
      </tr>
      <tr>
        <th scope="row">Cell 3.1</th>
        <td>Cell 3.2</td>
        <td>Cell 3.3</td>
        <td>Cell 3.4</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <th colspan="3">Footer Header</th>
        <td>Footer cell</td>
      </tr>
    </tfoot>
  </table>

  <script src="./index.js"></script>
  <script>
    const table = document.getElementById("tableId");
    console.log(table); // <table id="tableId">

    // collection of cells
    console.log(table.tHead.rows[0].cells); // HTMLCollection { 0: th, 1: th, 2: th, length: 3 }
    console.log(table.tBodies[0].rows[0].cells); // HTMLCollection { 0: th, 1: td, 2: td, 3: td, length: 4 }
    console.log(table.tFoot.rows[0].cells); // HTMLCollection { 0: th, 1: td, length: 2 }

    // individual cells
    console.log(table.tHead.rows[0].cells[0]); // < th scope = "col" rowspan = "2" >

    // the cell number inside the enclosing <tr>
    console.log(table.tHead.rows[0].cells[0].cellIndex); // 0
    console.log(table.tHead.rows[0].cells[1].cellIndex); // 1

    console.log(table.tHead.rows[1].cells[0].cellIndex); // 0
    console.log(table.tHead.rows[1].cells[1].cellIndex); // 1
  </script>
</body>
```

<hr>

## Select elements using CSS selectors

Below two DOM methods are very useful. Using these we access the HTML elements using the elements' CSS selectors.

- `querySelectorAll("<css>")` returns all elements inside body matching the given CSS selector.
- `querySelector("<css>")` returns the first element inside body matching the given CSS selector.

```html
<body>
  <h1 id="headingId">Heading</h1>

  <section class="paragraphsSection">
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <p>Paragraph 3</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const paragraphs = document.querySelectorAll("p");
    console.log(paragraphs); // NodeList(3) [ p, p, p ]

    const heading = document.querySelector("#headingId");
    console.log(heading); // <h1 id="headingId">

    const paragraphsSection = document.querySelector(".paragraphsSection");
    console.log(paragraphsSection); // <section class="paragraphsSection">
  </script>
</body>
```

<hr>

## Check if an element matches a CSS selector

`matches("<css>")` checks if an element matches the given CSS-selector.

```html
<body>
  <h1 id="headingId">Heading</h1>

  <script src="./index.js"></script>
  <script>
    const heading = document.querySelector("#headingId");
    console.log(heading.matches("#headingId")); // true
    console.log(heading.matches("h1")); // true
  </script>
</body>
```

<hr>

## Select the nearest ancestor that matches a CSS selector

`closest("<css>")` looks for the nearest ancestor that matches the CSS-selector. The element itself is also included in the search.

```html
<body>
  <section class="outerSection">
    <section>
      <h2>Paragraph Heading</h2>
    </section>
    <section class="innerSection">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
    </section>
  </section>

  <script src="./index.js"></script>
  <script>
    const firstParagraph = document.querySelector("p");
    console.log(firstParagraph.closest("section")); // <section class="innerSection">
  </script>
</body>
```

<hr>

## Select the HTML of an element

- `innerHTML` gets the HTML inside the element as a string. Only valid for element nodes.
- `outerHTML` gets the same as `innerHTML` plus the element itself.

```html
<body>
  <section class="outerSection">
    <section>
      <h2>Paragraph Heading</h2>
    </section>
    <section class="innerSection">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
    </section>
  </section>

  <script src="./index.js"></script>
  <script>
    const firstParagraph = document.querySelector("p");
    console.log(firstParagraph.innerHTML); // Paragraph 1
    console.log(firstParagraph.outerHTML); // <p>Paragraph 1</p>

    const innerSection = document.querySelector(".innerSection");
    console.log(innerSection.innerHTML);
    /* 
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <p>Paragraph 3</p>
    */

    console.log(innerSection.outerHTML);
    /* 
    <section class="innerSection">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
    </section>
    */
  </script>
</body>
```

<hr>

## Select the text of an element

`textContent` accesses the text inside an element: only text, minus all tags.

```html
<body>
  <h1 id="headingId">Heading</h1>

  <section class="outerSection">
    <section>
      <h2>Paragraph Heading</h2>
    </section>
    <section class="innerSection">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
    </section>
  </section>

  <script src="./index.js"></script>
  <script>
    const firstParagraph = document.querySelector("p");
    console.log(firstParagraph.textContent); // Paragraph 1

    const innerSection = document.querySelector(".innerSection");
    console.log(innerSection.textContent);
    /* 
    Paragraph 1
    Paragraph 2
    Paragraph 3
    */
  </script>
</body>
```

<hr>

## Retrieving the name of an HTML tag or node

`tagName` and `nodeName` gets the name of a tag and the name of a node, respectively.

```html
<body>
  <h1 id="headingId">Heading</h1>

  <section class="outerSection">
    <section>
      <h2>Paragraph Heading</h2>
    </section>
    <section class="innerSection">
      <p>Paragraph 1</p>
      <p>Paragraph 2</p>
      <p>Paragraph 3</p>
    </section>
  </section>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes[0]); // #text "\n\n  "
    console.log(document.body.childNodes[0].tagName); // undefined
    console.log(document.body.childNodes[0].nodeName); // #text

    const firstParagraph = document.querySelector("p");
    console.log(firstParagraph.tagName); // P
    console.log(firstParagraph.nodeName); // P

    const innerSection = document.querySelector(".innerSection");
    console.log(innerSection.tagName); // SECTION
    console.log(innerSection.nodeName); // SECTION
  </script>
</body>
```

<hr>

## Hiding an HTML element

We can hide an element using `<node>.hidden = true`. It is the same as `display: none;` in CSS. However, if we hide an element using CSS code - `display: none;` -, instead of hiding it with the JavaScript code, the `hidden` attribute will still show `false`.

```html
<body>
  <h1 id="headingId">Heading</h1>
  <h1 id="headingId2">Heading 2</h1>

  <script src="./index.js"></script>
  <script>
    const heading1 = document.querySelector("#headingId");
    heading1.hidden = true;

    const heading2 = document.querySelector("#headingId2");

    console.log(heading1.hidden); // true
    console.log(heading2.hidden); // false
  </script>
</body>
```

<hr>

## Input properties

The `<input>` tag has its own specific properties as well.

- `<inputElement>.type`
- `<inputElement>.id`
- `<inputElement>.value`
- `<inputElement>.checked`. This one is boolean.

```html
<body>
  <form action="">
    <label for="username">Username</label>
    <input type="text" id="username" />

    <br />
    <br />

    <p>Agree ?</p>
    <label for="yes">Yes</label>
    <input type="radio" id="yes" checked value="yes" />
    <label for="no">No</label>
    <input type="radio" id="no" value="no" />
  </form>

  <script src="./index.js"></script>
  <script>
    const inputUsername = document.querySelector("input#username");
    console.log(inputUsername); // <input id="username" type="text">
    console.log(inputUsername.type); // text
    console.log(inputUsername.id); // username
    console.log(inputUsername.value); // <empty string>

    const inputYes = document.querySelector("input#yes");
    const inputNo = document.querySelector("input#no");
    console.log(inputYes.checked); // true
    console.log(inputYes.value); // yes
    console.log(inputNo.checked); // false
    console.log(inputNo.value); // no
  </script>
</body>
```

<hr>

## Anchor element's `href` property

To get the link of an anchor tag, we can use `<anchorElement>.href`.

```html
<body>
  <a href="https://example.com" target="_blank">Example</a>
  <a href="https://test.com" target="_blank">Test</a>

  <script src="./index.js"></script>
  <script>
    const anchorTags = document.querySelectorAll("a");
    anchorTags.forEach((item) => {
      console.log(item.href);
      /* 
      https://example.com/
      https://test.com/
      */
    });
  </script>
</body>
```

<hr>

## Working with HTML tag attributes

There are several DOM properties that let us work with the attributes of tags.

- `<element>.hasAttribute(<attribute>)` checks for existence of the attribute.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");

    console.log(imgElem.hasAttribute("src")); // true
    console.log(imgElem.hasAttribute("width")); // false
  </script>
</body>
```

- `<element>.getAttribute(<attribute>)` gets the value of the attribute.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    console.log(imgElem.getAttribute("src")); // ./inexistent.img
  </script>
</body>
```

- `<element>.setAttribute(<attribute>, 'value')` sets the value of the attribute.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    console.log(imgElem.getAttribute("alt")); // This image doesn't exist

    imgElem.setAttribute("alt", "Inexistent image");
    console.log(imgElem.getAttribute("alt")); // Inexistent image
  </script>
</body>
```

- `<element>.removeAttribute(<attribute>)` removes the attribute.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    console.log(imgElem.hasAttribute("style")); // true

    imgElem.removeAttribute("style");
    console.log(imgElem.hasAttribute("style")); // false
  </script>
</body>
```

- `<element>.attributes` returns a `NamedNodeMap` object, which is a collection of attribute objects. `setAttribute` and `getAttribute` might be enough to access and manipulate the attributes of an element. However, `NamedNodeMap` object also provides various ways that could let us retrieve and manipulate the attributes of an element.

For example, we can use an array and object syntax to access the attribute objects within the `NamedNodeMap` returned by `<element>.attributes`.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    console.log(imgNamedNodeMap);
    // NamedNodeMap(3) [ src="./inexistent.img", alt="This image doesn't exist", style="border: 1px solid red;" ]

    console.log(imgNamedNodeMap[0]); // src="./inexistent.img"
    console.log(imgNamedNodeMap[0]["value"]); // ./inexistent.img

    console.log(imgNamedNodeMap["src"]); // src="./inexistent.img"
    console.log(imgNamedNodeMap["src"]["value"]); // ./inexistent.img

    console.log(imgNamedNodeMap.src); // src="./inexistent.img"
    console.log(imgNamedNodeMap.src.value); // ./inexistent.img
  </script>
</body>
```

The `NamedNodeMap` also has the `getNamedItem` method that helps to retrieve the attribute of an element:

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    console.log(imgNamedNodeMap.getNamedItem("src")); // src="./inexistent.img"
  </script>
</body>
```

Another method, that we can use to retrieve the attribute of an element, from the `NamedNodeMap` is the `item` method:

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    console.log(imgNamedNodeMap.item(0)); // src="./inexistent.img"
    console.log(imgNamedNodeMap.item("src")); // src="./inexistent.img"
  </script>
</body>
```

To set an attribute, we can use the `setNamedItem` metod from `NamedNodeMap`. This method accepts an attribute object, so if we want to use this method, we might need to use the `Document.createAttribute` method as well.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    const createdAltAttr = document.createAttribute("alt");
    createdAltAttr.value = "Inexistent image";

    console.log(imgNamedNodeMap.getNamedItem("alt")); // alt="This image doesn't exist"

    imgNamedNodeMap.setNamedItem(createdAltAttr);
    console.log(imgNamedNodeMap.getNamedItem("alt")); // "Inexistent image"
  </script>
</body>
```

We can also use the `value` property of the attribute object to set or change it's value:

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    imgNamedNodeMap.getNamedItem("alt").value = "Inexistent image";
    console.log(imgNamedNodeMap.getNamedItem("alt")); // "Inexistent image"
  </script>
</body>
```

To remove an attribute, we can use the `removeNamedItem` from the `NamedNodeMap`.

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");
    const imgNamedNodeMap = imgElem.attributes;

    console.log(imgNamedNodeMap.getNamedItem("alt")); // alt="This image doesn't exist"

    imgNamedNodeMap.removeNamedItem("alt");
    console.log(imgNamedNodeMap.getNamedItem("alt")); // null
  </script>
</body>
```

<hr>

## The `style` object

`style` is both an attribute and an object. So, it can be accessed using both:

- `<element>.getAttribute('style')`
- `<element>.style`

```html
<body>
  <img
    src="./inexistent.img"
    alt="This image doesn't exist"
    style="border: 1px solid red;"
  />

  <script src="./index.js"></script>
  <script>
    const imgElem = document.querySelector("img");

    console.log(imgElem.getAttribute("style")); // border: 1px solid red;
    console.log(imgElem.style); // CSSStyleDeclaration...
  </script>
</body>
```

Here is how to add and remove a styling of an element using the `style` property:

```html
<body>
  <p style="text-align: center;">This is a text</p>

  <script src="./index.js"></script>
  <script>
    const paragraphElem = document.querySelector("p");
    paragraphElem.style.backgroundColor = "lightblue";
    paragraphElem.style.border = "1px solid red";

    paragraphElem.style.removeProperty("border");
  </script>
</body>
```

We can also style an element using `<element>.style.cssText`. This one removes all the existing styles of an element:

```html
<body>
  <p style="text-align: center;">This is a text</p>

  <script src="./index.js"></script>
  <script>
    const paragraphElem = document.querySelector("p");
    paragraphElem.style.cssText = `background-color: lightgreen;
      border: 1px solid red;`;
  </script>
</body>
```

## Retrieving the style information of an element

To retrieve the style of an element, we can use `getComputedStyle`. This global method is read-only, and we cannot set the style of an element using it:

```html
<body>
  <p style="text-align: center;">This is a text</p>

  <script src="./index.js"></script>
  <script>
    const paragraphElem = document.querySelector("p");

    console.log(getComputedStyle(paragraphElem)); // CSSStyleDeclaration
    console.log(getComputedStyle(paragraphElem).textAlign); // center
    console.log(getComputedStyle(paragraphElem).marginTop); // not margin, but marginTop/Left etc. should be used

    // This causes an error
    // getComputedStyle(paragraphElem).textAlign = "right"
  </script>
</body>
```

<hr>

## Working with Attributes starting with `data-`

`data-*` attributes allow us to store extra information on standard, semantic HTML elements without other hacks such as non-standard attributes, or extra properties on DOM. Attributes starting with “`data-*`” are available in the `dataset` property.

```html
<body>
  <p style="text-align: center;" data-about-something="something">
    This is a text
  </p>

  <script src="./index.js"></script>
  <script>
    const paragraphElem = document.querySelector("p");

    console.log(paragraphElem.dataset.aboutSomething); // something

    paragraphElem.dataset.firstParagraph = true;
    if (paragraphElem.dataset.firstParagraph)
      paragraphElem.textContent = "This is the first paragraph.";
  </script>
</body>
```

<hr>

## Creating an HTML element

To create an element, we use `document.createElement("<element>")`.

```html
<body>
  <script src="./index.js"></script>
  <script>
    // This element has been created but not yet added to the webpage
    const newParagraphElem = document.createElement("p");

    console.log(newParagraphElem); // <p>
  </script>
</body>
```

## Creating a text node

To create a text node, we use `document.createTextNode("<text>");`

```html
<body>
  <script src="./index.js"></script>
  <script>
    const newTextNode = document.createTextNode(
      "This is a text node, which is not yet added to the webpage",
    );
    console.log(newTextNode); // #text "This is a text node, which is not yet added to the webpage"
  </script>
</body>
```

<hr>

## Adding elements to the DOM

There are various methods to add elements and nodes to the DOM:

- `append()` appends nodes or strings at the end of a node.
- `prepend()` inserts nodes or strings at the beginning of a node.

```html
<body>
  <p style="text-align: center;" data-about-something="something">
    This is a text
  </p>

  <script src="./index.js"></script>
  <script>
    console.log(document.body.childNodes); // NodeList(6)...
    console.log(document.body.children); // HTMLCollection { ...length: 3 }

    const newTextNode = document.createTextNode(
      "This text node is added to the webpage with JS",
    );
    const newParagraphElem = document.createElement("p");
    newParagraphElem.textContent =
      "This element is added to the webpage with JS";

    document.body.append(newTextNode); // append at the end of node
    document.body.prepend(newParagraphElem); // prepend at the beginning of node

    console.log(document.body.childNodes); // NodeList(8)...
    console.log(document.body.children); // HTMLCollection { ...length: 4 }
  </script>
</body>
```

- `before()` inserts nodes or strings before a node.
- `after()` inserts nodes or strings after a node.

```html
<body>
  <p style="text-align: center;" data-about-something="something">
    This is a text
  </p>

  <script src="./index.js"></script>
  <script>
    const existingParagraphElem = document.querySelector("p");

    const newTextNode = document.createTextNode(
      "This text node is added to the webpage with JS",
    );
    const newParagraphElem = document.createElement("p");
    newParagraphElem.textContent =
      "This element is added to the webpage with JS";

    existingParagraphElem.before(newTextNode); // insert nodes or strings before a node
    existingParagraphElem.after(newParagraphElem); // insert nodes or strings after a node
  </script>
</body>
```

- `replaceWith()` replaces a node with the given nodes or strings.

```html
<body>
  <p style="text-align: center;" data-about-something="something">
    This is a text
  </p>

  <script src="./index.js"></script>
  <script>
    const existingParagraphElem = document.querySelector("p");

    const newParagraphElem = document.createElement("p");
    newParagraphElem.textContent =
      "This element is added to the webpage with JS";

    existingParagraphElem.replaceWith(newParagraphElem);
  </script>
</body>
```

<hr>

## Insert an HTML string with `<element>.insertAdjacentHTML(<where>, <html>)`

To insert an HTML string “as html”, with all tags and stuff working, we can use `<element>.insertAdjacentHTML(<where>, <html>)`

- `<element>.insertAdjacentHTML('beforebegin', '<HTMLCode>');` - insert html immediately before the `<element>`.

```html
<body>
  <div>
    <p style="text-align: center;">This is a text</p>
  </div>

  <script src="./index.js"></script>
  <script>
    const divElement = document.querySelector("div");
    divElement.insertAdjacentHTML(
      "beforebegin",
      "<p>added before the DIV element</p>",
    );

    console.log(document.body.children); // HTMLCollection { 0: p, 1: div, ...length: 4 }
  </script>
</body>
```

- `<element>.insertAdjacentHTML('afterbegin', '<HTMLCode>');` - insert html into the `<element>`, at the beginning.

```html
<body>
  <div>
    <p style="text-align: center;">This is a text</p>
  </div>

  <script src="./index.js"></script>
  <script>
    const divElement = document.querySelector("div");
    divElement.insertAdjacentHTML(
      "afterbegin",
      "<p>added into the beginning of the DIV element</p>",
    );

    console.log(document.body.children); // HTMLCollection { 0: div, ...length: 3 }
  </script>
</body>
```

- `<element>.insertAdjacentHTML('beforeend', '<HTMLCode>');` - insert html into the `<element>`, at the end.

```html
<body>
  <div>
    <p style="text-align: center;">This is a text</p>
  </div>

  <script src="./index.js"></script>
  <script>
    const divElement = document.querySelector("div");
    divElement.insertAdjacentHTML(
      "beforeend",
      "<p>added into the end of the DIV element</p>",
    );

    console.log(document.body.children); // HTMLCollection { 0: div, ...length: 3 }
  </script>
</body>
```

- `<element>.insertAdjacentHTML('afterend', '<HTMLCode>');` - insert html immediately after the `<element>`.

```html
<body>
  <div>
    <p style="text-align: center;">This is a text</p>
  </div>

  <script src="./index.js"></script>
  <script>
    const divElement = document.querySelector("div");
    divElement.insertAdjacentHTML(
      "afterend",
      "<p>added after the DIV element</p>",
    );

    console.log(document.body.children); // HTMLCollection { 0: div, 1: p, ...length: 4 }
  </script>
</body>
```

## Insert Text with `<element>.insertAdjacentText(<where>, <text>)`

`<element>.insertAdjacentText(<where>, <text>)` has the same syntax as above but inserts text.

<hr>

## Remove a node from the DOM

To remove the node from a DOM, we can use the `remove()` method:

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const firstParagraph = document.querySelector("p");

    firstParagraph.remove();
  </script>
</body>
```

<hr>

## Copy a node

We can copy a node using the `cloneNode()` method:

- `<element>.cloneNode(true);` - the node, its attributes, and its whole subtree, including text that may be in child text nodes, is also copied.
- `<element>.cloneNode(false);` - only the node with all attributes is copied. The subtree, including any text that the node contains, is not cloned.

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");

    const newElem = sectionElem.cloneNode(true);
    document.body.append(newElem);
  </script>
</body>
```

<hr>

## Dealing with HTML Classes

There are various properties and methods to work with HTML classes:

- `<element>.className;` - access the class of an HTML element. The assignment to className, using this method, replaces the whole string of classes.
- `<element>.classList.contains("<className>");` - checks for the given class, returns `true` or `false`.

```html
<body>
  <section>
    <p class="blueBackground centerAligned">Paragraph 1</p>
    <p class="blueBackground centerAligned">Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const firstParagraph = document.querySelector("p");

    console.log(firstParagraph.className); // blueBackground centerAligned
    firstParagraph.className = "greenBackground";
    console.log(firstParagraph.className); // greenBackground

    console.log(firstParagraph.classList.contains("blueBackground")); // false
    console.log(firstParagraph.classList.contains("greenBackground")); // true
  </script>
</body>
```

- `<element>.classList.add("<className>");` - adds given classes to an HTML element.
- `<element>.classList.remove("<className>");` - removes given classes from an HTML element.

```html
<body>
  <section>
    <p class="blueBackground centerAligned">Paragraph 1</p>
    <p class="blueBackground centerAligned">Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const firstParagraph = document.querySelector("p");

    firstParagraph.classList.remove("centerAligned", "blueBackground");

    setTimeout(() => {
      firstParagraph.classList.add("centerAligned", "greenBackground");
    }, 1000);
  </script>
</body>
```

- `<element>.classList.toggle("<className>", <Boolean>);` adds the given class, if not present, to an HTML element. Also, removes the given class, if present, from an HTML element.
  - If the `<Boolean>` is `true`, then the class will only be added, but not removed.
  - If the `<Boolean>` is `false`, then the class will only be removed, but not added.

```html
<body>
  <section>
    <p class="blueBackground centerAligned">Paragraph 1</p>
    <p class="blueBackground centerAligned">Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const firstParagraph = document.querySelector("p");

    count = 0;
    const timerId = setInterval(() => {
      firstParagraph.classList.toggle("centerAligned");
      count++;
      if (count === 3) {
        clearInterval(timerId);
      }
    }, 1000);
  </script>
</body>
```

<hr>

## Accessing the positioned ancestor of HTML element

`<element>.offsetParent` is a read-only property that returns the nearest ancestor that the browser uses for calculating coordinates during rendering. The nearest ancestor that is one of the following:

- **CSS-positioned** (If there is no positioned ancestor element, the `<body>` is returned),
- `<body>`,
- `<table>`,
- `<th>`,
- `<td>`

In some occasions `offsetParent` is `null`:

- For not shown elements (`display:none` or not in the document).
- For `<body>` and `<html>`.
- For elements with `position:fixed`.

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p style="display: none;">Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const firstParagraph = document.querySelector("p");

    console.log(firstParagraph.offsetParent); // <body>, because section is not positioned
    console.log(firstParagraph.nextElementSibling.offsetParent); // null, because `display: none;`

    sectionElem.style.position = "absolute";
    console.log(firstParagraph.offsetParent); // <section style="position: absolute;">
  </script>
</body>
```

## Retrieving the coordinates of an element relative to `<element>.offsetParent`

- `<element>.offsetLeft` read-only property returns the number of pixels that the upper left corner of the current element is offset within the `<element>.offsetParent`.
- `<element>.offsetTop` read-only property returns the distance from the outer border of the current element (including its margin) to the top padding edge of the `<element>.offsetParent`.

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p style="display: none;">Paragraph 2</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const firstParagraph = document.querySelector("p");

    sectionElem.style.position = "absolute";

    console.log(firstParagraph.offsetParent); // <section style="position: absolute;">
    console.log(firstParagraph.offsetLeft); // 0

    firstParagraph.style.marginLeft = "5px";
    firstParagraph.style.marginTop = "150px";
    console.log(firstParagraph.offsetLeft); // 5
    console.log(firstParagraph.offsetTop); // 150
  </script>
</body>
```

<hr>

## Retrieving the width and height of an element

To get the content width and height together with paddings, without the scrollbar, we can use `<element>.clientWidth`, and `<element>.clientHeight`, respectively.

To get the content width and height together with paddings including the scrolled out parts, and without the scrollbar, we can use `<element>.scrollWidth`, and `<element>.scrollHeight`, respectively.

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <p>Paragraph 3</p>
    <p>Paragraph 4</p>
    <p>Paragraph 5</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");

    sectionElem.style.overflowY = "scroll";

    sectionElem.style.width = "100px";
    sectionElem.style.paddingLeft = "10px";
    sectionElem.style.height = "40px";
    sectionElem.style.paddingTop = "10px";

    console.log(sectionElem.clientWidth); // 110, width + padding
    console.log(sectionElem.scrollWidth); // 110, width + padding
    console.log(sectionElem.clientHeight); // 50, height + padding
    console.log(sectionElem.scrollHeight); // 196, visible height + scrolled-out height + padding

    sectionElem.style.width = "200px";
    sectionElem.style.height = "50px";

    console.log(sectionElem.clientWidth); // 210, width + padding
    console.log(sectionElem.scrollWidth); // 210, width + padding
    console.log(sectionElem.clientHeight); // 50, height + padding
    console.log(sectionElem.scrollHeight); // 196, visible height + scrolled-out height +
  </script>
</body>
```

## Deal with scrolling on a screen

- `<element>.scrollLeft` property gets or sets the number of pixels by which an element's content is scrolled from its left edge.
- `<element>.scrollTop` property gets or sets the number of pixels by which an element's content is scrolled from its top edge.

```html
<body>
  <section>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <p>Paragraph 3</p>
    <p>Paragraph 4</p>
    <p>Paragraph 5</p>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");

    sectionElem.style.overflowY = "scroll";

    sectionElem.style.height = "40px";
    sectionElem.style.paddingTop = "10px";

    sectionElem.scrollTop = "40";

    console.log(sectionElem.scrollTop); // 40
    console.log(sectionElem.scrollLeft); // 0
  </script>
</body>
```

- The read-only `window.scrollY` property returns the number of pixels by which the document is currently scrolled vertically.
- Likewise, the `window.scrollX` property returns the number of pixels by which the document is scrolled horizontally.

These properties are read-only. To scroll the window to a particular place, use `Window.scroll()`. It also accepts an object, which we can use to set the coordinate and the scrolling behavior.

`window.scrollTo()` is the same as the above method.

```html
<body>
  <section>
    <div style="height: 200px; border: 1px solid red;">1</div>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const divElem = document.querySelector("div");

    for (let divCount = 0; divCount < 10; divCount++) {
      divClone = divElem.cloneNode(true);
      divClone.textContent = Number(divClone.textContent) + divCount + 1;
      document.body.append(divClone);
    }

    console.log(window.scrollY); // 0
    console.log(window.scrollX); // 0

    window.scroll({
      top: 200,
      left: 100,
      behavior: "smooth",
    });

    /* window.scrollTo({
        top:200,
        left: 100,
        behavior: "smooth"
    }) */

    console.log(window.scrollY); // 200
    console.log(window.scrollX); // 0
  </script>
</body>
```

`window.scrollBy(x,y)` scrolls the page relative to its current position.

```html
<body>
  <section>
    <button style="position: fixed;">Scroll a bit</button>
    <div style="height: 200px; border: 1px solid red;">1</div>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const divElem = document.querySelector("div");
    const button = document.querySelector("button");

    for (let divCount = 0; divCount < 10; divCount++) {
      divClone = divElem.cloneNode(true);
      divClone.textContent = Number(divClone.textContent) + divCount + 1;
      document.body.append(divClone);
    }

    button.addEventListener("click", () => {
      window.scrollBy(0, 100);

      /* window.scrollBy({
        top: 100,
        left: 0,
        behavior: "smooth",
      }); */
    });
  </script>
</body>
```

`<element>.scrollIntoView()` method scrolls the element's ancestor containers such that the element on which `scrollIntoView()` is called is visible to the user. We can use this method with arguments:

- If `true`, the top of the element will be aligned to the top of the visible area of the scrollable ancestor.
- If `false`, the bottom of the element will be aligned to the bottom of the visible area of the scrollable ancestor.
- It also accepts an optional object to have a better control on the method.

```html
<body>
  <section>
    <button id="top" style="position: fixed;">Scroll to align the top</button>
    <button id="bottom" style="position: fixed; top: 40px;">
      Scroll to align the bottom
    </button>
    <div style="height: 200px; border: 1px solid red;">1</div>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const divElem = document.querySelector("div");
    const buttonToTop = document.querySelector("#top");
    const buttonToBottom = document.querySelector("#bottom");

    for (let divCount = 0; divCount < 10; divCount++) {
      divClone = divElem.cloneNode(true);
      divClone.textContent = Number(divClone.textContent) + divCount + 1;
      divClone.id = "div" + divClone.textContent;
      document.body.append(divClone);
    }

    div8 = document.querySelector("#div8");

    buttonToTop.addEventListener("click", () => {
      div8.scrollIntoView();
    });

    buttonToBottom.addEventListener("click", () => {
      div8.scrollIntoView(false);
    });
  </script>
</body>
```

## Retrieve the element size and coordinates with `getBoundingClientRect`

`<element>.getBoundingClientRect()` method returns a `DOMRect` object providing information about the size of an element and its position relative to the viewport. The `left`, `top`, `right`, `bottom`, `x`, `y`, `width`, and `height` properties describe the position and size of the overall rectangle in pixels. Properties other than width and height are relative to the top-left of the viewport. The `width` and `height` properties of the `DOMRect` object returned by the method include the padding and border-width, not only the content width/height.

```html
<body>
  <section>
    <div style="height: 200px; border: 1px solid red;">1</div>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const divElem = document.querySelector("div");

    console.log(divElem.getBoundingClientRect());
    // DOMRect { x: 8, y: 8, width: 700, height: 202, top: 8, right: 708, bottom: 210, left: 8 }
  </script>
</body>
```

## Retrieving the element coordinates with `elementFromPoint`

`document.elementFromPoint(x, y)` returns the most nested element at window coordinates (x, y).

```html
<body>
  <section>
    <div id="outer" style="height: 200px; border: 1px solid red;">
      Outer
      <div id="inner" style="border: 1px solid blue; height: 100px;">Inner</div>
    </div>
  </section>

  <script src="./index.js"></script>
  <script>
    const sectionElem = document.querySelector("section");
    const outerDiv = document.querySelector("#outer");
    const innerDiv = document.querySelector("#inner");

    innerDiv.onclick = getCoord;

    function getCoord(event) {
      elemHorizontal = this.getBoundingClientRect().x;
      elemVertical = this.getBoundingClientRect().y;
      console.log(document.elementFromPoint(elemHorizontal, elemVertical));
    }
  </script>
</body>
```

<hr>
<hr>

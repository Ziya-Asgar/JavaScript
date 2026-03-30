# JavaScript Cheatsheet

<hr>

- [JavaScript Cheatsheet](#javascript-cheatsheet)
  - [Useful Links](#useful-links)
  - [`use strict`](#use-strict)
  - [String Methods](#string-methods)
  - [Number Methods](#number-methods)
  - [Math Object](#math-object)
  - [Type Conversion](#type-conversion)
    - [`String()`](#string)
    - [`Number()`](#number)
      - [`+` operator](#-operator)
    - [`Boolean()`](#boolean)
  - [Conditionals](#conditionals)
    - [`if()` on a single line](#if-on-a-single-line)
    - [`if()...else`](#ifelse)
    - [`if()...else if()...else`](#ifelse-ifelse)
    - [Ternary conditions](#ternary-conditions)
    - [`switch`](#switch)
  - [Loops](#loops)
  - [Functions](#functions)
  - [Objects](#objects)
  - [Symbols](#symbols)
  - [Arrays](#arrays)
  - [Maps](#maps)
  - [WeakMaps](#weakmaps)
  - [Sets](#sets)
  - [WeakSets](#weaksets)
  - [Destructuring](#destructuring)
  - [Date Object](#date-object)
  - [JSON](#json)
  - [Classes](#classes)
  - [Error Handling](#error-handling)
  - [Promises, async/await](#promises-asyncawait)
  - [Generators](#generators)
  - [Modules](#modules)
  - [DOM](#dom)
  - [DOM Events](#dom-events)
  - [Forms](#forms)
    - [`document.forms`](#documentforms)
    - [`form.elements`](#formelements)
    - [`<fieldset>`](#fieldset)
    - [`<element>.form`](#elementform)
    - [`<select>` element](#select-element)
      - [`<option>`](#option)
    - [submit a form to a server manually](#submit-a-form-to-a-server-manually)
  - [Window object](#window-object)
    - [`window.caches`](#windowcaches)
      - [Create a new cache with `window.caches.open`](#create-a-new-cache-with-windowcachesopen)
      - [Add to cache with the `add()` method from a `Cache` instance](#add-to-cache-with-the-add-method-from-a-cache-instance)
      - [Add to cache with the `addAll()` method from a `Cache` instance](#add-to-cache-with-the-addall-method-from-a-cache-instance)
      - [Change and override cache with the `put()` method from a `Cache` instance](#change-and-override-cache-with-the-put-method-from-a-cache-instance)
      - [Retrieve an item in cache using `match()` method from `Cache` and `CacheStorage`](#retrieve-an-item-in-cache-using-match-method-from-cache-and-cachestorage)
      - [Retrieve all items in cache using `matchAll()` method from `Cache` and `CacheStorage`](#retrieve-all-items-in-cache-using-matchall-method-from-cache-and-cachestorage)
      - [Iterate through cache items using `keys()` method from `Cache` and `CacheStorage`](#iterate-through-cache-items-using-keys-method-from-cache-and-cachestorage)
      - [Delete an item from cache using `delete()` method from `Cache`](#delete-an-item-from-cache-using-delete-method-from-cache)
      - [Remove a cache with `window.caches.delete()`](#remove-a-cache-with-windowcachesdelete)
      - [Find a cache with `window.caches.has()`](#find-a-cache-with-windowcacheshas)
    - [`window.clientInformation` or `window.navigator`](#windowclientinformation-or-windownavigator)
      - [`navigator.clipboard`](#navigatorclipboard)
    - [`window.history`](#windowhistory)
      - [Moving back and forward in the browsing history](#moving-back-and-forward-in-the-browsing-history)
      - [Number of pages in the browsing history](#number-of-pages-in-the-browsing-history)
      - [`history.pushState()` and `history.replaceState()`](#historypushstate-and-historyreplacestate)
    - [`window.innerHeight` and `window.innerWidth`](#windowinnerheight-and-windowinnerwidth)
    - [`window.location`](#windowlocation)
      - [Location properties to retrieve URL parts](#location-properties-to-retrieve-url-parts)
      - [`location.assign()`](#locationassign)
      - [`location.replace()`](#locationreplace)
      - [`location.reload()`](#locationreload)
    - [`window.open()` and `close`](#windowopen-and-close)
    - [`window.confirm()`](#windowconfirm)
    - [`window.getSelection()`](#windowgetselection)
      - [Range](#range)
      - [Selection](#selection)
      - [Selection in forms](#selection-in-forms)
  - [Fetch](#fetch)
    - [GET request](#get-request)
    - [POST request](#post-request)
    - [Fetch and HTTP status codes](#fetch-and-http-status-codes)
    - [Headers](#headers)
    - [Cancel a fetch request](#cancel-a-fetch-request)
  - [Regular Expressions](#regular-expressions)
    - [Creating Regular Expressions](#creating-regular-expressions)
    - [Flags](#flags)
    - [Regular Expression methods](#regular-expression-methods)
      - [`.match()`](#match)
      - [`.replace()`](#replace)
      - [`.replaceAll()`](#replaceall)
      - [`<regexp>.test()`](#regexptest)
    - [Character classes](#character-classes)
      - [Inverse classes](#inverse-classes)
    - [Using dot `.`](#using-dot-)
    - [Unicode encoding and `u` flag](#unicode-encoding-and-u-flag)
    - [Anchors: string start `^` and end `$`](#anchors-string-start--and-end-)
      - [Multiline mode of anchors `^`, `$` and the flag `m`](#multiline-mode-of-anchors---and-the-flag-m)
    - [Word boundary: `\b`](#word-boundary-b)
    - [Escaping Special characters](#escaping-special-characters)
    - [Sets and ranges](#sets-and-ranges)
    - [Quantifiers `+`, `\*`, `?` and `{<number>}`](#quantifiers----and-number)
    - [Greedy and lazy quantifiers](#greedy-and-lazy-quantifiers)
    - [Capturing groups](#capturing-groups)
    - [Backreferences in pattern: `\N` and `\k<name>`](#backreferences-in-pattern-n-and-kname)
    - [Alternation (OR) `|`](#alternation-or-)
    - [Lookahead and lookbehind](#lookahead-and-lookbehind)
    - [Catastrophic backtracking](#catastrophic-backtracking)
    - [Sticky flag `y`, searching at position](#sticky-flag-y-searching-at-position)
    - [Methods of RegExp and String](#methods-of-regexp-and-string)
    - [Summary of Regular Expressions](#summary-of-regular-expressions)
  - [URL](#url)
    - [Creating a `URL` object](#creating-a-url-object)
    - [Properties of a `URL` object](#properties-of-a-url-object)
    - [`URLSearchParams`](#urlsearchparams)
    - [Functions for encoding and decoding url and url components](#functions-for-encoding-and-decoding-url-and-url-components)
    - [`createObjectURL()` and `revokeObjectURL()`](#createobjecturl-and-revokeobjecturl)
  - [Binary files](#binary-files)
    - [`ArrayBuffer`](#arraybuffer)
      - [Typed Arrays](#typed-arrays)
      - [Typed Array Methods](#typed-array-methods)
      - [`DataView`](#dataview)
    - [`TextDecoder` and `TextEncoder`](#textdecoder-and-textencoder)
      - [`TextDecoder`](#textdecoder)
      - [`TextEncoder`](#textencoder)
    - [Blob](#blob)
      - [Downloading Blobs](#downloading-blobs)
    - [File and FileReader](#file-and-filereader)
      - [`File`](#file)
      - [`FileReader`](#filereader)
    - [Summary of Binary Files](#summary-of-binary-files)

<hr>
<hr>

## Useful Links

- https://javascript.info
- https://developer.mozilla.org
- https://www.smashingmagazine.com/2012/06/all-about-unicode-utf8-character-sets/
- https://blog.hubspot.com/website/what-is-utf-8

<hr>
<hr>

## `use strict`

Strict mode makes several changes to normal JavaScript semantics:

- Eliminates some JavaScript silent errors by changing them to throw errors.
- Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
- Prohibits some syntax likely to be defined in future versions of ECMAScript.

To invoke strict mode for an entire script, put the exact statement `"use strict"` before any other statements.

```js
"use strict";
```

<hr>
<hr>

## String Methods

[String Methods](./JS_StringMethods.md)

<hr>
<hr>

## Number Methods

[Number Methods](./JS_NumberMethods.md)

<hr>
<hr>

## Math Object

[Math Object](./JS_MathObject.md)

<hr>
<hr>

## Type Conversion

### `String()`

`String()` turns the provided argument into a string:

```js
typeof String(10); // string
```

### `Number()`

`Number()` turns the provided argument into a number:

```js
typeof Number("10"); // number
```

#### `+` operator

As well as adding numbers, `+` operator, can be used to convert a variable to a number:

```js
typeof +"10"; // number
```

### `Boolean()`

`Boolean()` turns the provided argument to either `true` or `false`:

```js
Boolean(" "); // true
Boolean(""); // false
```

<hr>
<hr>

## Conditionals

### `if()` on a single line

We can write an `if()` statement on a single line like this:

```js
const condition1 = true,
  condition2 = true;

if (condition1 === condition2) console.log(`It worked`); // It worked
```

### `if()...else`

An example for an `if()...else` statement:

```js
const condition1 = true,
  condition2 = false;

if (condition1 === condition2) {
  console.log(`${condition1} and ${condition2} are equal`);
} else {
  console.log(`some default result`);
}
```

### `if()...else if()...else`

An example for `if()...else if()...else` statement:

```js
const condition1 = true,
  condition2 = false;

if (condition1 === condition2) {
  console.log(`${condition1} and ${condition2} are equal`);
} else if (condition1 < condition2) {
  console.log(`${condition1} is less than ${condition2}`);
} else {
  console.log(`some default result`);
}
```

<hr>

### Ternary conditions

We can set ternary conditions like this:

```js
const condition1 = true,
  condition2 = false;

const resultOfConditions =
  condition1 === condition2
    ? `Equal`
    : condition1 < condition2
      ? `Less`
      : condition1 > condition2
        ? `More`
        : `None is true`;

console.log(resultOfConditions); // More
```

<hr>

### `switch`

Another conditional statement is `switch`. `switch` statement needs a strict match, meaning the same data type:

```js
const condition1 = true;

switch (condition1) {
  case 0:
    console.log(0);
    break;
  case 1:
  case 2:
    console.log(`1 or 2`);
    break;
  case 3:
    console.log(3);
    break;
  default:
    console.log(`Default result`);
}
```

<hr>
<hr>

## Loops

[Loops](./JS_Loops.md)

<hr>
<hr>

## Functions

[Functions](./JS_Functions.md)

<hr>
<hr>

## Objects

[Objects](./JS_Objects.md)

<hr>
<hr>

## Symbols

[Symbols](./JS_Symbols.md)

<hr>
<hr>

## Arrays

[Arrays](./JS_Arrays.md)

<hr>
<hr>

## Maps

[Maps](./JS_Maps.md)

<hr>
<hr>

## WeakMaps

[WeakMaps](./JS_WeakMaps.md)

<hr>
<hr>

## Sets

[Sets](./JS_Sets.md)

<hr>
<hr>

## WeakSets

[WeakSets](./JS_WeakSets.md)

<hr>
<hr>

## Destructuring

[Destructuring](./JS_Destructuring.md)

<hr>
<hr>

## Date Object

[Date Object](./JS_Date_Object.md)

<hr>
<hr>

## JSON

[JSON](./JS_JSON.md)

<hr>
<hr>

## Classes

[Classes](./JS_Classes.md)

<hr>
<hr>

## Error Handling

[Error Handling](./JS_ErrorHandling.md)

<hr>
<hr>

## Promises, async/await

[Promises](./JS_Promises.md)

<hr>
<hr>

## Generators

[Generators](./JS_Generators.md)

<hr>
<hr>

## Modules

[Modules](./JS_Modules.md)

<hr>
<hr>

## DOM

[DOM](./JS_DOM.md)

<hr>
<hr>

## DOM Events

[Dom Events](./JS_DomEvents.md)

<hr>
<hr>

## Forms

### `document.forms`

`document.forms` is a named and ordered collection that lets us access the `<form>` element:

```html
<form name="formName">
  <input name="one" value="1" />
  <input name="two" value="2" />
</form>

<script src="./index.js"></script>
<script>
  // the form with name="formName"
  console.log(document.forms.formName);

  // the first form in the document
  console.log(document.forms[0]);
</script>
```

<hr>

### `form.elements`

There is `form.elements` which helps us access any form element:

```html
<form name="formName">
  <input name="one" value="1" />
  <input name="two" value="2" />
</form>

<script src="./index.js"></script>
<script>
  console.log(document.forms.formName.elements);
  console.log(document.forms.formName.elements["one"]);
</script>
```

<hr>

When there are multiple elements with the same name, then `<form>.elements["<nameOfTheFormElement>"]` is a collection as well. In that case, we can access elements like this: `<form>.elements.<nameOfTheFormElement>[0]`.

<hr>

### `<fieldset>`

`<fieldset>` elements inside a form have their own `.elements` collection as well.

```js
<form>.elements.<someFieldsetName>.elements.<someNameInTheFieldset>;
<form>.elements.<someFieldsetName>.elements[0];
```

<hr>

### `<element>.form`

If we access an element in the form, we can get the form through the element. For any element, the form is available as `<element>.form`.

Here are some ways to manipulate form elements:

```js
document.forms[0].elements.input.value = "New value";
document.forms[0].elements.textarea.value = "New text";
document.forms[0].elements.input.checked = true; // for a checkbox or radio button
```

<hr>

### `<select>` element

A `<select>` element has 3 important properties:

- `select.options` - the collection of `<option>` subelements,
- `select.value` - the value of the currently selected `<option>`,
- `select.selectedIndex` - the number of the currently selected `<option>`.

#### `<option>`

Option elements have their own properties:

- `option.selected` - Is the option selected.
- `option.index` - The number of the option among the others in its `<select>`.
- `option.text` - Text content of the option (seen by the visitor).

Here is how to manipulate the `<option>` element within the `<select>`:

```js
select.options[0].selected = true;
select.value = "some value for first option that to be selected";
```

```js
select.selectedIndex = 0;
select.value = "some value for first option that to be selected";
```

Here is a syntax to create a new `<option>`: `new Option(textInsideTheOption, optionValue, defaultSelected, selected)`

- `defaultSelected` – if `true`, then selected HTML-attribute is created,
- `selected` – if `true`, then the option is selected.

```js
const option1 = new Option("Text", "value");
const option2 = new Option("Text", "value", true, true);
```

<hr>

### submit a form to a server manually

To submit a form to the server manually, we can call `<form>.submit()`

<hr>
<hr>

## Window object

A global variable, `window`, represents the window in which the script is running. In a tabbed browser, each tab is represented by its own `Window` object. This object contains many properties and methods that we can use. We don't need to access all of them by prepending `window.`. For example, `document` is part of the `Window` object, and we can access it either using `window.document` or simply `document`.

For a full list of the window properties, go to [MDN Window](https://developer.mozilla.org/en-US/docs/Web/API/Window).

Let's review some properties and methods of this rich object.

### `window.caches`

`window.caches` is a read-only property that returns the `CacheStorage` object. This object enables functionality such as storing assets for offline use, and generating custom responses to requests.

Because older browsers may not support the functionality of `caches`, it is good practice to check for its availability before attempting to reference it. The `caches` property is available on the `window` object and we can check that it is implemented in the browser with this snippet:

```js
if ("caches" in window) {
  // your code
}
```

#### Create a new cache with `window.caches.open`

Use `window.caches.open(<name_of_cache>)` to obtain a `Cache` instance. The `Cache` interface provides methods for a persistent storage mechanism for `Request` / `Response` object pairs that are cached in long lived memory.

The `caches.open()` method first checks if a cache with the provided name already exists. If it doesn’t, it creates it and returns a `Promise` that resolves with the `Cache` object.

```js
const newCache = window.caches.open("new-cache").then((data) => {
  console.log(data);
}); // Cache {  }
```

The returned `Cache` itself has methods that we can use.

#### Add to cache with the `add()` method from a `Cache` instance

The `add()` method of the `Cache` interface takes a URL as an argument, makes a fetch request, and adds the resulting `Response` object to the given cache. If the response is already in the cache, the method does nothing.

The argument to the `add()` method can be a `Request` object or a URL string literal. `add()` will overwrite any key/value pair previously stored in the cache that matches the request.

```js
if ("caches" in window) {
  const cacheStuff = async () => {
    // this could also be a `new URL()` object
    const urlString = "./img1.jpg";

    await window.caches
      .open("img1")
      .then((cache) => {
        cache.add(urlString);
        console.log("Data was added to cache");
      })
      .catch((error) =>
        console.error("Error while adding data to cache:", error),
      );
  };

  cacheStuff();
}
```

We can gain more control by using a `Request` object:

```js
if ("caches" in window) {
  const cacheStuff = async () => {
    const urlString = "./img1.jpg";

    const options = {
      method: "GET",
      headers: new Headers({
        "Content-Type": "image/jpeg",
      }),
    };

    const req = new Request(urlString, options);

    await window.caches
      .open("img2")
      .then((cache) => {
        cache.add(req);
        console.log("Data was added to cache");
      })
      .catch((error) =>
        console.error("Error while adding data to cache:", error),
      );
  };

  cacheStuff();
}
```

#### Add to cache with the `addAll()` method from a `Cache` instance

The `addAll()` method of the `Cache` interface takes in an array of URL string literals or `Request` objects and returns a promise when all the resources have been cached. If any responses are already in the cache, the method skips them:

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  const urls = ["./file.json", "./file2.json"];

  newCache
    .addAll(urls)
    .then(() => console.log("Data added to cache."))
    .catch((error) => console.error("Error adding data to cache:", error));
};

cacheStuff();
```

#### Change and override cache with the `put()` method from a `Cache` instance

The `put()` method takes two parameters:

- a URL string literal or a `Request` object,
- a `Response` either from the network or generated within your code.

The `put()` method of the `Cache` interface makes a request and adds the response from that request to the cache. If the response is already in the cache, the method overwrites it.

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  newCache
    .put(
      "./file.json",
      new Response(
        '{"changedKey1": "changedValue1", "changedKey2": "changedValue2"}',
      ),
    )
    .then(() => console.log("Data added to cache."))
    .catch((error) => console.error("Error adding data to cache:", error));
};

cacheStuff();
```

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  newCache
    .put("./file2.json")
    .then(() => console.log("Data added to cache."))
    .catch((error) => console.error("Error adding data to cache:", error));
};

cacheStuff();
```

`Cache.add`/`Cache.addAll` do not cache responses with `Response.status` values that are not in the 200 range, whereas `Cache.put` lets you store any request/response pair.

#### Retrieve an item in cache using `match()` method from `Cache` and `CacheStorage`

The `match()` method finds the first matching request in the `Cache` object. It returns a `Promise` that resolves to the `Response` associated with the matching request. If no match is found, the `Promise` resolves to `undefined`.

The method could be accessed either through `CacheStorage` (`window.caches.match()`) or `Cache` instance.

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  const matchedCache = await newCache.match("./file2.json");

  console.log(matchedCache);
};

cacheStuff();
```

The browser uses different factors in determining if two or more Requests match. A `Request` may have the same URL as another but use a different HTTP method. Two such requests are considered to be different by the browser. When using the `match` method, we can also pass an options object as the second parameter. This object has key-value pairs that tell `match` to ignore specific factors when matching a request:

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  const options = {
    ignoreVary: true, // ignore differences in Headers
    ignoreMethod: true, // ignore differences in HTTP methods
    ignoreSearch: true, // ignore differences in query strings
  };

  const matchedCache = await newCache.match("./file2.json", options);

  console.log(matchedCache);
};

cacheStuff();
```

In a case where more than one cache item matches, the oldest one is returned.

#### Retrieve all items in cache using `matchAll()` method from `Cache` and `CacheStorage`

`matchAll()` method works the same as `match()` but retrieves all the matching items from cache. If no resources are found in the cache, the `matchAll()` method returns an empty array.

The method could be accessed either through `CacheStorage` (`window.caches.matchAll()`) or `Cache` instance.

#### Iterate through cache items using `keys()` method from `Cache` and `CacheStorage`

The `keys()` method returns a `Promise` that resolves to an array of `Request` objects representing the keys of the `Cache`. The requests are returned in the same order that they were inserted.

The method could be accessed either through `CacheStorage` (`window.caches.keys()`) or `Cache` instance.

```js
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  const cacheKeys = await newCache.keys();

  console.log(cacheKeys);
};

cacheStuff();
```

The `keys()` method also accepts an optional options object with properties such as `ignoreSearch`, `ignoreMethod`, and `ignoreVary`.

#### Delete an item from cache using `delete()` method from `Cache`

The `delete()` method finds the `Cache` entry whose key is the request, and if found, deletes the `Cache` entry and returns a `Promise` that resolves to `true`. If no `Cache` entry is found, it resolves to `false`. It accepts a URL string or a `Request` object as an argument.

```js
// delete a cache entry
const cacheStuff = async () => {
  const newCache = await window.caches.open("new-cache");

  newCache.delete("./file2.json");

  console.log(newCache);
};

cacheStuff();
```

The `delete()` method also accepts an optional options object with properties such as `ignoreSearch`, `ignoreMethod`, and `ignoreVary`.

#### Remove a cache with `window.caches.delete()`

We can also delete a cache by calling the `delete()` method on the `caches` property of the `window` object. This is different from the `delete()` method of the `Cache` instance. When a cache is deleted using `window.caches.delete()`, the method returns a `Promise` if the cache was actually deleted and a `false` if something went wrong or the cache doesn’t exist.

```js
// delete an existing cache
window.caches.delete("new-cache");
```

#### Find a cache with `window.caches.has()`

The `has(<cache_name>)` method of the `CacheStorage` interface returns a `Promise` that resolves to `true` if a `Cache` object matches the `<cache_name>`. It accepts a string representing the name of the `Cache` object you are looking for in the `CacheStorage`.

```js
window.caches.open("new-cache");

window.caches.has("new-cache").then((data) => console.log(data)); //true
```

<hr>

### `window.clientInformation` or `window.navigator`

`window.clientInformation` is an alias for `window.navigator`. The `Window.navigator` read-only property returns a reference to the `Navigator` object, which has methods and properties about the application running the script. The `Navigator` object represents the state and the identity of the user agent (browser). It has a lot of methods and properties. You can refer here for a thorough list: [MDN Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

#### `navigator.clipboard`

`navigator.clipboard` returns a `Clipboard` object that provides read and write access to the system clipboard. This is the entry point to the Clipboard API, which can be used to implement cut, copy, and paste features within a web application. To avoid potential issues, the Clipboard API can only be used on pages served over HTTPS (localhost is also permitted).

Because there are security risks of allowing a website to access user's clipboard, there are various errors that might happen while a developer is trying to work with the clipboard.

First of all, you can use the following code to check if the clipboard API is supported:

```js
if ("clipboard" in navigator) {
  console.log("Clipboard API is supported!");
} else {
  console.log("Clipboard API is not supported!");
}
```

`navigator.clipboard.writeText()`

To copy text to the clipboard call `writeText()`. The `writeText()` function returns a `Promise` that resolves or rejects depending on whether the passed text is copied successfully.

```js
navigator.clipboard
  .writeText("to be copied")
  .then(() => {
    console.log("Text copied to clipboard");
  })
  .catch((err) => {
    console.error("Failed to copy text: ", err);
  });
```

If you have error that says "Document is not focused", this might be because there is delay in writing to clipboard and user is not focusing on the window.

Another error that might occur is "Failed to copy text: DOMException: Clipboard write was blocked due to lack of user activation." To resolve this issue, you might need to call the `navigator.clipboard.writeText()` method within an event handler that is triggered by a user action.

So, you might try this:

```html
<button id="copyButton">Copy Text</button>

<script>
  const copyButton = document.getElementById("copyButton");

  copyButton.addEventListener("click", () => {
    navigator.clipboard
      .writeText("to be copied")
      .then(() => {
        console.log("Text copied to clipboard");
      })
      .catch((err) => {
        console.error("Failed to copy text: ", err);
      });
  });
</script>
```

`navigator.clipboard.readText()`

To read text from the clipboard, call `navigator.clipboard.readText()` and wait for the returned promise to resolve.

```html
<button id="readButton">Read the Copy</button>

<script>
  const readButton = document.getElementById("readButton");

  readButton.addEventListener("click", () => {
    navigator.clipboard
      .readText()
      .then((data) => {
        console.log(`Text from the clipboard is "${data}"`);
      })
      .catch((err) => {
        console.error(`Failed to read the text from clipboard: "${err}`);
      });
  });
</script>
```

<hr>

### `window.history`

The `window.history` read-only property returns a reference to the `History` object, which provides an interface for manipulating the browser session history (pages visited in the tab or frame that the current page is loaded in).

#### Moving back and forward in the browsing history

Moving backward and forward through the user's history is done using the `back()`, `forward()`, and `go()` methods.

```js
history.back(); // as if the user clicked on the Back button in their browser toolbar.
history.forward(); // as if the user clicked on the Forward button in their browser toolbar.
```

You can use the `go()` method to load a specific page from session history, identified by its relative position to the current page.

To move back one page:

```js
history.go(-1);
```

To move forward one page:

```js
history.go(1);
```

Another use for the `go()` method is to refresh the current page by either passing 0, or by invoking it without an argument:

```js
history.go(0);
history.go();
```

#### Number of pages in the browsing history

You can determine the number of pages in the history stack by looking at the value of the `history.length` property.

#### `history.pushState()` and `history.replaceState()`

`history.pushState(<state>, <title>, <URI/URL>)` will change the URL of the page and add the changed URL to the top of the URL stack of the history object.

- The `<state>` is any javascript data which will be stored in `history.state` variable, which will be available once you navigate through the page.

- The `<title>` on the code is just a text, which has no effect on any browser. You can skip that by passing an empty string `""` or some title text is fine.

- The `<URI/URL>` is a string which is the new URL to change.

If we are on "localhost:3000", and run the below code our directory will become "localhost:3000/newurl" (after 1 second) and the previous page in our history will be "localhost:3000".

```js
setTimeout(() => {
  history.pushState("temporary state data", "some title", "newurl"); // You can also provide a complete URL on the same domain

  console.log(history.state); // "temporary state data"
}, 1000);
```

Whenever users come back to the page which is added to history through `pushState` then an event with the name `popstate` will be triggered.

```js
window.addEventListener("popstate", (e) => {
  console.log("popstate");
});

setTimeout(() => {
  history.pushState("temporary state data", "some title", "newurl");

  console.log(history.state);
}, 1000);
// Whenever a user presses back `popstate` event will trigger
```

`history.replaceState()` only changes the URL . It doesn’t add URL to the history of URL the stack.

```js
setTimeout(() => {
  history.replaceState("temporary state data", "some title", "newurl");

  console.log(history.state);
}, 1000);
```

<hr>

### `window.innerHeight` and `window.innerWidth`

The read-only `innerHeight` property returns the interior height of the window in pixels, including the height of the horizontal scroll bar, if present.

The read-only `innerWidth` property returns the interior width of the window in pixels, including the width of the vertical scroll bar, if present.

```js
console.log(window.innerHeight);
console.log(window.innerWidth);
```

<hr>

### `window.location`

The `window.location` read-only property returns a `Location` object with information about the current location (URL) of the document.

#### Location properties to retrieve URL parts

Here are some properties in the `Location` object:

- `location.href`
- `location.hash`
- `location.search`
- `location.pathname`
- `location.origin`
- `location.port`
- `location.host`
- `location.hostname`
- `location.protocol`
- `location.origin` (Read only)

Let's explain all of the above properties on an example. Let's apply all of the above properties onto "https://example.org:8080/foo/bar?q=baz#bang"

- `location.href` - https://example.org:8080/foo/bar?q=baz#bang
- `location.hash` - #bang
- `location.search` - q=baz
- `location.pathname` - /foo/bar
- `location.origin` - https://example.org:8080
- `location.port` - 8080
- `location.host` - example.org:8080
- `location.hostname` - example.org
- `location.protocol` - https

`location.toString()` returns a string containing the whole URL. It is a read-only version of `location.href`.

If we want to go to a specific URL, we can manually set the `location.href` to a URL:

```js
setTimeout(() => {
  location.href = "http://localhost:5500/#hello";
  console.log(`redirected to ${location.origin}${location.pathname}#hello`);
}, 1000);
```

#### `location.assign()`

`location.assign(<url>)` loads the resource at the URL provided in the parameter. The URL can be absolute or relative. If the URL is not of the same origin as the script, it will cause an error.

```js
setTimeout(() => {
  location.assign("#hello");
  console.log(`redirected to ${location.origin}${location.pathname}#hello`);
}, 1000);
```

#### `location.replace()`

`location.replace(<url>)` replaces the current resource with the one at the provided URL (redirects to the provided URL).

The difference from the `assign()` method and setting the `href` property is that after using `replace()` the current page will not be saved in session `History`, meaning the user won't be able to use the back button to navigate to it.

```js
setTimeout(() => {
  location.replace("#hello");
  console.log(`redirected to ${location.origin}${location.pathname}#hello`);
}, 1000);
```

#### `location.reload()`

`location.reload()` reloads the current URL, like the Refresh button.

<hr>

### `window.open()` and `close`

The `Window` interface's `open(<URL> [, <target>, <windowFeatures>])` method

- takes a `<URL>` as a parameter, and loads the resource it identifies into a new or existing tab or window.
- The `<target>` parameter determines which window or tab to load the resource into, and
- the `<windowFeatures>` parameter can be used to control to open a new popup with minimal UI features and control its size and position.

For example:

```js
window.open("https://www.mozilla.org/", "mozillaTab");
```

The following example demonstrates how to open a popup, using the `popup` feature.

```js
window.open("https://www.mozilla.org/", "mozillaWindow", "popup");
```

`close()` closes the current window. This method can only be called on windows that were opened by a script using the `window.open()` method, or on top-level windows that have a single history entry.

```js
// Global variable to store a reference to the opened window
let openedWindow;

function openWindow() {
  openedWindow = window.open("https://www.mozilla.org/");
}

function closeOpenedWindow() {
  openedWindow.close();
}
```

The `window.closed` read-only property indicates whether the referenced window is closed or not. Returns `true` if the window has been closed or `false` if the window is open.

<hr>

### `window.confirm()`

`window.confirm()` instructs the browser to display a dialog with an optional message, and to wait until the user either confirms or cancels the dialog. It returns a boolean indicating whether OK (`true`) or Cancel (`false`) was selected.

```js
if (window.confirm("Do you really want to leave?")) {
  console.log("Thanks for Visiting!");
}
```

<hr>

### `window.getSelection()`

#### Range

JavaScript can access an existing selection, select/deselect DOM nodes as a whole or partially, remove the selected content from the document, wrap it into a tag, and so on. The basic concept of selection is `Range`, that is essentially a pair of “boundary points”: range start and range end.

A `Range` object is created without parameters

```js
const range = new Range();
```

After creating the `Range` objectm we can set the selection boundaries using `range.setStart(<node>, <offset>)` and `range.setEnd(<node>, <offset>)`.

- The first argument `<node>` in both methods can be either a text node or an element node, and the meaning of the second argument depends on what type of node is the first argument.

If `<node>` is a text node, then `<offset>` must be the position in its text.

```html
<p id="paragraph">Hello</p>

<script>
  let range = new Range();
  range.setStart(paragraph.firstChild, 2); // `firstChild` of `paragraph` is "Hello" - a text node
  range.setEnd(paragraph.firstChild, 4);

  // toString of a range returns its content as text
  console.log(range.toString()); // ll
</script>
```

If `<node>` is an element node, then `<offset>` must be the child number.

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 0); // 0th node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  // toString of a range returns its content as text, without tags
  console.log(range.toString()); // 0th text node, 1st text node,

  // select the range, as if we used a mouse and selected the range specified above
  document.getSelection().addRange(range);

  // You can see the childNodes of the paragraph
  console.log(paragraph.childNodes);
</script>
```

For text nodes, `<offset>` skips that many of characters, while for element nodes, that many child nodes.

We don’t have to use the same node in `setStart` and `setEnd`. A range may span across many unrelated nodes. It’s only important that the end is after the start in the document.

The range object that we created in the example above has following properties:

- `startContainer`, `startOffset` – node and offset of the start,
- `endContainer`, `endOffset` – node and offset of the end,
- `collapsed` – boolean, `true` if the range starts and ends on the same point (so there’s no content inside the range),
- `commonAncestorContainer` – the nearest common ancestor of all nodes within the range.

In addition to `setStart` and `setEnd`, there are other similar methods:

- `setStart(<node>, <offset>)` set start at: position offset in `<node>`
- `setStartBefore(<node>)` set start at: right before `<node>`
- `setEndBefore(<node>)` set end at: right before `<node>`
- `setEndAfter(<node>)` set end at: right after `<node>`

There are more methods to create ranges:

- `selectNode(<node>)` set range to select the whole node
- `selectNodeContents(<node>)` set range to select the whole node contents
- `collapse(toStart)`
- `cloneRange()` creates a new range with the same start/end

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  window.getSelection().addRange(range);

  setTimeout(() => {
    range.selectNode(paragraph);
  }, 1000);
</script>
```

The above methods are for creating ranges. There are also methods that are useful for editing ranges:

- `deleteContents()` – remove range content from the document
- `extractContents()` – remove range content from the document and return as `DocumentFragment`
- `cloneContents()` – clone range content and return as `DocumentFragment`
- `insertNode(node)` – insert node into the document at the beginning of the range
- `surroundContents(node)` – wrap node around range content. For this to work, the range must contain both opening and closing tags for all elements inside it: no partial ranges like `<i>abc`.

#### Selection

We may create `Range` objects but they do not visually select anything on their own. To select a range we use the `Selection` object, that can be obtained as `window.getSelection()` or `document.getSelection()`.

A selection may in theory contain multiple ranges (browser support isn't good at the moment). We can get these range objects using the method `getRangeAt(<i>)` – get i-th range, starting from 0.

Similar to a range, a selection object has a start, called “anchor”, and the end, called “focus”. Range objects always have their start before the end. But a selection object might have its anchor (start) after its focus (end).

The main selection properties are:

- `anchorNode` – the node where the selection starts,
- `anchorOffset` – the offset in `anchorNode` where the selection starts,
- `focusNode` – the node where the selection ends,
- `focusOffset` – the offset in `focusNode` where the selection ends,
- `isCollapsed` – true if selection selects nothing (empty range), or doesn’t exist.
- `rangeCount` – count of ranges in the selection, maximum 1 in all browsers except Firefox.

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  window.getSelection().addRange(range);

  console.log(window.getSelection().anchorNode); // p#paragraph
  console.log(window.getSelection().anchorOffset); // 1
  console.log(window.getSelection().focusNode); // p#paragraph
  console.log(window.getSelection().focusOffset); // 2
  console.log(window.getSelection().isCollapsed); // false
  console.log(window.getSelection().rangeCount); // 1
</script>
```

There are events on to keep track of selection:

- `<element>.onselectstart` – event fires when a selection starts specifically on `<element>` (or inside it). For instance, when the user presses the mouse button on it and starts to move the pointer.
  - Preventing the default action cancels the selection start. So starting a selection from this element becomes impossible, but the element is still selectable. The visitor just needs to start the selection from elsewhere.
- `document.onselectionchange` – whenever a selection changes or starts. Please note: this handler can be set only on document, it tracks all selections in it.

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  // will fire when a user clicks on a window
  window.addEventListener("selectstart", () => {
    console.log("selection started");
  });
</script>
```

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  // Fires even when the selection starts
  document.addEventListener("selectionchange", () => {
    console.log("selection has changed");
  });
</script>
```

There are two approaches to copying the selected content:

- We can use `document.getSelection().toString()` to get it as text.
- Otherwise, to copy the full DOM, e.g. if we need to keep formatting, we can get the underlying ranges with `getRangeAt(...)`. A `Range` object, in turn, has `cloneContents()` method that clones its content and returns as `DocumentFragment` object, that we can insert elsewhere.

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  document.getSelection().addRange(range);

  console.log(document.getSelection().toString()); // 1st node,
</script>
```

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  document.getSelection().addRange(range);

  console.log(document.getSelection().getRangeAt(0).toString()); // 1st node,
  console.log(document.getSelection().getRangeAt(0).startContainer); // p#paragraph
  console.log(document.getSelection().getRangeAt(0).endContainer); // p#paragraph

  const fragment = document.getSelection().getRangeAt(0).cloneContents();

  document.body.appendChild(fragment); // appends <i>1st node,</i>
</script>
```

In addition to `getRangeAt`, there are other useful methods:

- `addRange(<range>)` – add range to selection. All browsers except Firefox ignore the call, if the selection already has an associated range.
- `removeRange(<range>)` – remove range from the selection.
- `removeAllRanges()`– remove all ranges.
- `empty()`– alias to `removeAllRanges`.

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  document.getSelection().addRange(range);

  setTimeout(() => {
    document.getSelection().removeRange(range);
  }, 1000);
</script>
```

```html
<p id="paragraph">0th node, <i>1st node,</i> 2nd node, <b>3rd node</b></p>

<script>
  let range = new Range();

  range.setStart(paragraph, 1); // 1st node
  range.setEnd(paragraph, 2); // up to and exclusive of 2nd node

  document.getSelection().addRange(range);

  setTimeout(() => {
    document.getSelection().removeAllRanges();

    // below does the same as above
    // document.getSelection().empty();
  }, 1000);
</script>
```

If we don't want to access the underlying `Range` object, there are convenience methods to manipulate the selection range directly, without intermediate `Range` calls:

- `collapse(node, offset)` – replace selected range with a new one that starts and ends at the given node, at position offset.
- `setPosition(node, offset)` – alias to `collapse`.
- `collapseToStart()` – collapse (replace with an empty range) to selection start,
- `collapseToEnd()` – collapse to selection end,
- `extend(node, offset)` – move focus of the selection to the given node, position offset,
- `setBaseAndExtent(anchorNode, anchorOffset, focusNode, focusOffset)` – replace selection range with the given start `anchorNode`/`anchorOffset` and end `focusNode`/`focusOffset`. All content in-between them is selected.
- `selectAllChildren(node)` – select all children of the node.
- `deleteFromDocument()` – remove selected content from the document.
- `containsNode(node, allowPartialContainment = false)` – checks whether the selection contains node (partially if the second argument is true)

If a document selection already exists, empty it first with `removeAllRanges()`. And then add ranges. Otherwise, all browsers except Firefox ignore new ranges. The exception is some selection methods, that replace the existing selection, such as `setBaseAndExtent`.

#### Selection in forms

Form elements, such as input and textarea provide special API for selection, without `Selection` or `Range` objects.

- `input.selectionStart` – position of selection start (writeable),
- `input.selectionEnd` – position of selection end (writeable),
- `input.selectionDirection` – selection direction, one of: “forward”, “backward” or “none” (if e.g. selected with a double mouse click),

`input.onselect` – triggers when something is selected. `onselect` triggers when something is selected, but not when the selection is removed.

`document.onselectionchange` event should not trigger for selections inside a form control, according to the spec, as it’s not related to document selection and ranges. Some browsers generate it, but we shouldn’t rely on it.

```html
<input type="text" id="myInput" value="Hello, World!" />

<script>
  myInput.addEventListener("select", () => {
    console.log(myInput.selectionStart, myInput.selectionEnd);
    console.log(myInput.selectionDirection);
  });
</script>
```

- `input.select()` – selects everything in the text control (can be textarea instead of input),
- `input.setSelectionRange(start, end, [direction])` – change the selection to span from position start till end, in the given direction (optional).
- `input.setRangeText(replacement, [start], [end], [selectionMode])` – replace a range of text with the new text. Optional arguments start and end, if provided, set the range start and end, otherwise user selection is used. The last argument, `<selectionMode>`, determines how the selection will be set after the text has been replaced. The possible values are:
- `"select"` – the newly inserted text will be selected.
- `"start"` – the selection range collapses just before the inserted text (the cursor will be immediately before it).
- `"end"` – the selection range collapses just after the inserted text (the cursor will be right after it).
- `"preserve"` – attempts to preserve the selection. This is the default.

<hr>
<hr>

## Fetch

### GET request

Here is an example of a GET request with Fetch:

```js
const url = "https://jsonplaceholder.typicode.com/users";

// GET request with Fetch
fetch(url)
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

```js
// the same as above
fetch(url, {
  method: "GET", // GET method cannot have the "body" property
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

We can choose only one body-reading method.

- `response.text()` – read the response and return as text,
- `response.json()` – parse the response as JSON,
- `response.formData()` – return the response as `FormData` object,
- `response.blob()` – return the response as `Blob` (binary data with type),
- `response.arrayBuffer()` – return the response as `ArrayBuffer` (low-level representation of binary data),
- Additionally, `response.body` is a ReadableStream object, it allows you to read the body chunk-by-chunk

Here is an example of using `response.text`:

```js
const url = "https://jsonplaceholder.typicode.com/users";

fetch(url)
  .then((response) => response.text())
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

<hr>

### POST request

Here is an example of a POST request with Fetch:

```js
const postUrl = "https://httpbin.org/post";

const data = {
  name: "Some Name",
  username: "Some Username",
};

fetch(postUrl, {
  method: "POST",
  body: JSON.stringify(data),
  headers: { "Content-Type": "application/json" },
})
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```

<hr>

### Fetch and HTTP status codes

By default, the fetch function does not consider HTTP status codes such as 404 (Not Found) or 500 (Internal Server Error) as errors. To check for HTTP errors, you can use the `ok` property of the Response object, which returns `true` if the status code is in the range 200-299 (successful) and `false` otherwise.

```js
const url = "https://jsonplaceholder.typicode.com/users";

fetch(url)
  .then((response) => {
    console.log(response.ok);
    console.log(response.status);

    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

<hr>

### Headers

We can use the `get` method of the Headers object to retrieve the value of a specific header

```js
const url = "https://jsonplaceholder.typicode.com/users";

fetch(url)
  .then((response) => {
    console.log(response.ok);
    console.log(response.status);

    console.log(response.headers.get("Content-Type")); // "application/json"
  })
  .catch((error) => console.error(error));
```

Here is how to `set` headers using the `new Headers()` syntax:

```js
const postUrl = "https://httpbin.org/post";

const headers = new Headers();

headers.set("Authorization", "Bearer 123456");
headers.set("Content-Type", "application/json");

fetch(postUrl, {
  method: "POST",
  body: JSON.stringify({ name: "Some Name" }),
  headers: headers,
})
  .then((res) => {
    return res.json();
  })
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```

Here is how to `delete` headers using the `.delete()` method from the `Headers` object:

```js
const headers = new Headers();
headers.set("Authorization", "Bearer 123456");
headers.delete("Authorization");

fetch("https://example.com/api/users", {
  method: "POST",
  headers: headers,
})
  .then((res) => {
    return res.json();
  })
  .then((data) => console.log(data))
  .catch((error) => console.error(error));
```

<hr>

### Cancel a fetch request

We can cancel a `fetch` request by calling the `AbortController.abort()`. `AbortController` is a special built-in object and can be used to abort not only `fetch`, but other asynchronous tasks as well. To be able to cancel `fetch`, pass the `signal` property of an `AbortController` as a `fetch` option. For example, `fetch(url, {signal: controller.signal});`

```js
const url = "https://jsonplaceholder.typicode.com/users";

const controller = new AbortController();
const signal = controller.signal;

fetch(url, { signal })
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

// Cancel the request
controller.abort();
```

`AbortController` has a single method `abort()`, and a single property `signal` that allows to set event listeners on it.

When `abort()` is called:

- `controller.signal` emits the `"abort"` event. This allows to set event listeners on this property.
- `controller.signal.aborted` property becomes `true`.

We can use the `AbortSignal.aborted` property to check if the signal has been aborted.

```js
const url = "https://jsonplaceholder.typicode.com/users";

const controller = new AbortController();
const signal = controller.signal;

fetch(url, { signal })
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

// Cancel the request
controller.abort();

if (signal.aborted) {
  console.log("The request has been cancelled");
}
```

We can also use the `addEventListener` method to listen for the `abort` event, which is emitted when the `signal` is aborted.

```js
const url = "https://jsonplaceholder.typicode.com/users";

const controller = new AbortController();
const signal = controller.signal;

fetch(url, { signal })
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

signal.addEventListener("abort", () => {
  console.log("The request has been cancelled");
});

// Cancel the request
controller.abort();
```

When a `fetch` is aborted, its promise rejects with an error `AbortError`.

<hr>
<hr>

## Regular Expressions

Regular expressions are patterns that provide a powerful way to search in and replace a text. In JavaScript, they are available via the `RegExp` object, as well as being integrated in string methods. A Regular Expression consists of a pattern and optional flags.

### Creating Regular Expressions

There are two syntaxes that can be used to create a regular expression object.

- The “long” syntax:

```js
const regexp = new RegExp("<pattern>" [, "<flags>"]);
```

- And the “short” one, using a regular expression literal. This one is done by using forward slashes `/<regexp>/`:

```js
const regexp = /pattern/; // no flags
```

```js
const regexp = /pattern/gim; // with flags g,m and i
```

You should use a regex literal when you know the regular expression pattern at the time of writing the code. On the other hand, use the `RegExp` constructor if the regex pattern is to be created dynamically. Also, the regex constructor lets you write a pattern using a template literal, but this is not possible with the regex literal syntax.

<hr>

### Flags

There are 6 flags in JavaScript's Regular Expressions:

- `i` - With this flag the search is case-insensitive: no difference between "A" and "a".
- `g` - With this flag the search looks for all matches, without it – only the first match is returned.
- `s` - Enables “dotall” mode, that allows a dot `.` to match newline character `\n`
- `u` - Enables full Unicode support. The flag enables correct processing of surrogate pairs.
- `m` - Multiline mode
- `y` - “Sticky” mode: searching at the exact position in the text

<hr>

### Regular Expression methods

#### `.match()`

The method `<string>.match(<regexp>)` finds all matches of `<regexp>` in the string `<string>`.

Here is an example without any flags. Without the flag `g`, it returns only the first match in the form of an array, with the full match at index 0 and some additional details in properties.

```js
const str = "We will, we will rock you";

const result = str.match(/we/);

console.log(result[0]); // we (1st match)
console.log(result.index); // 9 (position of the match)

console.log(result.input); // We will, we will rock you (source string)
console.log(result.length); // 1
```

We add the `i` flag to make the search case-insensitive.

```js
const str = "We will, we will rock you";

const result = str.match(/we/i);

console.log(result[0]); // We (1st match)
console.log(result.index); // 0 (position of the match)

console.log(result.input); // We will, we will rock you (source string)
console.log(result.length); // 1
```

Then, we add the flag `g` which returns an array of all matches.

```js
const str = "We will, we will rock you";

const result = str.match(/we/gi);

console.log(result); // Array [ "We", "we" ]
```

If there are no matches, `null` is returned.

```js
const str = "Hello";

const result = str.match(/bye/i);

console.log(result); // null
```

#### `.replace()`

The `<string>.replace(<string>, <replacement)` method could be used on strings to replace parts of the string.

```js
const str = "JavaScript";
const newStr = str.replace("ava", "").replace("cript", "");
console.log(newStr); // JS
```

The method could also be used with regular expressions. `<string>.replace(<regexp>, <replacement>)` replaces matches found using `<regexp>` in string `<string>` with `<replacement>` (all matches if there’s flag `g`, otherwise, only the first one).

```js
// no flag g
console.log("We will, we will".replace(/we/i, "I")); // I will, we will

// with flag g
console.log("We will, we will".replace(/we/gi, "I")); // I will, I will
```

There are symbols that we can use to control the replacement process.

| Symbols          | Actions                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------- |
| `$&`             | inserts the whole match                                                                      |
| `` $` ``         | inserts a string before the match                                                            |
| `$'`             | inserts a string after the match                                                             |
| `$$`             | inserts character `$`                                                                        |
| `$group_number`  | Works with capturing groups. Inserts the contents of a capturing group in the `group_number` |
| `$<group_name> ` | Works with capturing groups. Inserts the contents of the parentheses with the given `<name>` |

```js
console.log("I love HTML and CSS".replace(/HTML/, "$&, JavaScript")); // I love HTML, JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$`, JavaScript")); // I love I love , JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$', JavaScript")); // I love  and CSS, JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$$, JavaScript")); // I love $, JavaScript and CSS

console.log("Name Surname".replace(/(Name)\s(Surname)/, "$2, $1")); // Surname, Name

console.log(
  "Name Surname".replace(
    /(?<firstName>Name)\s(?<lastName>Surname)/,
    "$<lastName>, $<firstName>",
  ),
); // Surname, Name
```

The `<replacement>` could also be a function. The `replace()` method will invoke the **replacer** function after the match has been performed and use the result of this function as the replacement string. The **replacer** function has the following syntax:

```js
function replacer(match, p1, p2, ..., offset, string);
```

The following are the meanings of each parameter:

- **match** is the matched substring.
- **p1, p2, …pn** are the nth string found by a parenthesized capture group provided by the regular expression.
- **offset** is the offset of the matched substring within the whole string being searched.
- **string** is the whole string being examined.

```js
const str = "I love HTML and CSS";

const result = str.replace(/(HTML)/, (match, p1, offset, string) => {
  console.log(match);
  console.log(p1);
  console.log(offset);
  console.log(string);

  return `HTML, JavaScript`;
});

console.log(result); // I love HTML, JavaScript and CSS
```

#### `.replaceAll()`

The main use case for `replaceAll` is replacing all occurrences of a string. This method is essentially the same as `<str>.replace()`, with two major differences:

- If the first argument is a string, it replaces all occurrences of the string, while `replace` replaces only the first occurrence.
- If the first argument is a regular expression, the `g` flag must be provided. Otherwise, there’ll be an error.

```js
const str = "I love HTML and CSS, HTML, HTML";

const result1 = str.replace(/(HTML)/g, (match, p1, offset, string) => {
  return match.toLowerCase();
});

const result2 = str.replaceAll(/(HTML)/g, (match, p1, offset, string) => {
  return match.toLowerCase();
});

console.log(result1); // I love html and CSS, html, html
console.log(result2); // I love html and CSS, html, html
```

#### `<regexp>.test()`

The method `<regexp>.test(<str>)` looks for at least one match, if found, returns `true`, otherwise `false`.

```js
const regexp = /hello/i;

console.log(regexp.test("Hello there")); // true
console.log(regexp.test("Hi there")); // false
```

<hr>

### Character classes

A character class is a special notation that matches any symbol from a certain set.

The **digit** class is written as `\d` and corresponds to “any single digit”.

```js
const phoneNumber = "+1(234)-567-89-01";

console.log(phoneNumber.match(/\d/)); // 1
console.log(phoneNumber.match(/\d/g)); // Array of 1, 2, 3 ... 9, 0, 1

console.log(phoneNumber.match(/\d/g).join("")); // 12345678901
```

The **space** class is denoted as `\s` and includes spaces, tabs `\t`, newlines `\n` and few other rare characters, such as `\v`, `\f` and `\r`.

```js
const str = "A sentence with some spaces.";

console.log(str.match(/\s/g)); // Array(4) [ " ", " ", " ", " " ]
```

The **word** class is denoted as `\w` and it is either a letter of Latin alphabet or a digit or an underscore \_. Non-Latin letters do not belong to `\w`.

```js
const str = "A word";

console.log(str.match(/\w/g)); // Array(5) [ "A", "w", "o", "r", "d" ]
```

A regexp may contain both regular symbols and character classes.

```js
const cssString = "CSS3 is the current version of CSS";

console.log(cssString.match(/CSS\d/)); // Array [ "CSS3" ]
```

A regexp can also contain one character class after another one.

```js
const str = "1 a";
const str2 = `1
a`;
const str3 = " abcde 12 ";

console.log(str.match(/\d\s\w/)); // matches - returns [ "1 a" ]
console.log(str2.match(/\d\s\w/)); // matches - returns [ "1\na" ]
console.log(str3.match(/\d\s\w/)); // doesnt't match - returns null
```

#### Inverse classes

For every character class there exists an “inverse class”, denoted with the same letter, but uppercased. The “inverse” means that it matches all other characters, for instance:

- `\D` means non-digit: any character except `\d`, for instance a letter.
- `\S` means non-space: any character except `\s`, for instance a letter.
- `\W` means non-wordly character: anything but `\w`, e.g a non-latin letter or a space.

In the below example, we find all the non-digits using `/\D/g`, and replace them.

```js
const phoneNumber = "+1(234)-567-89-01";

console.log(phoneNumber.replace(/\D/g, "")); // 12345678901
```

<hr>

### Using dot `.`

A dot `.` is a special character class that matches “any character except a newline”.

```js
console.log("ABcd".match(/./)); // Array [ "A" ]
console.log("ABcd".match(/./g)); // Array(4) [ "A", "B", "c", "d" ]

console.log("him".match(/hi./)); // Array [ "him" ]
console.log("his".match(/hi./)); // Array [ "his" ]
```

By default, a dot `.` doesn’t match the newline character `\n`.

```js
console.log("A-B".match(/A.B/)); // Array [ "A-B" ]
console.log("A B".match(/A.B/)); // Array [ "A B" ]
console.log("A\nB".match(/A.B/)); // null
```

If we want the dot `.` to include the newline character `\n` as well, then we can use the `s` flag.

```js
console.log("A\nB".match(/A.B/s)); // Array [ "A\nB" ]
```

<hr>

### Unicode encoding and `u` flag

JavaScript uses Unicode encoding for strings. Most characters are encoded with 2 bytes, but there are some that are 4 bytes. When JavaScript language was created, Unicode encoding was simpler: there were no 4-byte characters. So, some JavaScript features still handle 4-byte characters incorrectly. For instance, `length` treats 4 bytes as two 2-byte characters. Therefore, `length` thinks that there are two characters here:

```js
console.log("😄".length); // 2
console.log("𝒳".length); // 2
```

This might be problematic when we are working with regular expressions. To avoid the problem, we use the `u` flag. With the `u` flag, a regexp handles 4-byte characters correctly.

Every character in Unicode has a lot of properties. They describe what “category” the character belongs to and contain miscellaneous information about it. For instance, if a character has the `Letter` property, it means that the character belongs to an alphabet (of any language). A `Number` property means that it’s a digit: maybe Arabic or Chinese, and so on.

We can search for characters with a property, by writing `/\p{<unicode_property>}/u`. To use `\p{…}`, a regular expression must have the `u` flag. For instance, `\p{Letter}` denotes a letter in any language. We can also use `\p{L}`, as `L` is an alias of `Letter`.

```js
const str = "A ბ ㄱ";

console.log(str.match(/\p{L}/gu)); // Array(3) [ "A", "ბ", "ㄱ" ]
console.log(str.match(/\p{L}/g)); // null - `\p` doesn't work without the flag `u`
```

Here are the main character categories and their subcategories:

- Letter `L`:
  - lowercase `Ll`,
  - modifier `Lm`,
  - titlecase `Lt`,
  - uppercase `Lu`,
  - other `Lo`.
- Number `N`:
  - decimal digit `Nd`,
  - letter number `Nl`,
  - other `No`.
- Punctuation `P`:
  - connector `Pc`,
  - dash `Pd`,
  - initial quote `Pi`,
  - final quote `Pf`,
  - open `Ps`,
  - close `Pe`,
  - other `Po`.
- Mark `M` (accents etc):
  - spacing combining `Mc`,
  - enclosing `Me`,
  - non-spacing `Mn`.
- Symbol `S`:
  - currency `Sc`,
  - modifier `Sk`,
  - math `Sm`,
  - other `So`.
- Separator `Z`:
  - line `Zl`,
  - paragraph `Zp`,
  - space `Zs`.
- Other `C`:
  - control `Cc`,
  - format `Cf`,
  - not assigned `Cn`,
  - private use `Co`,
  - surrogate `Cs`.

Here are links to learn more about Unicode

- List all properties by a character: https://unicode.org/cldr/utility/character.jsp.
- List all characters by a property: https://unicode.org/cldr/utility/list-unicodeset.jsp.
- Short aliases for properties: https://www.unicode.org/Public/UCD/latest/ucd/PropertyValueAliases.txt.
- A full base of Unicode characters in text format, with all properties, is here: https://www.unicode.org/Public/UCD/latest/ucd/.

<hr>

### Anchors: string start `^` and end `$`

The caret `^` and dollar `$` characters have special meaning in a regexp. They are called **anchors**. The caret `^` matches at the beginning of the text, and the dollar `$` – at the end.

```js
const str = "Beginning is here. Here is the ending";

console.log(str.match(/^Beginning/)); // Array [ "Beginning" ]
console.log(str.match(/ending$/)); // Array [ "ending" ]
```

Both anchors together `^...$` are often used to test whether or not a string fully matches the pattern. For instance, to check if the user input is in the right format

```js
const goodInput = "12:34";
const badInput = "12:345";

const regexp = /^\d\d:\d\d$/;

console.log(regexp.test(goodInput)); // true
console.log(regexp.test(badInput)); // false
```

#### Multiline mode of anchors `^`, `$` and the flag `m`

The multiline mode with the flag `m` only affects the behavior of `^` and `$`. In the multiline mode anchors match not only at the beginning and the end of the string, but also at start/end of a line.

In the below example, the pattern `/^\d/gm` takes a digit from the beginning of each line:

```js
const str = `1st place
2nd place
3rd place`;

console.log(str.match(/^\d/gm)); // Array(3) [ "1", "2", "3" ]

// Without the flag `m` only the first digit is matched
console.log(str.match(/^\d/g)); // Array [ "1" ]
```

In the below example, the pattern `/\d$/gm` takes a digit from the end of each line:

```js
const str = `Winnie: 1
Piglet: 2
Eeyore: 3`;

console.log(str.match(/\d$/gm)); // Array(3) [ "1", "2", "3" ]

// Without the flag `m` only the digit at the end of the whole text is matched
console.log(str.match(/\d$/g)); // Array [ "3" ]
```

<hr>

### Word boundary: `\b`

A word boundary `\b` is similar to `^` and `$`. It tests if there is a word boundary. There are three different positions that qualify as word boundaries:

- At string start, if the first string character is a word character `\w`.
- Between two characters in the string, where one is a word character `\w` and the other is not.
- At string end, if the last string character is a word character `\w`.

```js
console.log("Hello, JavaScript!".match(/\bHello\b/)); // Array [ "Hello" ]
console.log("Hello, JavaScript!".match(/\bJavaScript\b/)); // Array [ "JavaScript" ]
console.log("Hello, JavaScript!".match(/\bHell\b/)); // null (no match)
console.log("Hello, JavaScript!".match(/\bJava!\b/)); // null (no match)
```

We can use `\b` with digits as well. For example, the pattern `\b\d\d\b` looks for standalone 2-digit numbers. In other words, it looks for 2-digit numbers that are surrounded by characters different from `\w`, such as spaces or punctuation.

```js
console.log("1 23 456 78".match(/\b\d\d\b/g)); // Array [ "23", "78" ]
console.log("12,34,56".match(/\b\d\d\b/g)); // Array(3) [ "12", "34", "56" ]
```

The word boundary test `\b` checks that there should be `\w `on the one side from the position and "not `\w`" – on the other side. But `\w `means a latin letter a-z (or a digit or an underscore), so the test doesn’t work for other characters, e.g. cyrillic letters or hieroglyphs.

<hr>

### Escaping Special characters

There are special characters in a regexp, such as `[ ] { } ( ) \ ^ $ . | ? * +`.

So far, we have used a backslash `\` as a special character in regex. It is used to denote character classes like `\d` for digits, `\s` for spaces, etc. But it's also used for escaping. If there is a special character, let's say a dot `.`, and we don't want to use the dot as a special character, then we can use `\` to indicate that we are looking for a regular dot. This is called escaping a character. By using the `\` we are escaping the special use case of a character.

```js
console.log("Chapter 5.1".match(/\d\.\d/)); // 5.1 (match!)
console.log("Chapter 511".match(/\d\.\d/)); // null (looking for a real dot \.)

// we don't escape the dot in the below example
console.log("Chapter 511".match(/\d.\d/)); // Array [ "511" ]
```

Here is one more example. Parenteses are special characters, so we are escaping them in the below example:

```js
console.log("function g()".match(/g\(\)/)); // Array [ "g()" ]
```

A slash symbol '/' is not a special character, but in JavaScript it is used to open and close the regexp: `/...pattern.../`, so we should escape it too:

```js
console.log("path/to/folder".match(/\//)); // Array [ "/" ]
```

If we’re not using `/.../`, but create a regexp using `new RegExp`, then we don’t need to escape it:

```js
console.log("path/to/folder".match(new RegExp("/"))); // Array [ "/" ]
```

From the above example, it's visible that `new Regexp()` accepts a string as an argument to create a regular expression. That might cause a problem with using a backslash, because backslash has its own meaning while used as part of a string. For example:

- `\n` – becomes a newline character,
- `\u0024` – becomes the Unicode character with such code,
- …And when there’s no special meaning: like `\d` or `\z`, then the backslash is simply removed.

```js
console.log("d\nd"); // d [new line] d
console.log("\u0024 "); // $ - unicode character
console.log("d.d"); // d.d
```

So, if we need to use `new Regexp()`, and we want to use the backslash in it, the way backslash is used in `/.../` pattern, then we need to use double backslash `\\`.

```js
const regStr = "\\d\\.\\d";
console.log(regStr); // \d\.\d

const regexp = new RegExp(regStr);
console.log("Chapter 5.1".match(regexp)); // 5.1
```

<hr>

### Sets and ranges

Several characters or character classes inside square brackets `[…]` mean to “search for any character among given”. That’s called a **set** and they can be used in a regexp along with regular characters:

```js
// find "t" or "m", and then "op"
console.log("Mop top".match(/[tm]op/gi)); // Array [ "Mop", "top" ]
```

Note that although there are multiple characters in the set, they correspond to exactly one character in the match.

```js
// find "V", then "o" or "i", then "la"
console.log("Voila".match(/V[oi]la/)); // null, no matches

console.log("Vila".match(/V[oi]la/)); // Array [ "Vila" ]

console.log("Vola".match(/V[oi]la/)); // Array [ "Vola" ]
```

Square brackets may also contain character ranges:

- `[a-z]` is a character in range from a to z
- `[0-5]` is a digit range from 0 to 5

```js
console.log("Exception 0xAF".match(/[0-9]x[A-F][A-F]/g)); // Array [ "0xAF" ]

// We can have more than one range in the same [ ... ]
console.log("Exception 0xAF".match(/[0-9]x[0-9A-F][0-9A-F]/g)); // Array [ "0xAF" ]
console.log("Exception 0xA5".match(/[0-9]x[0-9A-F][0-9A-F]/g)); // Array [ "0xA5" ]
```

We can also use special characters in sets:

- `\d` – is the same as `[0-9]`,
- `\w` – is the same as `[a-zA-Z0-9_]`,
- `\s` – is the same as `[\t\n\v\f\r ]`, plus few other rare Unicode space characters.

Besides normal ranges, there are “excluding” ranges that look like `[^…]`. They are denoted by a caret character `^` at the start and match any character except the given ones.

The example below looks for any characters except letters, digits and spaces:

```js
console.log("test15@example.com".match(/[^\d\sA-Z]/gi)); // Array [ "@", "." ]
```

In square brackets, we can use the vast majority of special characters without escaping:

- Symbols `. + ( )` never need escaping.
- A hyphen `-` is not escaped in the beginning or the end (where it does not define a range).
- A caret `^` is only escaped in the beginning (where it means exclusion).
- The closing square bracket `]` is always escaped (if we need to look for that symbol).

But if you decide to escape them just in case, then it won't be a problem.

<hr>

### Quantifiers `+`, `\*`, `?` and `{<number>}`

A quantifier is appended to a character (or a character class, or a set etc) and specifies how many we need.

The simplest quantifier is a number in curly braces: `{<number>}`. For example, `\d{4}` is the same as `\d\d\d\d`.

```js
console.log("1 12 123 1234 12345".match(/\d{4}/)); //  Array [ "123" ]
```

The range: `{3,5}` means match 3 to 5 times.

```js
console.log("1 12 123 1234 12345".match(/\d{3,5}/)); //  Array [ "123" ]
console.log("1 12 123 1234 12345".match(/\d{3,5}/g)); //  Array(3) [ "123", "1234", "12345" ]
```

We can omit the upper limit and write `{3,}`.

```js
console.log("1 12 123 1234 12345".match(/\d{3,}/)); //  Array [ "123" ]
console.log("1 12 123 1234 12345".match(/\d{3,}/g)); //  Array(3) [ "123", "1234", "12345" ]
```

Instead of writing something as `{1,}`, we can use the shorthand `+`. `+` means match something one or more times:

```js
console.log("1 12 123 1234 12345".match(/\d{1,}/)); //  Array [ "1" ]
console.log("1 12 123 1234 12345".match(/\d{1,}/g)); //  Array(5) [ "1", "12", "123", "1234", "12345" ]

console.log("1 12 123 1234 12345".match(/\d+/)); //  Array [ "1" ]
console.log("1 12 123 1234 12345".match(/\d+/g)); //  Array(5) [ "1", "12", "123", "1234", "12345" ]
```

Instead of writing something as `{0,1}`, we can use the shorthand `?`. `?` means match something zero times or once:

```js
const str = "Should I write color or colour?";

console.log(str.match(/colou{0,1}r/g)); // Array [ "color", "colour" ]
console.log(str.match(/colou?r/g)); // Array [ "color", "colour" ]
```

Instead of writing something as `{0,}`, we can use the shorthand `*`. `*` means match something zero times or more:

```js
console.log("100 10 1".match(/\d0*/g)); // Array(3) [ "100", "10", "1" ]
```

<hr>

### Greedy and lazy quantifiers

There is something called greedy search in regular expressions. In the greedy mode (by default), a quantified character is repeated as many times as possible.

To understand let's see an example. Let's say, we want to retrieve all the words that are in quotes from a sentence. Let's try using `/".+"/g`:

```js
const regexp = /".+"/g;

const str = 'a "witch" and her "broom" is one';

console.log(str.match(regexp)); // Array [ '"witch" and her "broom"' ]
```

It doesn't work. Instead of finding two matches "witch" and "broom", it finds one: "witch" and her "broom".

- First, JavaScript tries to find the quote. JavaScript finds the quote at the 3rd position.
- Then it tries to see if the rest of the subject string conforms to `.+"`.
- It tries to match the dot. Dot means any character, except the newline. So, the next character matches the dot. But we have provided `+` and therefore JavaScript tries to check if more characters match the dot. All characters match the dot, so it only stops when it reaches the end of the string.
- Now the engine finished repeating `.+` and tries to find the next character of the pattern. It’s the quote `"`. But the string has finished. The regular expression engine understands that it took too many `.+` and starts to backtrack.
- Now it assumes that `.+` ends one character before the string end and tries to match the rest of the pattern from that position. It keeps backtracking until it finds the quote.
- Finally, the result ends up being `"witch" and her "broom"`.

The **lazy** mode of quantifiers is an opposite to the greedy mode. It means: “repeat minimal number of times”. We can enable it by putting a question mark `?` after the quantifier. Usually a question mark `?` is a quantifier by itself (zero or one), but if added after another quantifier (or even itself) it gets another meaning – it switches the matching mode from greedy to lazy. So,

- `*` becomes `*?`,
- `+` becomes `+?`,
- `?` becomes `??`.

The regexp `/".+?"/g` works as intended: it finds "witch" and "broom":

```js
const regexp = /".+?"/g;

const str = 'a "witch" and her "broom" is one';

console.log(str.match(regexp)); // Array [ '"witch"', '"broom"' ]
```

<hr>

### Capturing groups

A part of a pattern can be enclosed in parentheses `(...)`. This is called a “capturing group”. It has two effects:

- It allows to get the part of a match as a separate item in the result array.
- If we put a quantifier after the parentheses, it applies to the parentheses as a whole.

```js
console.log("Gogogo now!".match(/go+/gi)); // Array(3) [ "Go", "go", "go" ]

console.log("Gogogo now!".match(/(go)+/gi)); // Array [ "Gogogo" ]
```

Parentheses are numbered from left to right. The search engine memorizes the content matched by each of them and allows to get it in the result. The method `<str>.match(<regexp>)`, if regexp has no flag `g`, looks for the first match and returns it as an array:

- At index 0: the full match.
- At index 1: the contents of the first parentheses.
- At index 2: the contents of the second parentheses.
- …and so on…

```js
const str = "<h1>Hello, world!</h1>";

const tag = str.match(/<(.*?)>/);

console.log(tag[0]); // <h1>
console.log(tag[1]); // h1
```

Parentheses can be nested.

```js
const str = '<span class="my">';

const regexp = /<(([a-z]+)\s*([^>]*))>/;

const result = str.match(regexp);
console.log(result[0]); // <span class="my">
console.log(result[1]); // span class="my"
console.log(result[2]); // span
console.log(result[3]); // class="my"
```

When we search for all matches (flag `g`), the `match` method does not return contents for capturing groups. For example, let’s find all tags in a string:

```js
const str = "<h1> <h2>";

const tags = str.match(/<(.*?)>/g);

console.log(tags); // Array [ "<h1>", "<h2>" ]
```

To get `groups` in the result, we should search using the method `<str>.matchAll(<regexp>)`. Just like `match`, it looks for matches, but there are 3 differences:

- It returns not an array, but an iterable object.
- When the flag `g` is present, it returns every match as an array with groups.
- If there are no matches, it returns not `null`, but an empty iterable object.

```js
let results = "<h1> <h2>".matchAll(/<(.*?)>/gi);

// results - is not an array, but an iterable object
console.log(results); // RegExp String Iterator {  }

console.log(results[0]); // undefined (*)

results = Array.from(results); // let's turn it into array

console.log(results[0]); // Array [ "<h1>", "h1" ]
console.log(results[1]); // Array [ "<h2>", "h2" ]
```

Remembering groups by their numbers is hard. For simple patterns it’s doable, but for more complex ones counting parentheses is inconvenient. We can give a name to a capturing group. That’s done by putting `?<group_name>` **immediately after the opening parenthesis**.

```js
const str = "2019-04-30";

const dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/;

const groups = str.match(dateRegexp).groups;

console.log(groups); // Object { year: "2019", month: "04", day: "30" }
console.log(groups.year); // 2019
console.log(groups.month); // 04
console.log(groups.day); // 30
```

As you can see, the groups reside in the `.groups` property of the `match`. To look for all dates, we can add flag `g`. We’ll also need `matchAll` to obtain full matches, together with groups:

```js
const str = "2019-10-30 2020-01-01";

const dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;

const results = str.matchAll(dateRegexp);

for (let result of results) {
  const { year, month, day } = result.groups;

  console.log(`${day}.${month}.${year}`);
  // first log: 30.10.2019
  // second log: 01.01.2020
}
```

Method `<str>.replace(<regexp>, <replacemen>t)` that replaces all matches with regexp in `<str>` allows to use parentheses contents in the `<replacement>` string. That’s done using `$group_number` syntax.

```js
const str = "John Bull";
const regexp = /(\w+) (\w+)/;

console.log(str.replace(regexp, "$2, $1")); // Bull, John
```

For named parentheses, the reference will be `$<name>`.

```js
const regexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;

const str = "2019-10-30, 2020-01-01";

console.log(str.replace(regexp, "$<day>.$<month>.$<year>"));
// 30.10.2019, 01.01.2020
```

Sometimes we need parentheses to correctly apply a quantifier, but we don’t want their contents in results. A group may be excluded by adding `?:` in the beginning:

```js
const str = "Gogogo John!";

// ?: excludes 'go' from capturing
const regexp = /(?:go)+ (\w+)/i;

const result = str.match(regexp);

console.log(result[0]); // Gogogo John (full match)
console.log(result[1]); // John
console.log(result.length); // 2 (no more items in the array)
```

<hr>

### Backreferences in pattern: `\N` and `\k<name>`

We can use the contents of capturing groups `(...)` not only in the result or in the replacement string, but also in the pattern itself. A group can be referenced in the pattern using `\N`, where `N` is the group number.

```js
const str = `He said: "She's the one!".`;

// `\1` means “find the same text as in the first group”
const regexp = /(['"])(.*?)\1/g;

console.log(str.match(regexp)); // Array [ `"She's the one!"` ]
```

If we use `?:` in the group, then we can’t reference it. Groups that are excluded from capturing `(?:...)` are not memorized by the engine.

To reference a named group, we can use `\k<name>`.

```js
const str = `He said: "She's the one!".`;

const regexp = /(?<quote>['"])(.*?)\k<quote>/g;

console.log(str.match(regexp)); // Array [ `"She's the one!"` ]
```

<hr>

### Alternation (OR) `|`

Alternation is the term in regular expression that is actually a simple “OR”. In a regular expression, it is denoted with a vertical line character `|`.

```js
const regexp = /html|php|css|java(script)?/gi;

const str = "First HTML appeared, then CSS, then JavaScript";

console.log(str.match(regexp)); // Array(3) [ "HTML", "CSS", "JavaScript" ]
```

To apply alternation to a chosen part of the pattern, we can enclose it in parentheses:

- I love `HTML|CSS` matches I love HTML or CSS.
- I love `(HTML|CSS)` matches I love HTML or I love CSS.

```js
const str = "I love HTML and CSS";
const str2 = "I love CSS";

// This tries to find either "I love HTML" or "CSS"
console.log(str.match(/I love HTML|CSS/g)); // Array [ "I love HTML", "CSS" ]
console.log(str2.match(/I love HTML|CSS/g)); // Array [ "CSS" ]

// This tries to find either "I love HTML" or "I love CSS"
console.log(str.match(/I love (HTML|CSS)/g)); // Array [ "I love HTML" ]
console.log(str2.match(/I love (HTML|CSS)/g)); // Array [ "I love CSS" ]
```

One more example:

```js
// better time regexp
const regexp = /([01]\d|2[0-3]):[0-5]\d/g;

console.log("00:00 10:10 23:59 25:99 1:2".match(regexp)); // Array(3) [ "00:00", "10:10", "23:59" ]
```

<hr>

### Lookahead and lookbehind

Sometimes we need to find only those matches for a pattern that are followed or preceded by another pattern. There’s a special syntax for that, called “lookahead” and “lookbehind”, together referred to as “lookaround”. The syntax is: `X(?=Y)`, it means "look for X, but match only if followed by Y". There may be any pattern instead of X and Y. Please note: the lookahead is merely a test, the contents of the parentheses `(?=...)` is not included in the result.

```js
const str = "1 turkey costs 30€";

console.log(str.match(/\d+(?=€)/)); // Array [ "30" ], the number 1 is ignored, as it's not followed by €
```

More complex tests are possible, e.g. `X(?=Y)(?=Z)` means:

- Find X.
- Check if Y is immediately after X (skip if isn’t).
- Check if Z is also immediately after X (skip if isn’t).
- If both tests passed, then the X is a match, otherwise continue searching.

```js
const str = "1 turkey costs 30€";

// looks for \d+ that is followed by a space (?=\s), and there’s 30 somewhere after it (?=.*30)
console.log(str.match(/\d+(?=\s)(?=.*30)/)); // Array [ "1" ]
```

There is also a negative lookahead. The syntax is: `X(?!Y)`, it means "search X, but only if not followed by Y".

```js
const str = "2 turkeys cost 60€";

console.log(str.match(/\d+\b(?!€)/g)); // Array [ "2" ] (the price is not matched)
```

Lookahead allows to add a condition for “what follows”. Lookbehind is similar, but it looks behind. The syntax is:

- Positive lookbehind: `(?<=Y)X`, matches X, but only if there’s Y before it.
- Negative lookbehind: `(?<!Y)X`, matches X, but only if there’s no Y before it.

Please Note: Lookbehind is not supported in non-V8 browsers, such as Safari, Internet Explorer.

```js
const str = "1 turkey costs $30";

// the dollar sign is escaped \$
// Positive lookbehind
console.log(str.match(/(?<=\$)\d+/)); // Array [ "30" ] (skipped the sole number)

// Negative lookbehind
console.log(str.match(/(?<!\$)\b\d+/g)); // Array [ "1" ] (the price is not matched)
```

Generally, the contents inside lookaround parentheses does not become the part of a result. E.g. in the pattern `\d+(?=€)`, the € sign doesn’t get captured as a part of the match. That’s natural: we look for a number `\d+`, while `(?=€)` is just a test that it should be followed by €. But in some situations we might want to capture the lookaround expression as well, or a part of it. If we want that, just wrap that part into additional parentheses.

```js
const str = "1 turkey costs 30€";
const regexp1 = /\d+(?=€)/;
const regexp2 = /\d+(?=(€))/; // extra parentheses around €

console.log(str.match(regexp1)); // Array [ "30" ]
console.log(str.match(regexp2)); // Array [ "30", "€" ]
```

And here’s the same for lookbehind:

```js
const str = "1 turkey costs $30";
const regexp1 = /(?<=\$|£)\d+/;
const regexp2 = /(?<=(\$|£))\d+/;

console.log(str.match(regexp1)); // Array [ "30" ]
console.log(str.match(regexp2)); // Array [ "30", "$" ]
```

<hr>

### Catastrophic backtracking

We mentioned that to turn from the greedy search mode to the lazy mode, we need to `?` after a quantifier. But in some situations, we might want to keep the greedy search mode, but get rid of the backtracking. To stop the backtracking, we add `+` after a quantifier. That is, we use `\d++` instead of `\d+` to stop `+` from backtracking. With one more `+`, the quantifier, in this example `\d++`, becomes a **possessive quantifier**. Possessive quantifiers are in fact simpler than “regular” ones. They just match as many as they can, without any backtracking. The search process without backtracking is simpler.

<hr>

### Sticky flag `y`, searching at position

The flag `y` allows to perform the search at the given position in the source string. We can use this flag with `<regexp>.exec(<str>)` method. For a regexp without flags `g` and `y`, this method looks only for the first match, it works exactly like `<str>.match(<regexp>)`. But if there’s flag `g`, then it performs the search in `<str>`, starting from the position stored in the `<regexp>.lastIndex` property. And, if it finds a match, then sets `<regexp>.lastIndex` to the index immediately after the match. If we can `exec` again, the next `exec` will run starting from the `<regexp>.lastIndex`.

```js
const str = "let varName"; // Let's find all words in this string
const regexp = /\w+/g;

console.log(regexp.lastIndex); // 0 (initially lastIndex=0)

const word1 = regexp.exec(str);
console.log(word1[0]); // let (1st word)
console.log(regexp.lastIndex); // 3 (position after the match)

const word2 = regexp.exec(str);
console.log(word2[0]); // varName (2nd word)
console.log(regexp.lastIndex); // 11 (position after the match)

const word3 = regexp.exec(str);
console.log(word3); // null (no more matches)
console.log(regexp.lastIndex); // 0 (resets at search end)
```

Here is the implementation with the `for` loop:

```js
const str = "let varName";
const regexp = /\w+/g;

let result;

while ((result = regexp.exec(str))) {
  console.log(`Found ${result[0]} at position ${result.index}`);
  // Found let at position 0, then
  // Found varName at position 4
}
```

If we want the `exec` to start searching from a specific position in a string, we can manually set `lastIndex` to a number.

```js
const str = 'let varName = "value"';

const regexp = /\w+/g; // without flag "g", property lastIndex is ignored

regexp.lastIndex = 4;

const word = regexp.exec(str);
console.log(word); // Array [ "varName" ]
```

The `regexp.exec` call starts searching at position `lastIndex` and then goes further. If there’s no word at position `lastIndex`, but it’s somewhere after it, then it will be found. If we need to find a match exactly at the given position at the text, not somewhere after it, we can use flag `y`. The flag `y` makes `<regexp>.exec` to search exactly at the position `lastIndex`, not “starting from” it.

```js
const str = 'let varName = "value"';

const regexp = /\w+/y;

regexp.lastIndex = 3;
console.log(regexp.exec(str)); // null (there's a space at position 3, not a word)

regexp.lastIndex = 4;
console.log(regexp.exec(str)); // Array [ "varName" ] (word at position 4)
```

<hr>

### Methods of RegExp and String

The `.split(<delimiter>)` could be used on a string without regular expressions. It splits a string by a provided delimiter. However, we can also use it with a regular expression.

```js
console.log("12, 34, 56".split(/,\s*/)); // Array(3) [ "12", "34", "56" ]
```

The method `<str>.search(<regexp>)` returns the position of the first match or `-1` if none found. `search` only finds the first match:

```js
const str = "A drop of ink may make a million think";

console.log(str.search(/ink/i)); // 10 (first match position
```

<hr>

### Summary of Regular Expressions

Here is a brief summary of some concepts in the regular expressions:

```js
const shortStr = "This is a short text.";
const longStr = `Here is a long text.
This is a multiline one.
It has numbers "like" 123 or 45678, also numbers with "symbols" +1-234-4567-89-01.
It has a lot more "symbols such as" [ ] ( ) * & $ ! @.`;

// Simple match with all the details that could be access through the result
console.log(longStr.match(/is/)); // Array [ "is" ]

console.log(Array.isArray(longStr.match(/is/))); // true, the result of `match` comes as an array, if there's a match
console.log(longStr.match(/no match/)); // returns null, if there's no match

console.log(longStr.match(/is/)[0]); // is
console.log(longStr.match(/is/).length); // 1, the number of matches
console.log(longStr.match(/is/).index); // 5, the position of the matched string in the source string
console.log(longStr.match(/is/).input); // the source string, where the search happens

console.log(longStr.match(/is/g)); // Array(3) [ "is", "is", "is" ], flag `g` returns all matches
console.log(longStr.match(/is/g).length); // 3
console.log(longStr.match(/is/g).index); // undefined, with the `g` flag, `match` doesn't return additional details about the match
console.log(longStr.match(/is/g).input); // undefined, with the `g` flag, `match` doesn't return additional details about the match

console.log(longStr.matchAll(/is/g)); // `matchAll` mustbe called with the flag `g`
const matchAllArr = Array.from(longStr.matchAll(/is/g)); // `matchAll` returns an iterable object, we can convert it to an array, if we are going to iterate through it more than once
console.log(matchAllArr); // Array(3) [ (1) […], (1) […], (1) […] ]
console.log(matchAllArr.length); // 3

// `matchAll` has access to additional details for all the matches
console.log(matchAllArr[0].length); // 1, the number of matches in the array for the first match, same as `longStr.match(/is/).length`
console.log(matchAllArr[0].index); // 5, the position of the first matched string in the source string, same as `longStr.match(/is/).index`
console.log(matchAllArr[0].input); // the source string, where the search happens, same as `longStr.match(/is/).input`

console.log(longStr.matchAll(/no match/g)); // returns an empty iterable object, if there's no match

console.log(longStr.match(/it/g)); // Array [ "it" ], the "it" is from "...with..." in the source
console.log(longStr.match(/it/gi)); // Array(3) [ "It", "it", "It" ], flag `i` makes the search case-insensitive

console.log(/it/i.test(longStr)); // true, returns true on the first match
console.log(/no match/i.test(longStr)); // false, returns false if no match

console.log(/it/gi.test(longStr)); // true, flag `g` doesn't matter with `test`, as it returns true on the first match

console.log(shortStr.replace("short", "very short")); // This is a very short text. `replace` could be used with a simple string
console.log(shortStr.replace(/short/, "very short")); // This is a very short text. `replace` could be used with regexp

console.log(shortStr.replace(/short/, "very $&")); // This is a very short text. `$&` is the matched string
console.log(shortStr.replace(/short/, "...hapchi... I said, $`short")); // This is a ...hapchi... I said, This is a short text. `$`` is the string before the matched string.
console.log(shortStr.replace(/short/, "$'")); // This is a  text. text. `$'` is the string after the matched string.
console.log(shortStr.replace(/short/, "$$")); // This is a $ text. `$$` is $.

console.log(shortStr.replace(/(This) (is)/, "$2 $1")); // is This a short text. `$1` is (This) and `$2` is (is).
console.log(
  shortStr.replace(
    /(?<firstWord>This) (?<secondWord>is)/,
    "$<secondWord> $<firstWord>",
  ),
); // is This a short text. `$<firstWord>` is (This) and `$<secondWord>` is (is).

// `replace` accepts a function whose return value will be used as a replacement
console.log(
  "A\nB\nC".replace(/A/, function (match, offset, string) {
    return `Return from func: match: ${match}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A, offset: 0, input string: A
B
C. The End.
B
C */

// matching string, capturing groups, the offset of the position of the match from the beginning of the source string, and the source string itself could be accessed
console.log(
  "A\nB\nC".replace(/(A)/, function (match, p1, offset, string) {
    return `Return from func: match: ${match}, capturing group: ${p1}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A, capturing group: A, offset: 0, input string: A
B
C. The End.
B
C */

// the more capturing groups are accessed between match and offset parameters
console.log(
  "A\nB\nC".replace(/(A)\n(B)/, function (match, p1, p2, offset, string) {
    return `Return from func: match: ${match}, capturing group 1: ${p1}, capturing group 2: ${p2}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A
B, capturing group 1: A, capturing group 2: B, offset: 0, input string: A
B
C. The End.
C */

console.log(shortStr.replaceAll(/is/g, "IS")); // ThIS IS a short text. `replaceAll` must be used with the flag `g`
console.log(shortStr.replace(/is/g, "IS")); // ThIS IS a short text, `replace` with the flag `g` is the same as `replaceAll`

console.log(longStr.match(/\d/)); // Array [ "1" ], `\d` returns digits
console.log(longStr.match(/\D/)); // Array [ "H" ], `\d` returns non-digits

console.log(longStr.match(/\s/)); // Array [ " " ], `\d` returns spaces
console.log(longStr.match(/\S/)); // Array [ "H" ], `\d` returns non-spaces

console.log(longStr.match(/\w/)); // Array [ "H" ], `\d` returns wordly characters
console.log(longStr.match(/\W/)); // Array [ " " ], `\d` returns non-wordly characters

console.log(longStr.match(/./g)); // matches any character except the newline
console.log(longStr.match(/./gs)); // with flag `s`, `.` matches the newline character as well

console.log(longStr.match(/^Here/gi)); // Array [ "Here" ], `^` anchor searches the beginning of a string
console.log(longStr.match(/\.$/gi)); // Array [ "." ], `$` anchor searches the end of a string

console.log(longStr.match(/^It/gim)); // Array [ "It", "It" ], `^` with the flag `m` searches the beggining of every line
console.log(longStr.match(/\.$/gim)); // Array(4) [ ".", ".", ".", "." ], `$` with the flag `m` searches the end of every line

console.log(longStr.match(/it/gi)); // Array(3) [ "It", "it", "It" ], the second "it" is from "...with..." in the source
console.log(longStr.match(/\bit\b/gi)); // Array [ "It", "It" ], `\b` means a word boundary, a non-`\w` character

console.log(longStr.match(/\b[Ii]t\b/g)); // Array [ "It", "It" ], `[Ii ]` means one of I or i
console.log(longStr.match(/\bit\b/g)); // null

console.log(longStr.match(/\b[^Ii]t\b/g)); // null, `[^Ii ]` means any character other than I or i

console.log(longStr.match(/\d{3}/g)); // Array(3) [ "123", "234", "456" ], `\d{3}` is the same as \d\d\d
console.log(longStr.match(/\d{3,}/g)); // Array(3) [ "123", "234", "4567" ], `\d{3,}` means 3 or more digits
console.log(longStr.match(/\d{4,5}/g)); // Array [ "45678", "4567" ], `\d{4,5}` means 4 or 5 digits

console.log(longStr.match(/\d+/g)); // Array(7) [ "123", "45678", "1", "234", "4567", "89", "01" ], `+` means {1,}
console.log(longStr.match(/4\d?/g)); // Array(3) [ "45", "4", "45" ], `?` means {0,1}
console.log(longStr.match(/4\d*/g)); // Array(3) [ "45678", "4", "4567" ], `*` means {0,}

console.log(longStr.match(/".+?"/gi)); // Array(3) [ '"like"', '"symbols"', '"symbols such as"' ], +? turns on the lazy mode for +
console.log(longStr.match(/".??"/gi)); // null, ?? turns on the lazy mode for ?
console.log(longStr.match(/".*?"/gi)); // Array(3) [ '"like"', '"symbols"', '"symbols such as"' ], +? turns on the lazy mode for *

// match
// matchAll
// test
// replace
// replaceAll

// g
// i
// s
// u
// m
// y

// $&
// $`
// $'
// $$
// $group_number
// $<group_name>

// \d
// \s
// \w

// \D
// \S
// \W

// .

// ^
// $
// \b

// [ ]
// [^ ]

// {<number>}
// {<number>,}
// {<lower_limit_number>,<upper_limit_number>}
// + same as {1,}
// ? same as {0,1}
// * same as {0,}

// +?
// *?
// ??

// ( )
// ( ( ) ( ) )
// (?: )

// (?<group_name>)
// (\group_number)
// (\k<group_name)

// |
// ( | )

// (?=)
// (?!)
// (?<=)
// (?<!)

// (?=( ))

// \d++
// \w++

// exec with lastIndex and flag y
```

<hr>
<hr>

## URL

### Creating a `URL` object

The built-in `URL` class provides a convenient interface for creating and parsing URLs. The syntax to create a new URL object is `new URL(<url>, [<base>])`

- `<url>` – the full URL or only path (if `<base>` is set),
- `<base>` – an optional base URL: if set and `<url>` argument has only path, then the URL is generated relative to base.

```js
const url = new URL("https://example.com/path/to/folder");

console.log(url.href); // https://example.com/path/to/folder
```

```js
const url = new URL("path/to/folder", "https://example.com");

console.log(url.href); // https://example.com/path/to/folder
```

We can easily create a new `URL` based on the path relative to an existing URL:

```js
const url = new URL("https://example.com/path/to/folder");
const newUrl = new URL("newPath", url);

console.log(newUrl.href); // 'https://example.com/path/to/newPath'
```

<hr>

### Properties of a `URL` object

The `URL` object has a lot of properties that inform us about the url.

```js
const url = "https://example.org:8080/foo/bar?q=baz#bang";
const newUrl = new URL(url);

console.log("protocol: ", newUrl.protocol); // protocol:  https:
console.log("hostname: ", newUrl.hostname); // hostname:  example.org
console.log("port: ", newUrl.port); // port:  8080
console.log("host: ", newUrl.host); // host:  example.org:8080
console.log("origin: ", newUrl.origin); // origin:  https://example.org:8080
console.log("pathname: ", newUrl.pathname); // pathname:  /foo/bar
console.log("search: ", newUrl.search); // search:  ?q=baz
console.log("hash: ", newUrl.hash); // hash:  #bang
console.log("href: ", newUrl.href); // href:  https://example.org:8080/foo/bar?q=baz#bang
console.log("toString(): ", newUrl.toString()); // toString():  https://example.org:8080/foo/bar?q=baz#bang
console.log("toJSON(): ", newUrl.toJSON()); // toJSON():  https://example.org:8080/foo/bar?q=baz#bang
```

Generally, the `URL` object can be passed to any method (for example, `fetch`) instead of a string, as most methods will perform the string conversion, that turns a `URL` object into a string with full URL.

<hr>

### `URLSearchParams`

If we want to add search parameters to a url, we can add it into a url string. However, we can also use `<url>.searchParams`, an object of type `URLSearchParams`. It provides convenient methods for search parameters:

- `append(<name>, <value>)` – add the parameter by name,
- `delete(<name>)` – remove the parameter by name,
- `get(<name>)` – get the parameter by name,
- `getAll(<name>)` – get all parameters with the same name (that’s possible, e.g. `?user=John&user=Pete`),
- `has(<name>)` – check for the existence of the parameter by name,
- `set(<name>, <value>)` – set/replace the parameter,
- `sort()` – sort parameters by name,
- …and it’s also iterable, similar to `Map`.

```js
const url = new URL("https://example.org:8080/query?q1=value1");
console.log(url.search); // ?q1=value1

url.searchParams.append("q2", "value2.1");
console.log(url.search); // ?q1=value1&q2=value2.1

url.searchParams.delete("q2");
console.log(url.search); // ?q1=value1

console.log(url.searchParams.has("q1")); // true
console.log(url.searchParams.has("q2")); // false

url.searchParams.set("q2", "value2.1");
url.searchParams.append("q2", "value2.2");

console.log(url.searchParams.get("q1")); // value1
console.log(url.searchParams.getAll("q2")); // Array [ "value2.1", "value2.2" ]
```

The reason why using `URLSearchParams` could be better is because search parameters need to be encoded if they contain spaces, non-latin letters, etc. If we are manually adding a search parameter to a url string, then we would also need to add the encoding for some characters.

```js
const url = new URL("https://example.com/query");

url.searchParams.set("queryKey", "query value!"); // added parameter with a space and !
console.log(url.href); // https://example.com/query?queryKey=query+value%21

url.searchParams.set("queryKey", "query:value"); // added parameter with a colon :
// parameters are automatically encoded
console.log(url.href); // https://example.com/query?queryKey=query%3Avalue

console.log(url.searchParams); // URLSearchParams { queryKey → "query:value" }

// iterate over search parameters (decoded)
for (let [name, value] of url.searchParams) {
  console.log(`${name}=${value}`); // queryKey=query:value
}
```

There’s a standard RFC3986 that defines which characters are allowed in URLs and which are not. The good news is that `URL` objects handle all of that automatically:

```js
const url = new URL("https://example.az/ƏÜĞ");

url.searchParams.set("key", "Ç");

// url is automatically encoded
console.log(url.href); // https://example.az/%C6%8F%C3%9C%C4%9E?key=%C3%87
console.log(url.searchParams); // URLSearchParams { key → "Ç" }
```

<hr>

### Functions for encoding and decoding url and url components

Even though `new URL` and `URLSearchParams` are convenient for encoding and decoding, we might need to add a url as a string at some point. If we use a string though, we need to encode/decode special characters manually. There are built-in functions for that:

- `encodeURI` – encodes URL as a whole.
- `decodeURI` – decodes it back.
- `encodeURIComponent` – encodes a URL component, such as a search parameter, or a hash, or a pathname.
- `decodeURIComponent` – decodes it back.

What’s the difference between `encodeURIComponent` and `encodeURI`? When we should use either? There are characters that are allowed in the whole URL, but they need to be encoded when it's part of some URL component such as a search parameter. For example, characters such as `:`, `?`, `=`, `&`, `#` are allowed in URL but they have a special meaning as part of some URL components.

- `encodeURI` encodes only characters that are totally forbidden in URL.
- `encodeURIComponent` encodes same characters, and, in addition to them, characters `#`, `$`, `&`, `+`, `,`, `/`, `:`, `;`, `=`, `?` and `@`.

```js
const param = encodeURIComponent("test1&test2");
const url = `https://example.com/?q=${param}`;

console.log(url); // 'https://example.com/?q=test1%26test2'
```

```js
const param = encodeURI("test1&test2");
const url = `https://example.com/?q=${param}`;

console.log(url); // 'https://example.com/?q=test1&test2'
```

There are cases where `encodeURI*` functions will not work. Classes `URL` and `URLSearchParams` are based on the latest URI specification: RFC3986, while `encodeURI*` functions are based on the obsolete version RFC2396. There are a few differences, e.g. IPv6 addresses are encoded wrong with `encodeURI`:

```js
// valid url with IPv6 address
const url = "http://[2607:f8b0:4005:802::1007]/";

console.log(encodeURI(url)); // http://%5B2607:f8b0:4005:802::1007%5D/
console.log(new URL(url).href); // http://[2607:f8b0:4005:802::1007]/
```

<hr>

### `createObjectURL()` and `revokeObjectURL()`

There are 2 static methods in the URL constructor. It has the `createObjectURL()` method and the `revokeObjectURL()` method. The `createObjectURL()` static method creates a `DOMString` containing a URL representing the object given in the parameter. A `DOMString` is a UTF-16 encoded string. Since JavaScript uses UTF-16 strings, `DOMString`s are mapped directly to strings. The `createObbjectURL()` method accepts an object, which can be a `File`, `Blob`, or `MediaSource` object to create a URL for.

```js
const objUrl = URL.createObjectURL(new File([""], "filename"));
console.log(objUrl); // blob:http://...
```

The browsers will release object `URL`s automatically when the document is unloaded, but for the sake of improving performance, we should release it manually. The `revokeObjectURL()` method takes in an object `URL` as its argument.

```js
const objUrl = URL.createObjectURL(new File([""], "filename"));
console.log(objUrl); // blob:http://...

URL.revokeObjectURL(objUrl); // returns undefined
```

Here is an example, where we receive an image from a server, turn it into a url and show as an image:

```js
fetch("https://picsum.photos/400/400")
  .then((res) => res.blob())
  .then((blob) => handler(blob));

function handler(blob) {
  const url = URL.createObjectURL(blob);

  const img = new Image();
  img.src = url;

  img.onload = () => {
    document.body.appendChild(img);
    URL.revokeObjectURL(url);
  };
}
```

<hr>
<hr>

## Binary files

### `ArrayBuffer`

`ArrayBuffer` is a JavaScript constructor that can be used to allocate a specific number of
bytes in memory. It is an array of bytes. `ArrayBuffer` is the chunk of memory that is set aside to hold typed arrays (`Int8Array`, `UInt8Array` etc). The syntax to create an `ArrayBuffer` is `new ArrayBuffer(<bytes>)`:

```js
const buffer = new ArrayBuffer(16); // create a buffer of length of 16 bytes
console.log(buffer.byteLength); // 16
```

This allocates a contiguous memory area of 16 bytes and pre-fills it with zeroes.

Let’s eliminate a possible source of confusion. `ArrayBuffer` is not `Array`:

- It has a fixed length, we can’t increase or decrease it.
- It takes exactly that much space in the memory.
- To access individual bytes, another “view” object is needed, not `<buffer>[<index>]`.

<hr>

#### Typed Arrays

We cannot interact with the `ArrayBuffer` directly. To manipulate an `ArrayBuffer`, we need to use a view object. A view object does not store anything on its own. It’s the “eyeglasses” that give an interpretation of the bytes stored in the `ArrayBuffer`.

```js
const buffer = new ArrayBuffer(16); // create a buffer of length of 16 bytes, 8-bit (1 byte) * 16 bytes = 128 bits

const view = new Uint32Array(buffer); // view the buffer as a sequence of 32-bit integers

console.log(Uint32Array.BYTES_PER_ELEMENT); // 16 bytes / 32 bits = 128 bits / 32 bits = 4 bytes per integer

console.log(view.length); // 4, it stores that many integers
console.log(view.byteLength); // 16, the size in bytes

// let's write a value
view[0] = 123456;

// iterate over values
for (let num of view) {
  console.log(num); // 123456, then 0, 0, 0 (4 values total)
}

// use the spread operator with a typed array
console.log(...view); // 123456 0 0 0
```

The common term for all these views (`Uint8Array`, `Uint32Array`, etc) is **typed array**. Please note, there’s no constructor called TypedArray, it’s just a common “umbrella” term to represent one of views over `ArrayBuffer`: `Int8Array`, `Uint8Array` and so on. Typed arrays behave like regular arrays: have indexes and are iterable.

There are various typed arrays:

- `Int8Array` - is an array of 8-bit integers. These integers can be in the range of -128 to 127.
- `UInt8Array` (unsigned array) - is an array of 8-bit integers. These integers can be in the range of 0 to 255.
- `UInt8ClampedArray` (unsigned and clamped array) - is an array of 8-bit integers. These integers can be in the range of 0 to 255. Clamped means that if you try to put a number less than 0, it will be converted to 0. If you try to put a number greater than 255, it will be converted to 255.
- `Int16Array` - is an array of 16-bit integers. These integers can be in the range of -32768 to 32767.
- `UInt16Array` (unsigned array) - is an array of 16-bit integers. These integers can be in the range of 0 to 65535.
- `Int32Array` - is an array of 32-bit integers. These integers can be in the range of -2147483648 to 2147483647.
- `UInt32Array` (unsigned array) - is an array of 32-bit integers. These integers can be in the range of 0 to 4294967295.
- `Float32Array` - for signed floating-point numbers of 32. It treats every 4 bytes as a floating point number.
- `Float64Array` - for signed floating-point numbers of 64 bits. It treats every 8 bytes as a floating point number with possible values from 5.0x10^-324 to 1.8x10^308.

A typed array constructor (be it `Int8Array` or `Float64Array`, doesn’t matter) behaves differently depending on argument types. There are 5 variants of arguments:

```js
new <TypedArray>(<buffer>, [<byteOffset>, <length>]);
new <TypedArray>(<object>);
new <TypedArray>(<typedArray>);
new <TypedArray>(<length>);
new <TypedArray>();
```

- If an `<ArrayBuffer>` argument is supplied, the view is created over it.
  - Optionally, we can provide `<byteOffset>` to start from (0 by default) and the `<length>` (till the end of the buffer by default), then the view will cover only a part of the buffer.
- If an Array, or any array-like object is given, it creates a typed array of the same length and copies the content. We can use it to pre-fill the array with the data:

```js
const arr = new Uint8Array([0, 1, 2, 3]);
console.log(arr.length); // 4, created binary array of the same length
console.log(arr[1]); // 1, filled with 4 bytes (unsigned 8-bit integers) with given values
```

- If another typed array is supplied, it does the same: creates a typed array of the same length and copies values. Values are converted to the new type in the process, if needed.

```js
const arr16 = new Uint16Array([1, 1000]);
const arr8 = new Uint8Array(arr16);
console.log(arr8[0]); // 1
console.log(arr8[1]); // 232, tried to copy 1000, but can't fit 1000 into 8 bits
```

- For a numeric argument length – creates the typed array to contain that many elements. Its byte length will be length multiplied by the number of bytes in a single item `<TypedArray>.BYTES_PER_ELEMENT`:

```js
const arr = new Uint16Array(4); // create typed array for 4 integers, 4 * 16-bit = 64-bit
console.log(Uint16Array.BYTES_PER_ELEMENT); // 2 bytes per integer, 2 bytes = 16-bit = 1 integer
console.log(arr.byteLength); // 8 (size in bytes), 4 integers - 64-bit, 64 / 8-bit(1 byte) = 8 bytes
```

- Without arguments, creates a zero-length typed array.

We can create a typed array directly, without mentioning `ArrayBuffer`. But a view cannot exist without an underlying `ArrayBuffer`, so it gets created automatically in all these cases except the first one (when provided).

- To access the underlying `ArrayBuffer`, there are following properties in TypedArray:
  - `buffer` – references the `ArrayBuffer`.
  - `byteLength` – the length of the `ArrayBuffer`.

This lets us to move from one view to another easily:

```js
const arr8 = new Uint8Array([0, 1, 2, 3]);

// another view on the same data
const arr16 = new Uint16Array(arr8.buffer);
```

<hr>

#### Typed Array Methods

Typed arrays have regular `Array` methods, with notable exceptions. We can iterate with `map`, `slice`, `find`, `reduce` etc.

There are few things we can’t do though:

- No `splice` – we can’t “delete” a value, because typed arrays are views on a buffer, and these are fixed, contiguous areas of memory. All we can do is to assign a zero.
- No `concat` method.

There are two additional methods that typed arrays have:

- `<typedArray>.set(<fromArr>, [<offset>])` copies all elements from `<fromArr>` to the `<typedArray>`, starting at position `<offset>` (0 by default).
- `<typedArray>.subarray([<begin>, <end>])` creates a new view of the same type from `<begin>` to `<end>` (exclusive). That’s similar to `slice` method, but doesn’t copy anything – just creates a new view, to operate on the given piece of data.

<hr>

#### `DataView`

`DataView` is a special super-flexible “untyped” view over `ArrayBuffer`. It allows to access the data on any offset in any format. `DataView` is great when we store mixed-format data in the same buffer.

- For typed arrays, the constructor dictates what the format is. The whole array is supposed to be uniform. The i-th number is `<arr>[<i>]`.
- With `DataView` we access the data with methods like `.getUint8(<i>)` or `.getUint16(<i>)`. We choose the format at method call time instead of the construction time. We also set the data with methods like `setUint8()`, `setUint16()`, etc.

The syntax is `new DataView(<buffer>, [<byteOffset>], [<byteLength>])`.

- `<buffer>` – the underlying `ArrayBuffer`. Unlike typed arrays, `DataView` doesn’t create a buffer on its own. We need to have it ready.
- `<byteOffset>` – the starting byte position of the view (by default 0).
- `<byteLength>` – the byte length of the view (by default till the end of buffer).

```js
// binary array of 4 bytes, all have the maximal value 255
const buffer = new Uint8Array([255, 255, 255, 255]).buffer;

const dataView = new DataView(buffer);

// get 8-bit number at offset 0
console.log(dataView.getUint8(0)); // 255

// now get 16-bit number at offset 0, it consists of 2 bytes, together interpreted as 65535
console.log(dataView.getUint16(0)); // 65535 (biggest 16-bit unsigned int)

// get 32-bit number at offset 0
console.log(dataView.getUint32(0)); // 4294967295 (biggest 32-bit unsigned int)

dataView.setUint32(0, 0); // set 4-byte number to zero, thus setting all bytes to 0
```

<hr>

### `TextDecoder` and `TextEncoder`

#### `TextDecoder`

What if the binary data is actually a string? The built-in `TextDecoder` object allows one to read the value into an actual JavaScript string, given the buffer and the encoding.

- We first need to create it with `new TextDecoder([<encoding>], [<options>])`
  - `<encoding>` – `utf-8` by default, but `big5`, `windows-1251` and others are also supported.
  - `<options>` – optional object:
    - `fatal` – boolean, if `true` then throw an exception for invalid (non-decodable) characters, otherwise (default) replace them with character \uFFFD.
    - `ignoreBOM` – boolean, if `true` then ignore BOM (an optional byte-order Unicode mark), rarely needed.

- After creating the `TextDecoder`, we can decode with `.decode([<input>], [<options>])`
  - `<input>` – BufferSource to decode.
  - `<options>` – optional object:
    - `stream` – true for decoding streams, when decoder is called repeatedly with incoming chunks of data. In that case a multi-byte character may occasionally split between chunks. This option tells `TextDecoder` to memorize “unfinished” characters and decode them when the next chunk comes.

```js
const uint8Array = new Uint8Array([72, 101, 108, 108, 111]);
console.log(new TextDecoder().decode(uint8Array)); // Hello
```

We can decode a part of the buffer by creating a subarray view for it:

```js
const uint8Array = new Uint8Array([0, 72, 101, 108, 108, 111, 0]);

// the string is in the middle
// create a new view over it, without copying anything
const binaryString = uint8Array.subarray(1, -1);

console.log(new TextDecoder().decode(binaryString)); // Hello
```

<hr>

#### `TextEncoder`

`TextEncoder` does the reverse thing – converts a string into bytes. The syntax is `new TextEncoder()`. The only encoding it supports is “utf-8”. It has two methods:

- `encode(<str>)` – returns `Uint8Array` from a string.
- `encodeInto(<str>, <destination>)` – encodes `<str>` into `<destination>` that must be `Uint8Array`.

```js
const encoder = new TextEncoder();

const uint8Array = encoder.encode("Hello");
console.log(uint8Array); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]

console.log(new TextDecoder().decode(uint8Array)); // Hello
```

<hr>

### Blob

`ArrayBuffer` and views are parts of ECMA standard, parts of JavaScript. In the browser, there are additional higher-level objects, described in the File API, in particular `Blob`. Blob stands for Binary Large Object. It's basically any binary file.

The constructor syntax is `new Blob(<blobParts>, <options>);`

- `<blobParts>` is an array of Blob/BufferSource/String values. The first argument to `Blob` must be an array.
- `<options>` optional object:
  - `type` – Blob type, usually MIME-type, e.g. image/png, text/plain, etc.
  - `endings` – whether to transform end-of-line to make the Blob correspond to current OS newlines (\r\n or \n). By default `"transparent"` (do nothing), but also can be `"native"` (transform).

```js
// create Blob from a typed array and strings
const helloArr = new Uint8Array([72, 101, 108, 108, 111]); // "Hello" in binary form

const blob = new Blob([helloArr, " ", "world"], { type: "text/plain" });

console.log(helloArr); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]
console.log(blob); // Blob { size: 11, type: "text/plain"
```

We can’t change data directly in a Blob, but we can slice parts of a Blob, create new Blob objects from them, mix them into a new Blob and so on. This behavior is similar to JavaScript strings: we can’t change a character in a string, but we can make a new corrected string.

We can extract Blob slices with `<blob>.slice([<byteStart>], [<byteEnd>], [<contentType>]);`

- `<byteStart>` – the starting byte, by default 0.
- `<byteEnd>` – the last byte (exclusive, by default till the end).
- `<contentType>` – the type of the new blob, by default the same as the source.

The arguments are similar to `<array>.slice`, negative numbers are allowed too.

The `Blob` constructor allows to create a blob from almost anything, including any BufferSource. If we need to perform low-level processing, we can get the lowest-level `ArrayBuffer` from `<blob>.arrayBuffer()`.

#### Downloading Blobs

We can download/upload Blob objects, and the `type` naturally becomes `Content-Type` in network requests. A Blob can also be easily used as a URL for `<a>`, `<img>` or other tags, to show its contents.

```html
<!-- download attribute forces the browser to download instead of navigating -->
<a download="hello.txt" href="#" id="link">Download and Clear the Link</a>

<script>
  const blob = new Blob(["Hello, world!"], { type: "text/plain" });

  // URL.createObjectURL takes a Blob and creates a unique URL for it, in the form blob:<origin>/<uuid>.
  link.href = URL.createObjectURL(blob);

  link.addEventListener("click", function () {
    URL.revokeObjectURL(link.href); // will download and then revoke the URL, won't be able to download in the next click
  });
</script>
```

An alternative to `URL.createObjectURL` is to convert a Blob into a base64-encoded string. That encoding represents binary data as a string of ultra-safe “readable” characters with ASCII-codes from 0 to 64. And what’s more important – we can use this encoding in “data-urls”. A data url has the form `data:[<mediatype>][;base64],<data>`. We can use such urls everywhere, on par with “regular” urls.

To transform a Blob into base64, we’ll use the built-in `FileReader` object. It can read data from Blobs in multiple formats.

```js
const link = document.createElement("a");
link.download = "hello.txt";

const blob = new Blob(["Hello, world!"], { type: "text/plain" });

const reader = new FileReader();
reader.readAsDataURL(blob); // converts the blob to base64 and calls onload

reader.onload = function () {
  link.href = reader.result; // data url
  link.click();
};
```

By using a Blob with the `URL.createObjectURL(<blob>)` option we need to revoke the blob to free up the memory. Using a Blob with this "Blob to data url" option, we might have performance and memory losses on big `Blob` objects for encoding.

<hr>

### File and FileReader

#### `File`

A `File` object inherits from `Blob` and is extended with filesystem-related capabilities. As `File` inherits from `Blob`, `File` objects have the same properties, plus:

- `name` – the file name,
- `lastModified` – the timestamp of last modification.

There are two ways to obtain it.

- First, there’s a constructor, similar to `Blob`: `new File(<fileParts>, <fileName>, [<options>])`
  - `<fileParts>` – is an array of Blob/BufferSource/String values.
  - `<fileName>` – file name string.
  - `<options>` – optional object:
    - `lastModified` – if `true`, the timestamp (integer date) of last modification.
- Second, more often we get a file from `<input type="file">` or "drag and drop" or other browser interfaces. In that case, the file gets this information from OS.
  - The input may select multiple files. The `<input>.files` is an array-like object with them.

```js
<input type="file" onchange="showFile(this)">

<script>
function showFile(input) {
  const file = input.files[0];

  console.log(`File name: ${file.name}`);
  console.log(`Last modified: ${file.lastModified}`);
  console.log(input.files); // FileList [ File ]
}
</script>
```

<hr>

#### `FileReader`

`FileReader` is an object with the sole purpose of reading data from a `Blob` (and hence `File` too). The syntax is

```js
const reader = new FileReader(); // no arguments
```

The main methods:

- `readAsArrayBuffer(<blob>)` – read the data in binary format `ArrayBuffer`.
  - This is for binary files, to do low-level binary operations.
- `readAsText(<blob>, [<encoding>])` – read the data as a text string with the given encoding (`utf-8` by default).
  - This is for text files, when we’d like to get a string.
- `readAsDataURL(<blob>)` – read the binary data and encode it as base64 data url.
  - This can be used when we’d like to use this data in `src` for `img` or another tag. We can also use `URL.createObjectURL()`.
- `abort()` – cancel the operation.

As the reading proceeds, there are events:

- `loadstart` – loading started.
- `progress` – occurs during reading.
- `load` – no errors, reading complete.
- `abort` – `abort()` called.
- `error` – error has occurred.
- `loadend` – reading finished with either success or failure.

When the reading is finished, we can access the result as:

- `reader.result` is the result (if successful)
- `reader.error` is the error (if failed).

Here is an example of reading a text file with `readAsText()` method:

```html
<input type="file" onchange="readFile(this)" />

<script>
  function readFile(input) {
    const file = input.files[0];

    const reader = new FileReader();

    reader.readAsText(file);

    reader.onload = function () {
      console.log(reader.result);
    };

    reader.onerror = function () {
      console.log(reader.error);
    };
  }
</script>
```

Here is an example of reading an image file with `readAsDataURL()` method, attaching it a page, and sending it to a server as a `Blob`:

```html
<input type="file" />
<div id="preview"></div>

<script>
  const fileInput = document.querySelector("input");
  const preview = document.getElementById("preview");

  fileInput.addEventListener("change", () => {
    const fileReader = new FileReader();

    fileReader.readAsDataURL(fileInput.files[0]);

    fileReader.addEventListener("load", () => {
      const url = fileReader.result;
      // console.log(url)

      const img = new Image();
      img.src = url;
      // preview.appendChild(img)

      img.onload = () => {
        const canvas = document.createElement("canvas");
        const ctx = canvas.getContext("2d");
        canvas.width = img.width;
        canvas.height = img.height;

        ctx.drawImage(img, 0, 0);
        preview.appendChild(canvas);

        canvas.toBlob((blob) => {
          const formData = new FormData();
          formData.append("img", blob, "img.png");

          fetch("https://httpbin.org/post", {
            method: "POST",
            body: formData,
          })
            .then((res) => res.json())
            .then((res) => console.log(res));
        });
      };
    });
  });
</script>
```

The `error` event fires if the file cannot be read for some reason. When the `error` event fires, the `error` property of the `FileReader` is filled in. This object has a single property, `code`, which can have an error code of

- 1 - file not found
- 2 - security error
- 3 - read was aborted
- 4 - file isn’t readable
- 5 - encoding error

<hr>

### Summary of Binary Files

Here is the brief summary of above concepts about binary files:

```js
// create an array buffer
const buffer = new ArrayBuffer(4); // create an array buffer - binary data - of 4 bytes

console.log(buffer); // 4
console.log(buffer.byteLength); // 4

// create an 8-bit view over the buffer
const view8 = new Int8Array(buffer);

// the view of the buffer when all the bytes are viewed as separate 8-bit entities
console.log(view8); // Int8Array(4) [ 0, 0, 0, 0 ]
console.log(view8.byteLength); // 4
console.log(view8.byteOffset); // 0
console.log(view8.BYTES_PER_ELEMENT); // 1
console.log(view8.length); // 4, byteLength / BYTES_PER_ELEMENT

// create an 8-bit view over the buffer by offsetting 1 byte
console.log(new Int8Array(buffer, 1)); // Int8Array(3) [ 0, 0, 0 ], byteOffset is 1
console.log(new Int8Array(buffer, 1).byteOffset); // byteOffset is 1, so the view of the buffer starts after offsetting 1 byte

// create an 8-bit view over the buffer by offsetting 2 bytes and having 2 byte-length
console.log(new Int8Array(buffer, 2, 2)); // Int8Array [ 0, 0 ], byteOffset is 2 and the length is 2
console.log(new Int8Array(buffer, 2, 2).byteLength); // 2
console.log(new Int8Array(buffer, 2, 2).byteOffset); // 2
console.log(new Int8Array(buffer, 2, 2).length); // 2

// create a 16-bit view over the buffer
const view16 = new Uint16Array(buffer);

console.log(view16); // Uint16Array [ 0, 0 ]
console.log(view16.byteLength); // 4
console.log(view16.BYTES_PER_ELEMENT); // 2
console.log(view16.length); // 2, byteLength / BYTES_PER_ELEMENT

// set the 0th position to 45
view16[0] = 45;
console.log(view16); // Uint16Array [ 45, 0 ]
console.log(view8); // Int8Array(4) [ 45, 0, 0, 0 ]
console.log(new Int8Array(buffer, 1)); // Int8Array(3) [ 0, 0, 0 ], byteOffset is 1, so 1 byte (which now holds the value of 45) is skipped

// iterate over the 8-bit view of the buffer
for (let num of view8) {
  console.log(num); // 45, 0, 0, 0
}

// create a 32-bit view over the buffer
const view32 = new Uint32Array(buffer);
console.log(view32); // Uint32Array [ 45 ]

// create a view and an array buffer at the same time
const view16_2 = new Uint16Array([1, 2, 3, 4]); // Array buffer created automatically
console.log(view16_2); // Uint16Array(4) [ 1, 2, 3, 4 ]

// create a view using another view
const view16_3 = new Uint16Array([1, 2, 3, 4]);
const view8_2 = new Uint8Array(view16_3);

// create a view using the buffer of another view
const view32_2 = new Uint32Array(view16_3.buffer);

console.log(view16_3); // Uint16Array(4) [ 1, 2, 3, 4 ]
console.log(view8_2); // Uint8Array(4) [ 1, 2, 3, 4 ]
console.log(view32_2); // Uint32Array [ 131073, 262147 ]

// create a view specifying only the length - the number of elements
console.log(new Uint8Array(2)); // Uint8Array [ 0, 0 ]

// create a view without specifying only the length - the number of elements
console.log(new Float32Array()); // Float32Array []

// set the existing view `Uint8Array(4) [ 1, 2, 3, 4 ]` to have elements 5, 6
view8_2.set([5, 6]);
console.log(view8_2); // Uint8Array(4) [ 5, 6, 3, 4 ]

// set the existing view to have elements 7, 8 starting from position 1
view8_2.set([7, 8], 1);
console.log(view8_2); // Uint8Array(4) [ 5, 7, 8, 4 ]

// create the copy of view8_2 from position 1 till 3 (exclusive)
const view8_3 = view8_2.subarray(1, 3);
console.log(view8_3); // Uint8Array [ 7, 8 ]

// Create a DataView over the buffer
const dataView = new DataView(buffer);

// log the items in the dataView in the positions 0, 1, 2
console.log(dataView.getUint8(0)); // 45
console.log(dataView.getUint8(1)); // 0
console.log(dataView.getUint8(2)); // 0

// Create a DataView over the buffer with offsetting 1 byte, and having length 2
const dataView2 = new DataView(buffer, 1, 2);

// log the items in the dataView in the positions 0, 1
console.log(dataView2.getUint8(0)); // 0
console.log(dataView2.getUint8(1)); // 0

// set the item in the dataView2, position 0 to 10
dataView2.setUint8(0, 10);
console.log(dataView2.getUint8(0)); // 0
console.log(dataView.getUint8(1)); // 0 the item in the dataView in the position 1 is the same as dataView2 position 0

// decode binary data into a string
const view8_4 = new Uint8Array([72, 101, 108, 108, 111]);
console.log(new TextDecoder().decode(view8_4)); // Hello
console.log(new TextDecoder("utf-8").decode(view8_4)); // Hello

// encode a string into binary data
console.log(new TextEncoder().encode("Hello")); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]

// declare a typed array and encode a string into it
const encodedArr = new Uint8Array(6);
new TextEncoder().encodeInto("Hello", encodedArr);
console.log(encodedArr); // Uint8Array(6) [ 72, 101, 108, 108, 111, 0 ]

const blob = new Blob(["Hello"], { type: "text/plain" });
console.log(blob); // Blob { size: 5, type: "text/plain"

blob
  .arrayBuffer()
  .then((b) => {
    console.log(b); // ArrayBuffer { byteLength: 5 }
  })
  .catch((error) => console.error(error));

const blob_2 = new Blob([view8_4], { type: "text/plain" });
console.log(blob_2); // Blob { size: 5, type: "text/plain" }

const url = URL.createObjectURL(blob);
console.log(url); // blob:http...

URL.revokeObjectURL(blob);

const reader = new FileReader();
reader.readAsDataURL(blob_2);

reader.onload = () => {
  console.log(reader.result); // data:text/plain;base64,SGVsbG8=
};

const file = new File(["Hello"], "filename", { type: "text/plain" });
console.log(file); // File { name: "filename", lastModified: 1717209982047, webkitRelativePath: "", size: 5, type: "text/plain" }

// If uploaded from by user using the `input` tag, then can be accessed via <input>.files

const reader2 = new FileReader();

reader2.readAsArrayBuffer(file);
reader2.onload = () => {
  console.log(reader2.result); // ArrayBuffer { byteLength: 5 }
};

const reader3 = new FileReader();

reader3.readAsText(file);
reader3.onload = () => {
  console.log(reader3.result); // Hello
};

const reader4 = new FileReader();

reader4.readAsDataURL(file);
reader4.onload = () => {
  console.log(reader4.result); // data:text/plain;base64,SGVsbG8=
};

const reader5 = new FileReader();

reader5.readAsText(file);

reader5.onloadstart = () => {
  console.log("starting to read as text");
};

reader5.onprogress = () => {
  console.log("progressing to read as text");
};

reader5.onabort = () => {
  console.log("aborted to read as text"); // aborted to read as text
};

reader5.onerror = () => {
  console.log("error while reading as text");
  reader5.error;
};

reader5.onload = () => {
  console.log("loaded the text");
  console.log(reader5.result);
};

reader5.onloadend = () => {
  console.log("ended reading as text"); // ended reading as text
};

reader5.abort();
```

<hr>
<hr>

# Window object

- [Window object](#window-object)
  - [Intro](#intro)
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

---

---

## Intro

A global variable, `window`, represents the window in which the script is running. In a tabbed browser, each tab is represented by its own `Window` object. This object contains many properties and methods that we can use. We don't need to access all of them by prepending `window.`. For example, `document` is part of the `Window` object, and we can access it either using `window.document` or simply `document`.

For a full list of the window properties, go to [MDN Window](https://developer.mozilla.org/en-US/docs/Web/API/Window).

Let's review some properties and methods of this rich object.

---

---

## `window.caches`

`window.caches` is a read-only property that returns the `CacheStorage` object. This object enables functionality such as storing assets for offline use, and generating custom responses to requests.

Because older browsers may not support the functionality of `caches`, it is good practice to check for its availability before attempting to reference it. The `caches` property is available on the `window` object and we can check that it is implemented in the browser with this snippet:

```js
if ("caches" in window) {
  // your code
}
```

### Create a new cache with `window.caches.open`

Use `window.caches.open(<name_of_cache>)` to obtain a `Cache` instance. The `Cache` interface provides methods for a persistent storage mechanism for `Request` / `Response` object pairs that are cached in long lived memory.

The `caches.open()` method first checks if a cache with the provided name already exists. If it doesn’t, it creates it and returns a `Promise` that resolves with the `Cache` object.

```js
const newCache = window.caches.open("new-cache").then((data) => {
  console.log(data);
}); // Cache {  }
```

The returned `Cache` itself has methods that we can use.

### Add to cache with the `add()` method from a `Cache` instance

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

### Add to cache with the `addAll()` method from a `Cache` instance

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

### Change and override cache with the `put()` method from a `Cache` instance

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

### Retrieve an item in cache using `match()` method from `Cache` and `CacheStorage`

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

### Retrieve all items in cache using `matchAll()` method from `Cache` and `CacheStorage`

`matchAll()` method works the same as `match()` but retrieves all the matching items from cache. If no resources are found in the cache, the `matchAll()` method returns an empty array.

The method could be accessed either through `CacheStorage` (`window.caches.matchAll()`) or `Cache` instance.

### Iterate through cache items using `keys()` method from `Cache` and `CacheStorage`

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

### Delete an item from cache using `delete()` method from `Cache`

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

### Remove a cache with `window.caches.delete()`

We can also delete a cache by calling the `delete()` method on the `caches` property of the `window` object. This is different from the `delete()` method of the `Cache` instance. When a cache is deleted using `window.caches.delete()`, the method returns a `Promise` if the cache was actually deleted and a `false` if something went wrong or the cache doesn’t exist.

```js
// delete an existing cache
window.caches.delete("new-cache");
```

### Find a cache with `window.caches.has()`

The `has(<cache_name>)` method of the `CacheStorage` interface returns a `Promise` that resolves to `true` if a `Cache` object matches the `<cache_name>`. It accepts a string representing the name of the `Cache` object you are looking for in the `CacheStorage`.

```js
window.caches.open("new-cache");

window.caches.has("new-cache").then((data) => console.log(data)); //true
```

<hr>

## `window.clientInformation` or `window.navigator`

`window.clientInformation` is an alias for `window.navigator`. The `Window.navigator` read-only property returns a reference to the `Navigator` object, which has methods and properties about the application running the script. The `Navigator` object represents the state and the identity of the user agent (browser). It has a lot of methods and properties. You can refer here for a thorough list: [MDN Navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator)

### `navigator.clipboard`

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

## `window.history`

The `window.history` read-only property returns a reference to the `History` object, which provides an interface for manipulating the browser session history (pages visited in the tab or frame that the current page is loaded in).

### Moving back and forward in the browsing history

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

### Number of pages in the browsing history

You can determine the number of pages in the history stack by looking at the value of the `history.length` property.

### `history.pushState()` and `history.replaceState()`

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

## `window.innerHeight` and `window.innerWidth`

The read-only `innerHeight` property returns the interior height of the window in pixels, including the height of the horizontal scroll bar, if present.

The read-only `innerWidth` property returns the interior width of the window in pixels, including the width of the vertical scroll bar, if present.

```js
console.log(window.innerHeight);
console.log(window.innerWidth);
```

<hr>

## `window.location`

The `window.location` read-only property returns a `Location` object with information about the current location (URL) of the document.

### Location properties to retrieve URL parts

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

### `location.assign()`

`location.assign(<url>)` loads the resource at the URL provided in the parameter. The URL can be absolute or relative. If the URL is not of the same origin as the script, it will cause an error.

```js
setTimeout(() => {
  location.assign("#hello");
  console.log(`redirected to ${location.origin}${location.pathname}#hello`);
}, 1000);
```

### `location.replace()`

`location.replace(<url>)` replaces the current resource with the one at the provided URL (redirects to the provided URL).

The difference from the `assign()` method and setting the `href` property is that after using `replace()` the current page will not be saved in session `History`, meaning the user won't be able to use the back button to navigate to it.

```js
setTimeout(() => {
  location.replace("#hello");
  console.log(`redirected to ${location.origin}${location.pathname}#hello`);
}, 1000);
```

### `location.reload()`

`location.reload()` reloads the current URL, like the Refresh button.

<hr>

## `window.open()` and `close`

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

## `window.confirm()`

`window.confirm()` instructs the browser to display a dialog with an optional message, and to wait until the user either confirms or cancels the dialog. It returns a boolean indicating whether OK (`true`) or Cancel (`false`) was selected.

```js
if (window.confirm("Do you really want to leave?")) {
  console.log("Thanks for Visiting!");
}
```

<hr>

## `window.getSelection()`

### Range

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

### Selection

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

### Selection in forms

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

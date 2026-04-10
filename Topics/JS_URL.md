# URL

- [URL](#url)
  - [Creating a `URL` object](#creating-a-url-object)
  - [Properties of a `URL` object](#properties-of-a-url-object)
  - [`URLSearchParams`](#urlsearchparams)
  - [Functions for encoding and decoding url and url components](#functions-for-encoding-and-decoding-url-and-url-components)
  - [`createObjectURL()` and `revokeObjectURL()`](#createobjecturl-and-revokeobjecturl)

---

---

## Creating a `URL` object

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

## Properties of a `URL` object

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

## `URLSearchParams`

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

## Functions for encoding and decoding url and url components

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

## `createObjectURL()` and `revokeObjectURL()`

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

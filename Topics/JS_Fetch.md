# Fetch

- [Fetch](#fetch)
  - [GET request](#get-request)
  - [POST request](#post-request)
  - [Fetch and HTTP status codes](#fetch-and-http-status-codes)
  - [Headers](#headers)
  - [Cancel a fetch request](#cancel-a-fetch-request)

---

---

## GET request

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

---

---

## POST request

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

---

---

## Fetch and HTTP status codes

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

---

---

## Headers

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

---

---

## Cancel a fetch request

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

---

---

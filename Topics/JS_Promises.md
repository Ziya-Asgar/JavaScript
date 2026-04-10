# Promises, async/await

- [Promises, async/await](#promises-asyncawait)
  - [Quick intro to promise](#quick-intro-to-promise)
  - [Internal properties of a returned promise object](#internal-properties-of-a-returned-promise-object)
  - [`.then` without catching the promise rejection](#then-without-catching-the-promise-rejection)
  - [Chained `then`s](#chained-thens)
  - [Controlling for errors using `.then`](#controlling-for-errors-using-then)
  - [`.then` after `.catch`](#then-after-catch)
  - [`finally`](#finally)
  - [A promise inside a promise](#a-promise-inside-a-promise)
  - [`Promise.all`](#promiseall)
  - [`Promise.allSettled`](#promiseallsettled)
  - [`Promise.race()`](#promiserace)
  - [`Promise.any`](#promiseany)
  - [`async`/`await`](#asyncawait)

---

---

## Quick intro to promise

Here is an example of using `Promise`. The function passed to `new Promise` is called the executor. When a `new Promise` is created, the executor runs automatically. Its arguments `resolve` and `reject` are callbacks provided by the JavaScript itself. When the executor obtains the result, it should call one of these callbacks:

- `resolve(value)` — if the job is finished successfully, with the result `value`.
- `reject(error)` — if an error has occurred, error is the `error` object.

```js
const promise = new Promise(function (resolve, reject) {
  resolve("done");
}).then(
  function (result) {
    console.log(`result is ${result}`);
  },
  function (error) {
    console.log(`error is ${error}`);
  },
);
```

The executor should call only one `resolve` or one `reject`. Any state change is final. All further calls of `resolve` and `reject` are ignored.

```js
const promise = new Promise(function (resolve, reject) {
  resolve("done");
  reject("this doesn't run");
}).then(
  function (result) {
    console.log(`result is ${result}`);
  },
  function (error) {
    console.log(`error is ${error}`);
  },
);
```

<hr>

## Internal properties of a returned promise object

The promise object returned by the new Promise constructor has these internal properties:

- `state` — initially "pending", then changes to either "fulfilled" when resolve is called or "rejected" when reject is called.
- `result` — initially `undefined`, then changes to `value` when `resolve(value)` is called or `error` when `reject(error)` is called.

The properties `state` and `result` of the `Promise` object are internal. We can’t directly access them. We can use the methods `.then`/`.catch`/`.finally` for that.

The first argument of `.then` is a function that runs when the promise is resolved and receives the result. The second argument of `.then` is a function that runs when the promise is rejected and receives the error.

```js
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

// the first function runs because promise resolves
promise.then(
  function (result) {
    console.log(`result is ${result}`);
  },
  function (error) {
    console.log(`error is ${error}`);
  }, // doesn't run because promise is not rejected
);
```

```js
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error("Custom Error Message")), 1000);
});

// the second function runs
promise.then(
  function (result) {
    console.log(`result is ${result}`); // doesn't run
  },
  function (error) {
    console.log(`error is ${error}`); // "Custom Error Message" after 1 second
  },
);
```

## `.then` without catching the promise rejection

`.then` accepts 2 functions: one to handle the result from a resolved promise, and the second one to handle the promise rejection. However, we can also use `.then` with one function alone, if we don't want to control for a possible error:

```js
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => resolve("done!"), 1000);
});

promise.then(function (result) {
  console.log(`result is ${result}`);
});
```

## Chained `then`s

We can have chained `then`s as well:

```js
const promise = new Promise(function (resolve, reject) {
  resolve("done");
})
  .then(function (result) {
    return `this goes to the next function in the chain with the result: ${result}`;
  })
  .then(function (result) {
    console.log(
      `This is from the second "then". This is what was returned from the first "then": ${result}`,
    );
  });
```

## Controlling for errors using `.then`

If we’re interested only in errors, then we can use `null` as the first argument to the `.then`: `.then(null, errorHandlingFunction)`. Or we can use `.catch(errorHandlingFunction)`, which is exactly the same:

```js
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error("Custom Error Message")), 1000);
});

// the second function runs
promise.then(
  null, // doesn't run
  function (error) {
    console.log(`error: ${error}`);
  },
);
```

```js
const promise = new Promise(function (resolve, reject) {
  setTimeout(() => reject(new Error("Custom Error Message")), 1000);
});

// catch runs
promise.catch(
    console.log(`error: ${error}`);
);
```

## `.then` after `.catch`

Usually, we define the `then` part of the promise and after that define the `catch`. However, we can use `.then` after a `.catch` as well:

```js
const promise = new Promise((resolve, reject) => {
  throw new Error("Custom Error Message");
})
  .catch(function (error) {
    console.log(error);
    return `this is not an error, keep running`;
  })
  .then((result) => {
    console.log("Final `then` runs");
    console.log(result);
  });
```

Moreover, we can define `then`, after that `catch`, and after that one more `then` again:

```js
const promise = new Promise((resolve, reject) => {
  throw new Error("Custom Error Message");
})
  .then(function (result) {
    console.log(`this doesn't run`);
  })
  .catch(function (error) {
    console.log(error);
    return `this is not an error, keep running`;
  })
  .then((result) => {
    console.log("Final `then` runs");
    console.log(result);
  });
```

## `finally`

`finally` always runs, and it shouldn't return anything. If it returns something, it will be ignored.

```js
const promise = new Promise(function (resolve, reject) {
  reject("error");
})
  .then(function (result) {
    console.log(result);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    console.log(`will run anyway`);
    // finally shouldn't return anything, if returns it will be ignored
  });
```

<hr>

## A promise inside a promise

A handler function, used in `.then(<handler>)` may create and return a promise. In that case further handlers wait until it settles, and then get its result.

```js
const promise = new Promise(function (resolve, reject) {
  resolve("1st promise");
})
  .then(function (result) {
    console.log(result);
    return new Promise(function (resolve, reject) {
      resolve("2nd promise");
    });
  })
  .then(function (result) {
    console.log(result);
  });
```

<hr>

## `Promise.all`

`Promise.all` takes an iterable (usually, an array of promises) and returns a new promise. The new promise resolves when all listed promises are resolved, and the array of their results becomes its result. If any promise is rejected, all gets rejected.

```js
const arrOfPromises = [
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(2), 1500)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 2000)),
];

// executes promises in parallel and waits until all of them are ready.
// If any promise is rejected, all gets rejected.
Promise.all(arrOfPromises)
  .then((res) => console.log(res)) // [1, 2, 3]
  .catch((err) => console.log(err));
```

```js
const arrOfPromises = [
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Rejected with an Error")), 1500),
  ),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 2000)),
];

// executes promises in parallel and waits until all of them are ready.
// If any promise is rejected, all gets rejected.
Promise.all(arrOfPromises)
  .then((res) => console.log(res))
  .catch((err) => console.log(err)); // Error: Rejected with an Error
```

`Promise.all(...)` accepts an iterable (in most cases an array) of promises. But it also accepts non-`Promise` items. Those non-`Promise` items are passed to the resulting array “as is”.

```js
Promise.all([
  new Promise((resolve, reject) => {
    setTimeout(() => resolve(1), 1000);
  }),
  2,
  3,
]).then(console.log); // 1, 2, 3
```

<hr>

## `Promise.allSettled`

`Promise.allSettled` waits for all promises to settle, regardless of the result. The resulting array has:

- `{status:"fulfilled", value:result}` for successful responses,
- `{status:"rejected", reason:error}` for errors.

```js
const arrOfPromises = [
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Rejected with an Error")), 1500),
  ),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 2000)),
];

Promise.allSettled(arrOfPromises).then(console.log);
```

<hr>

## `Promise.race()`

`Promise.race()` waits only for the first settled promise and gets its result. If there is an error, then it returns the error:

```js
const arrOfPromises = [
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Rejected with an Error")), 1500),
  ),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 2000)),
];

Promise.race(arrOfPromises).then(console.log);
```

<hr>

## `Promise.any`

`Promise.any` waits only for the first fulfilled promise and gets its result. If all of the given promises are rejected, then the returned promise is rejected with the `AggregateError` – a special error object that stores all promise errors in its `errors` property.

```js
const arrOfPromises = [
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) =>
    setTimeout(() => reject(new Error("Rejected with an Error")), 1500),
  ),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 2000)),
];

Promise.any(arrOfPromises)
  .then((res) => console.log(`fulfilled result ${res}`))
  .catch((error) => {
    console.log(error.constructor.name);
    console.log(error.errors[0]);
  });
```

<hr>

## `async`/`await`

`async`/`await` is a more comfortable special syntax to work with promises. Async functions are defined by putting the word `async` before the function. `async` before a function means that a function always returns a promise.

```js
async function asyncFunc() {
  return 1; // same as return Promise.resolve(1)
}
```

`async` functions also can use `.then` and `.catch`:

```js
async function asyncFunc() {
  return 1; // same as return Promise.resolve(1)
}

asyncFunc().then(console.log).catch(console.log);
```

The `await` keyword makes JavaScript wait until the promise settles and returns its result. `await` can only be used inside an `async` function.

```js
async function asyncFunc() {
  const promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000);
  });

  const result = await promise; // wait until the promise resolves

  console.log(result); // "done!"
}

asyncFunc();
```

<hr>
<hr>

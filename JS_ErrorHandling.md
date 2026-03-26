# Error Handling

- [Error Handling](#error-handling)
  - [`try...catch()`, and properties of an error object](#trycatch-and-properties-of-an-error-object)
  - [`try...catch()` and asynchronous code](#trycatch-and-asynchronous-code)
  - [`catch` without parentheses](#catch-without-parentheses)
  - [`throw` operator and different built-in error constructors](#throw-operator-and-different-built-in-error-constructors)

---

## `try...catch()`, and properties of an error object

To handle the errors, we can use `try...catch()` or `try...catch()...finally` block. For all built-in errors, the error object has two main properties: `name`, and `message`. There are other non-standard properties available in the most environments. One of the most widely used and supported is `stack`:

```js
try {
  console.log(`try runs`);
} catch (err) {
  console.log(`if there is an error this part of the code catches it`);
  console.log(err.name);
  console.log(err.message);
  console.log(err.stack);
  console.log(err);
} finally {
  console.log(`finally always runs`);
}
```

```js
try {
  // throw an error to see the catch block working
  throw new Error("custom message");
} catch (err) {
  console.log(`if there is an error this part of the code catches it`);
  console.log(err.name);
  console.log(err.message);
  console.log(err.stack);
  console.log(err);
} finally {
  console.log(`finally always runs`);
}
```

<hr>

## `try...catch()` and asynchronous code

`try...catch()` works synchronously. If an exception happens in a “scheduled” code, like in `setTimeout`, then `try...catch()` won’t catch it. That’s because the function itself is executed later, when the engine has already left the `try...catch()` construct. To catch an exception inside a scheduled function, `try...catch()` must be inside that function:

```js
setTimeout(function () {
  try {
    undefinedVariable; // try...catch handles the error!
  } catch (err) {
    console.log("Here is the error: " + err);
  }
}, 1000);
```

<hr>

## `catch` without parentheses

If we don’t need the error details, `catch` might be used without parentheses:

```js
try {
  undefinedVariable;
} catch {
  console.log(`catch runs`);
} finally {
  console.log(`finally always runs`);
}
```

<hr>

## `throw` operator and different built-in error constructors

The `throw` operator generates an error. JavaScript has many built-in constructors for standard errors: `Error`, `SyntaxError`, `ReferenceError`, `TypeError` and others. We can use them to throw our own errors, if needed:

```js
try {
  console.log(`we can throw our own errors if needed`);

  if (!someVariable) {
    throw new SyntaxError(`custom Syntax Error message`);
  }
} catch (err) {
  if (!(err instanceof SyntaxError)) {
    throw new Error(`This is not a Syntax Error, do something else`);
  }

  console.log(`Here is the syntax error message: ${err.message}`);
}
```

<hr>
<hr>

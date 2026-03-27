# Generators

- [Generators](#generators)
  - [Intro to generators](#intro-to-generators)
  - [`next()`](#next)
  - [Looping over generators](#looping-over-generators)
  - [Spread syntax with generators](#spread-syntax-with-generators)
  - [Generator in a generator](#generator-in-a-generator)
  - [Passing an argument to a generator](#passing-an-argument-to-a-generator)
  - [Pass an error to the generator](#pass-an-error-to-the-generator)
  - [Finishing a generator early](#finishing-a-generator-early)

---

---

## Intro to generators

Regular functions return single value (or nothing). Generators can return (`yield`) multiple values, one after another, on-demand. To create a generator, we use `function*`, so-called “generator function”.

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  return 3;
}
```

<hr>

When a generator function is called, it doesn’t run its code. It returns a special object, called “generator object”, to manage the execution.

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  return 3;
}

const generator = generatorFunc();
console.log(generator); // // [object Generator]
```

<hr>

## `next()`

To run the code of a generator, we use the `next()` method. When called, it runs the execution until the nearest `yield <value>` statement and returns the yielded value. The result of `next()` is always an object with two properties:

- `value`: the yielded value.
- `done`: `true` if the function code has finished, otherwise `false`.

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  return 3;
}

const generator = generatorFunc();

console.log(generator.next()); // {value: 1, done: false}
console.log(generator.next()); // {value: 2, done: false}
console.log(generator.next()); // {value: 3, done: true}
```

After the final return value is reached, if the `next()` method is used again, it will return `{value: undefined, done: true}`.

<hr>

## Looping over generators

Generators are iterable. We can loop over their values using `for..of`:

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  return 3;
}

const generator = generatorFunc();

for (let value of generator) {
  console.log(value);
  // outputs 1, 2. To output 3, yield should be used instead of return
}
```

`for..of` ignores the last value, when `done: true`. So, if we want all results to be shown by `for..of`, we must return them with `yield` not `return`.

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = generatorFunc();

for (let value of generator) {
  console.log(value);
  // outputs 1, 2, 3
}
```

<hr>

## Spread syntax with generators

As generators are iterable, we can also use the spread syntax `...` with them:

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  return 3;
}

const generator = generatorFunc();

const arrFilledByGenerator = [0, ...generator];

// To have 3 in the array, `yield` should be used instead of `return`
console.log(arrFilledByGenerator); // [0, 1, 2]
```

<hr>

## Generator in a generator

Generator composition allows to have generators in each other. There’s a special `yield*` syntax to embed one generator into another one. The `yield*` directive delegates the execution to another generator. In other words, `yield* <gen>` iterates over the generator `<gen>` and transparently forwards its yields outside, as if the values were yielded by the outer generator.

```js
function* generatorFunc(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

function* genWithinGen() {
  yield* generatorFunc(40, 60);
}

const generator = genWithinGen();

console.log(generator.next()); // { value: 40, done: false }
console.log(generator.next()); // { value: 41, done: false }
```

<hr>

## Passing an argument to a generator

`yield` not only returns the result to the outside, but also can pass the value inside the generator. To pass a value inside, we should call `generator.next(<arg>)`, with an argument. That argument becomes the result of `yield`.

```js
function* generatorFunc() {
  let result = yield `2 + 2 = ?`;

  console.log(result);
}

const generator = generatorFunc();
console.log(generator.next().value); // here the value returns the yielded "2 + 2 = ?"
generator.next(4); // 4 passed inside and becomes the result, after which it is logged to the console
```

The first call `generator.next()` should always be made without an argument. The argument is ignored if passed.

<hr>

## Pass an error to the generator

We can also pass an error to the generator. To pass an error into a `yield`, we should call `generator.throw(<err>)`.

```js
function* generatorFunc() {
  try {
    let result = yield `2 + 2 = ?`;
    console.log(result);
  } catch (error) {
    console.log(error);
  }
}

const generator = generatorFunc();
generator.next().value;

generator.throw(new Error("Custom Error message"));
```

<hr>

## Finishing a generator early

Even if a generator has more values to yield, we can finish it using the `generator.return(<arg>)`. It returns the provided `<arg>`:

```js
function* generatorFunc() {
  yield 1;
  yield 2;
  yield 3;
}

const generator = generatorFunc();
console.log(generator.next()); // { value: 1, done: false }

// generator.return(value) finishes the generator execution and returns the given value.
console.log(generator.return("The End")); // { value: "The End", done: true }

console.log(generator.next()); // { value: undefined, done: true }
```

<hr>
<hr>

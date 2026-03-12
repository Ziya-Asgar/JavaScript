# Notes about loops in JavaScript

- [Notes about loops in JavaScript](#notes-about-loops-in-javascript)
  - [`for...in` loop](#forin-loop)
  - [Four native ways to list/traverse an object](#four-native-ways-to-listtraverse-an-object)
  - [`for...of` loop](#forof-loop)

<hr>

## `for...in` loop

- `for...in` loop is used with objects.

```js
const obj = {
  name: "some name",
  age: 30,
};

for (let key in obj) {
  console.log(`${key}: ${obj[key]}`);
}
```

- Symbol properties do not participate in the `for...in` loop

```js
const id = Symbol("id");

const obj = {
  name: "SomeName",
  [id]: 123,
};

for (key in obj) {
  console.log(key);
} // name

// `Object.keys()` also ignores Symbol properties
console.log(Object.keys(obj)); // ['name']
```

<hr>

## Four native ways to list/traverse an object

There are four native ways to list/traverse object properties, which could be useful in looping through objects:

- `for...in` loops. This method traverses all of the enumerable string properties of an object as well as its prototype chain.

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

for (let key in Child1) {
  console.log(key); // childProp1 prototypeProp1
}
```

- `Object.keys()` returns an array of object keys. `Object.values()` returns an array of object values. These methods do not return keys and values from the prototype chain.

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.keys(obj); // returns an array of keys
Object.values(obj); // returns an array of values
```

- `Object.entries()` returns an array that includes arrays consisting of key-value pairs

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.entries(obj); // returns an array of [key, value] pairs.
```

- `Object.getOwnPropertyNames(<obj>)` returns an array containing all the own string property names in the object `obj`, regardless of if they are enumerable or not.

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

console.log(Object.getOwnPropertyNames(Child1)); // ['childValue1']
```

<hr>

## `for...of` loop

- `for...of` loop could be used with arrays.

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

// Object.values() returns an array
for (let value of Object.values(obj)) {
  console.log(value); // loop over values
}
```

- `for...of` loop could be used with maps.

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

for (let entry of map) {
  console.log(entry);
}
```

- `for...of` loop could be used with sets.

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

for (let item of set) console.log(item);
```

- `for...of` loop could be used with generators.

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

- `for...of` loop could generally be used with iterable objects such as strings, childNodes, classList, etc.

```js
const str = `This is a string`;

for (let char of str) {
  console.log(char);
}
```

# Destructuring

- [Destructuring](#destructuring)
  - [Destructuring an array](#destructuring-an-array)
  - [Destructuring a string](#destructuring-a-string)
  - [Destructuring a set](#destructuring-a-set)
  - [Sawpping values using destructuring](#sawpping-values-using-destructuring)
  - [Destructuring an object](#destructuring-an-object)

---

## Destructuring an array

Here is an example of destructuring an array:

```js
const arr = ["Firstname", "Lastname"];

const [firstname, lastname] = arr;

console.log(firstname); // John
console.log(lastname); // Smith
```

Another example of destructuring an array (`.split()` returns an array):

```js
const [firstname, lastname] = "Firstname Lastname".split(" ");

console.log(firstname); // John
console.log(lastname); // Smith
```

Here is an example of destructuring an array and setting the destructured items as values of keys in an object:

```js
const obj = {};
[obj.key1, obj.key2] = "value1 value2".split(" ");

console.log(obj); // {key1: 'value1', key2: 'value2'}
```

We can also destructure partially by taking only some of the array items:

```js
const arr = [1, 2, 3, 4, 5];

const [firstValue, secondValue] = arr; // takes first 2 values and ignores the rest
```

Here is a similar example, but this time the rest of the array items are saved into an array using destructuring:

```js
const arr = [1, 2, 3, 4, 5];
const [first, second, ...theRest] = arr;

console.log(first); // 1
console.log(second); // 2
console.log(theRest); // [3, 4, 5]
```

Here is an example of destructuring by setting default values to variables:

```js
const [value1 = "default value1", value2 = "default value2"] = ["new value1"];

console.log(value1); // new value1
console.log(value2); // default value2
```

## Destructuring a string

Here is an example of destructuring a string:

```js
const [a, b, c] = "abc";
```

## Destructuring a set

Here is an example of destructuring a set:

```js
const [one, two, three] = new Set([1, 2, 3]);
```

## Sawpping values using destructuring

Here is how to swap the values of variables using destructuring:

```js
let one = 2;
let two = 1;

[one, two] = [two, one];

console.log(one); // 1
console.log(two); // 2
```

## Destructuring an object

Destructuring an object:

```js
const obj = {
  title: "title",
  height: 100,
  width: 200,
};

const { title, height, width } = obj;
```

Destructuring an object by setting default values to variables:

```js
const obj = {
  title: "title",
};

const { title = "default value", height = "default height" } = obj;

console.log(title); // title
console.log(height); // default height
```

Instead of using the variables that are exactly the same as keys of an object, we can also rename those variables while destructuring:

```js
const obj = {
  title: "title",
  height: 100,
  width: 200,
};

const { title: t, height: h, width: w } = obj;

console.log(t); // title
console.log(h); // 100
console.log(w); // 200

console.log(title); // Uncaught ReferenceError: title is not defined
```

We can combine both setting the default values and renaming the keys of an object that we are destructuring:

```js
const obj = {
  title: "title",
  height: 100,
};

const {
  title: t = "default value",
  height: h,
  width: w = "default value",
} = obj;

console.log(t); // title
console.log(h); // 100
console.log(w); // default value
```

We can use the spread operator together with the object destructuring as well:

```js
const obj = {
  title: "title",
  height: 100,
  width: 200,
};

const { title, ...restOfObj } = obj;

console.log(title); // title
console.log(restOfObj); // {height: 100, width: 200}
```

We can destructure an object in the function parameters as well:

```js
const obj = {
  title: "some title",
  height: 100,
  width: 200,
};

function func({ title }) {
  return title;
}

console.log(func(obj)); // some title
```

We can also destructure nested objects and arrays:

```js
const obj = {
  size: {
    length: 100,
    altitude: 200,
  },
  items: ["Cake", "Donut"],
  extra: true,
};

const {
  size: { length, altitude },
  items: [item1, item2],
  anotherItem = "default value",
} = obj;

console.log(length); // 100
console.log(item1); // cake
```

<hr>
<hr>

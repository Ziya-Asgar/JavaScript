# Notes on Copying an Object in JavaScript

<hr>

Here are different ways of copying an object:

1. Using `for...in` loop:

```js
const obj = {
  name: "some name",
  age: 30,
};

const copyOfObj = {};

for (let key in obj) {
  copyOfObj[key] = obj[key];
}
```

2. using `Object.assign`:

`Object.assign()` accepts an object as a first argument, and copies all the properties of other objects given to it, into the first argument:

```js
const obj = {
  name: "some name",
  age: 30,
};

const copyOfObj = {};

Object.assign(copyOfObj, obj, {
  "key in another object": "some value",
});
```

3. using `structuredClone`:

The global `structuredClone()` method creates a deep copy of an object. If there is a nested object this function copies the nested object as well, and not just a reference to that nested object. It copies together with all the nested objects, and properties, except functions:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const copyOfObj = structuredClone(obj);
```

4. Copying an object with its property flags:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const copyOfObjectWithFlags = Object.defineProperties(
  {},
  Object.getOwnPropertyDescriptors(obj)
);
```

5. Copying an object with its Prototype, and flags:

```js
// Object that will be used as a prototype
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const obj = {};

// Set the Prototype1 as the prototype of obj
Object.setPrototypeOf(obj, Prototype1);
console.log(Object.getPrototypeOf(obj)); // {prototypeValue1: 'prototypeValue1'}

const powerfulCopyOfObj = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(Prototype1)
);

console.log(Object.getPrototypeOf(powerfulCopyOfObj)); // {prototypeValue1: 'prototypeValue1'}
```

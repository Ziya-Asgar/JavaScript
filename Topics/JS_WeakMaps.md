# WeakMaps

- [WeakMaps](#weakmaps)
  - [Create a `WeakMap`](#create-a-weakmap)
  - [Add key-value pairs into a weakmap](#add-key-value-pairs-into-a-weakmap)
  - [Get the value of a specific key](#get-the-value-of-a-specific-key)
  - [`.has()`](#has)
  - [`.delete()`](#delete)

---

---

## Create a `WeakMap`

To create a `WeakMap`, we use the `new WeakMap()` syntax:

```js
const weakMap = new WeakMap();
```

---

---

## Add key-value pairs into a weakmap

To add key-value pairs into a weakmap, we use the `.set()` method. Remember the key of a weakmap must be an object:

```js
const weakMap = new WeakMap();

const obj = {
  key: "value",
  key2: "value2",
};

weakMap.set(obj, "value1");
```

---

---

## Get the value of a specific key

To get the value of a specific key, we use the `.get()` method:

```js
const weakMap = new WeakMap();

const obj = {
  key: "value",
  key2: "value2",
};

weakMap.set(obj, "value1");

console.log(weakMap.get(obj)); // value1
```

---

---

## `.has()`

`.has()` method returns `true`, if a weakmap has a specific key or `false` otherwise:

```js
const weakMap = new WeakMap();

const obj = {
  key: "value",
  key2: "value2",
};

weakMap.has(obj);
```

---

---

## `.delete()`

`.delete()` method deletes a specific key-value pair from weakmap:

```js
const weakMap = new WeakMap();

const obj = {
  key: "value",
  key2: "value2",
};

weakMap.delete(obj); // true
```

---

---

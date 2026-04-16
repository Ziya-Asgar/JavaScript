# Maps

- [Maps](#maps)
  - [Create a `Map`](#create-a-map)
  - [Add key-value pairs](#add-key-value-pairs)
  - [Get the value of a specific key](#get-the-value-of-a-specific-key)
  - [`.has()`](#has)
  - [`.size`](#size)
  - [`.keys()`](#keys)
  - [`.values()`](#values)
  - [`.entries()`](#entries)
  - [`.forEach()`](#foreach)
  - [`.delete()`](#delete)
  - [`.clear()`](#clear)

---

---

## Create a `Map`

To create a `Map`, we use the `new Map()` syntax:

```js
const map = new Map();
```

---

We can create a map from an object:

```js
const obj = {
  key: "value",
  key2: "value2",
};

const mapFromObj = new Map(Object.entries(obj));

console.log(mapFromObj); // {'key' => 'value', 'key2' => 'value2'}
```

---

We can create a map from an array of arrays:

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

console.log(map);
// {'1' => 'str1', 1 => 'num1', true => 'bool1'}
```

---

---

## Add key-value pairs

To add key-value pairs into a map, we use the `.set()` method:

```js
const map = new Map();

map.set("key", "value");
map.set(1, "value");
map.set("another key", 3).set(4, true);

console.log(map);
// {'key' => 'value', 1 => 'value', 'another key' => 3, 4 => true}
```

---

---

## Get the value of a specific key

To get the value of a specific key, we use the `.get()` method:

```js
const map = new Map();

map.set("key", "value");
map.set("another key", 3).set(4, true);

const result = map.get("key");

console.log(result); // value
```

---

---

## `.has()`

`.has()` method returns `true`, if a map has a specific key or `false` otherwise:

```js
const map = new Map();

map.set("key", "value");
map.set("another key", 3).set(4, true);

const result = map.has("key");

console.log(result); // true
```

---

---

## `.size`

`.size` property of a map returns how many key-value pairs a map has:

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

console.log(map.size); // 3
```

---

---

## `.keys()`

`.keys()` returns an iterable for keys of a map:

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

for (let key of map.keys()) {
  console.log(key);
}
```

---

---

## `.values()`

`.values()` returns an iterable for values of a map:

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

for (let value of map.values()) {
  console.log(value);
}
```

---

---

## `.entries()`

`.entries()` returns an iterable for key-value pairs of a map. Each key-value pair is returned as an array of 2 items - [key, value]:

```js
const map = new Map([
  ["1", "str1"],
  [1, "num1"],
  [true, "bool1"],
]);

for (let entry of map.entries()) {
  console.log(entry);
}
```

We can also loop over the key-value pairs of a map without using `entries` and simply using map itself:

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

---

---

## `.forEach()`

Map has a built-in `.forEach()` method, which provides access to each value, key, and the map itself:

```js
const map = new Map();

map.set("key", "value");
map.set("another key", 3).set(4, true);

map.forEach((value, key, map) => {
  console.log(`${key}: ${value} in ${map}`);
});
```

---

---

## `.delete()`

`.delete()` method deletes a specific key-value pair from map:

```js
const map = new Map();

map.set("key", "value");
map.set("another key", 3).set(4, true);

console.log(map); // {'key' => 'value', 'another key' => 3, 4 => true}

map.delete("key");

console.log(map); // {'another key' => 3, 4 => true}
```

---

---

## `.clear()`

`.clear()` method deletes all the key-value pairs from a map:

```js
const map = new Map();

map.set("key", "value");
map.set("another key", 3).set(4, true);

console.log(map); // {'key' => 'value', 'another key' => 3, 4 => true}

map.clear();

console.log(map); // {size: 0}
```

---

---

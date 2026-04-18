# Sets

- [Sets](#sets)
  - [Create a `Set`](#create-a-set)
  - [Add items to a set](#add-items-to-a-set)
  - [`.has()`](#has)
  - [`.size`](#size)
  - [Loop over the set items](#loop-over-the-set-items)
  - [`.forEach()`](#foreach)
  - [`.delete()`](#delete)
  - [`.clear()`](#clear)

---

---

## Create a `Set`

To create a `Set`, we use the `new Set()` syntax:

```js
const set = new Set();
```

We can create a set from an array:

```js
const set = new Set(["value1", "value1", "value2", "value3"]);

console.log(set); // Set(3) {'value1', 'value2', 'value3'}
```

---

---

## Add items to a set

To add items to a set, we use the `add` method:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });
```

---

---

## `.has()`

`.has()` method returns `true`, if a set has a specific item or `false` otherwise:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

const result = set.has("value");

console.log(result); // true
```

---

---

## `.size`

We can find how many items a set has using the `.size` property:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

const result = set.size;

console.log(result); // 2
```

---

---

## Loop over the set items

We can loop over the set items using the `for...of` loop:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

for (let item of set) console.log(item);
```

---

---

## `.forEach()`

Set has a `.forEach()` method, which provides access to each value (twice) and the set itself:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

set.forEach((value, valueAgain, set) => {
  console.log(value);
});
```

---

---

## `.delete()`

`.delete()` method deletes a specific item from a set:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

set.delete("value");
```

---

---

## `.clear()`

`.clear()` method deletes all the key-value pairs from a set:

```js
const set = new Set();

set.add("value");
set.add({ name: "some name" });

set.clear();
```

---

The same methods Map has for iterators are also supported with Set:

- `.keys()` – returns an iterable object for values,
- `.values()` – same as `.keys()`, for compatibility with Map,
- `.entries()` – returns an iterable object for entries [value, value], exists for compatibility with Map.

```js
const set = new Set(["value1", "value2"]);

for (let key of set.keys()) console.log(key);
for (let value of set.values()) console.log(value);
for (let entry of set.entries()) console.log(entry);
```

---

---

# WeakSets

- [WeakSets](#weaksets)
  - [Create a `WeakSet`](#create-a-weakset)
  - [Add an item to a weakset](#add-an-item-to-a-weakset)
  - [`.has()`](#has)
  - [`.delete()`](#delete)

---

## Create a `WeakSet`

To create a `WeakSet`, we use the `new WeakSet()` syntax:

```js
const weakSet = new WeakSet();
```

<hr>

## Add an item to a weakset

To add an item to a weakset, we use the `add` method:

```js
const obj = {
  key: "value",
  key2: "value2",
};

const weakSet = new WeakSet();

weakSet.add(obj);
```

<hr>

## `.has()`

`.has()` method returns `true`, if a weakset has a specific item or `false` otherwise:

```js
const obj = {
  key: "value",
  key2: "value2",
};

const weakSet = new WeakSet();

weakSet.has(obj);
```

<hr>

## `.delete()`

`.delete()` method deletes a specific item from a weakset:

```js
const obj = {
  key: "value",
  key2: "value2",
};

const weakSet = new WeakSet();

weakSet.delete(obj);
```

<hr>
<hr>

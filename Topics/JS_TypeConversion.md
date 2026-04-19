# Type Conversion

- [Type Conversion](#type-conversion)
  - [`String()`](#string)
  - [`Number()`](#number)
    - [`+` operator](#-operator)
  - [`Boolean()`](#boolean)

---

---

## `String()`

`String()` turns the provided argument into a string:

```js
typeof String(10); // string
```

---

---

## `Number()`

`Number()` turns the provided argument into a number:

```js
typeof Number("10"); // number
```

### `+` operator

As well as adding numbers, `+` operator, can be used to convert a variable to a number:

```js
typeof +"10"; // number
```

---

---

## `Boolean()`

`Boolean()` turns the provided argument to either `true` or `false`:

```js
Boolean(" "); // true
Boolean(""); // false
```

---

---

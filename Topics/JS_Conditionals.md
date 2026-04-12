# Conditionals

- [Conditionals](#conditionals)
  - [`if()` on a single line](#if-on-a-single-line)
  - [`if()...else`](#ifelse)
  - [`if()...else if()...else`](#ifelse-ifelse)
  - [Ternary conditions](#ternary-conditions)
  - [`switch`](#switch)

---

---

## `if()` on a single line

We can write an `if()` statement on a single line like this:

```js
const condition1 = true,
  condition2 = true;

if (condition1 === condition2) console.log(`It worked`); // It worked
```

---

---

## `if()...else`

An example for an `if()...else` statement:

```js
const condition1 = true,
  condition2 = false;

if (condition1 === condition2) {
  console.log(`${condition1} and ${condition2} are equal`);
} else {
  console.log(`some default result`);
}
```

---

---

## `if()...else if()...else`

An example for `if()...else if()...else` statement:

```js
const condition1 = true,
  condition2 = false;

if (condition1 === condition2) {
  console.log(`${condition1} and ${condition2} are equal`);
} else if (condition1 < condition2) {
  console.log(`${condition1} is less than ${condition2}`);
} else {
  console.log(`some default result`);
}
```

---

---

## Ternary conditions

We can set ternary conditions like this:

```js
const condition1 = true,
  condition2 = false;

const resultOfConditions =
  condition1 === condition2
    ? `Equal`
    : condition1 < condition2
      ? `Less`
      : condition1 > condition2
        ? `More`
        : `None is true`;

console.log(resultOfConditions); // More
```

---

---

## `switch`

Another conditional statement is `switch`. `switch` statement needs a strict match, meaning the same data type:

```js
const condition1 = true;

switch (condition1) {
  case 0:
    console.log(0);
    break;
  case 1:
  case 2:
    console.log(`1 or 2`);
    break;
  case 3:
    console.log(3);
    break;
  default:
    console.log(`Default result`);
}
```

---

---

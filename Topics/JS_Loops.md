# Loops

- [Loops](#loops)
  - [`while()`](#while)
  - [`while` with `break`](#while-with-break)
  - [`while()` loop on a single line](#while-loop-on-a-single-line)
  - [`do...while()`](#dowhile)
  - [`for()`](#for)
  - [Named `for` loop](#named-for-loop)

---

## `while()`

An example for the `while()` loop:

```js
let condition = 1;

while (condition < 3) {
  console.log(condition);
  condition++;
} // 1 2
```

## `while` with `break`

We can use `while` with `break` as well:

```js
let condition = 1;

while (condition < 3) {
  console.log(condition);
  condition++;
  break;
} // 1
```

## `while()` loop on a single line

We can write a `while()` loop on one line:

```js
let condition = 1;

while (condition < 3) console.log(condition++);
```

<hr>

## `do...while()`

`do...while()` loop runs at least once, then checks if a condition for the loop is true:

```js
let condition = 1;

do {
  console.log(condition);
  condition++;
} while (condition < 1);
```

<hr>

## `for()`

An example for the `for()` loop:

```js
for (let i = 0; i < 3; i++) {
  console.log(i);
}
```

`for` loops can also be like these:

```js
let condition = 1;

for (; condition < 3; condition++) {
  console.log(condition);
}
```

```js
let condition = 1;

for (; condition < 3; ) {
  console.log(condition++);
  break;
}
```

<hr>

## Named `for` loop

We can name a `for` loop and then `break` the loop using the name:

```js
label: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (j == 1) continue; // skips the inner loop when j == 1
    if (i == 1) break label; // breaks the outer loop when i == 1

    console.log(`i is ${i}, j is ${j}`);
  }
}
```

```js
// Example 2: Using break to exit the inner loop:
outerLoop: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    if (j == 1) {
      console.log(`Breaking out of inner loop`);
      break;
    }
    console.log(`i: ${i}, j: ${j}`);
  }
}
```

<hr>
<hr>

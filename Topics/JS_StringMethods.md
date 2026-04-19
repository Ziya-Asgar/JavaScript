# String Methods

- [String Methods](#string-methods)
  - [Define a string and access characters](#define-a-string-and-access-characters)
  - [Turning the string into upper or lower case](#turning-the-string-into-upper-or-lower-case)
  - [`.length`](#length)
  - [`.indexOf()`](#indexof)
  - [`.lastIndexOf()`](#lastindexof)
  - [`.includes()`](#includes)
  - [`.startsWith()`, `.endsWith()`](#startswith-endswith)
  - [`.slice()`](#slice)
  - [`.substring()`](#substring)
  - [`.substr()`](#substr)
  - [`.split()`](#split)
  - [`.trim()`](#trim)
  - [Looping through strings](#looping-through-strings)

---

---

## Define a string and access characters

Here is an easy way to define a string:

```js
const str = `This is a string`;
```

---

Accessing different characters of a string:

```js
const str = `This is a string`;

str[0]; // T

str.at(0); // default is zero. T

str.charAt(); // default is zero. T
```

---

---

## Turning the string into upper or lower case

Turning the string into upper or lower case:

```js
const str = `This is a string`;

str.toUpperCase(); // THIS IS A STRING

str.toLowerCase(); // this is a string
```

---

---

## `.length`

`length` returns the number of characters in a string:

```js
const str = `This is a string`;

str.length; // 16
```

---

---

## `.indexOf()`

`indexOf(<characters>, [optional position number])` returns the position of the first occurrence of a substring from a specified position number. Returns `-1` when can't find the string.

```js
const str = `This is a string`;

str.indexOf("is"); // 2

str.indexOf("is", 3); // 5

str.indexOf("is", 6); // -1
```

---

---

## `.lastIndexOf()`

`lastIndexOf(<characters>, [optional position number])` similar to `indexOf`, but searches from right to left. Returns the position of the first occurrence of a substring from a specified position number. Returns `-1` when can't find the string.

```js
const str = `This is a string`;

str.lastIndexOf("is"); // 5

str.lastIndexOf("is", 4); // 2
```

---

---

## `.includes()`

`includes(<characters>, [optional position number])` searches for characters in a given string, and returns `true` or `false`. It starts the search from an optional position number if provided.

```js
const str = `This is a string`;

str.includes("is"); // true
str.includes("is", 6); // false
```

---

---

## `.startsWith()`, `.endsWith()`

`startsWith(<characters>)` checks if a string starts with given characters. Returns `true` or `false`. It's case sensitive:

```js
const str = `This is a string`;

str.startsWith("This"); // true
str.startsWith("this"); // false
```

`endsWith(<characters>)` checks if a string ends with given characters. Returns `true` or `false`. It's case sensitive:

```js
const str = `This is a string`;

str.endsWith("string"); // true
str.endsWith("String"); // false
```

---

---

## `.slice()`

`slice(<start>, <end>)` returns a section of a string based on given start, and end positions:

```js
const str = `This is a string`;

str.slice(); // This is a string
str.slice(0); // This is a string
str.slice(0, 4); // This
str.slice(-6, -1); // strin
str.slice(-6); // string

str.slice(5, 2); // nothing is returned, as the end position number is smaller than the start position number
```

---

---

## `.substring()`

`substring(<start> or <end>, <end> or <start>)` returns a section of a string based on given start, and end positions. Unlike `slice`, the end position provided to `substring` can be lower than the start position. Also, if either or both of the arguments to `substring()` are negative or `NaN`, the `substring()` method treats them as if they were 0:

```js
const str = `This is a string`;

str.substring(); // This is a string
str.substring(0); // This is a string
str.substring(2, 9); // is is a
str.substring(9, 2); // is is a.

str.substring(-5, -2); // nothing is returned
```

---

---

## `.substr()`

`substr(<start>, <number of characters>)` returns a section of a string at the specified location and having the specified length. Negative lengths in `substr()` are treated as zero. This method is deprecated, and is not advised to be used.

```js
const str = `This is a string`;

str.substr(); // This is a string
str.substr(0); // This is a string
str.substr(5, 4); // is a
str.substr(-4, 4); // ring

str.substr(-4, -4); // nothing is returned
```

---

---

## `.split()`

`split(<delimiter> [, <limit>])` returns a string split by a provided delimiter. If you provide a number to `split` as a second argument, it will return the limited number of split items in the resulting array:

```js
const str = `This is a string`;

str.split(); // ['This is a string']
str.split(" "); // ['This', 'is', 'a', 'string']
str.split(" ", 2); // ['This', 'is']
str.split(""); // ['T', 'h', 'i', 's', ' ', 'i', 's', ' ', 'a', ' ', 's', 't', 'r', 'i', 'n', 'g']
str.split("is"); // ['Th', ' ', ' a string']
```

---

---

## `.trim()`

The `trim()` method removes whitespace from both ends of a string without modifying the original string.:

```js
const sentence = "   JavaScript is amazing!   ";

console.log(sentence.trim()); // JavaScript is amazing!
```

---

---

## Looping through strings

You can loop through strings:

```js
const str = `This is a string`;

for (let char of str) {
  console.log(char);
}
```

```js
const str = `This is a string`;

for (let charIndex = 0; charIndex < str.length; charIndex++) {
  console.log(str[charIndex]);
}
```

---

---

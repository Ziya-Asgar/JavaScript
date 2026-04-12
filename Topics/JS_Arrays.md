# Arrays

- [Arrays](#arrays)
  - [Create an array](#create-an-array)
  - [Accessing array items](#accessing-array-items)
  - [Copy arrays with the spread operator](#copy-arrays-with-the-spread-operator)
  - [`.pop()`](#pop)
  - [`.push()`](#push)
  - [`.shift()`](#shift)
  - [`.unshift()`](#unshift)
  - [Return values of `.push()` and `.unshift()`](#return-values-of-push-and-unshift)
  - [Cutting out arrays with `.length`](#cutting-out-arrays-with-length)
  - [`.splice()`](#splice)
  - [`.concat()`](#concat)
  - [`.forEach()`](#foreach)
  - [`.indexOf()` and `.lastIndexOf`](#indexof-and-lastindexof)
  - [`.includes()`](#includes)
  - [`.find()`](#find)
  - [`.findIndex()` and `.findLastIndex`](#findindex-and-findlastindex)
  - [`.filter()`](#filter)
  - [`.map()`](#map)
  - [`.sort()`](#sort)
  - [`.toSorted()`](#tosorted)
  - [`.reverse()`](#reverse)
  - [`.toReversed()`](#toreversed)
  - [`.join()`](#join)
  - [`.reduce()`](#reduce)
  - [`.reduceRight()`](#reduceright)
  - [Higher order functions and `this`](#higher-order-functions-and-this)
  - [`Array.isArray()`](#arrayisarray)
  - [`.some()`](#some)
  - [`.every()`](#every)
  - [`Array.from()`](#arrayfrom)
  - [`.fill()`](#fill)

---

---

## Create an array

Here are some ways to create an array:

```js
const array = new Array();

console.log(array); // []
```

```js
const array = new Array(4); // creates an array of length 4

console.log(array); // [empty × 4]
console.log(array.length); // 4
```

```js
const array = new Array("value1", "value2", "value3");

console.log(array); // ['value1', 'value2', 'value3']
```

```js
const array = ["value1", "value2", "value3"];

console.log(array); // ['value1', 'value2', 'value3']
```

---

---

## Accessing array items

We can access the array items using the square bracket notation. Also, `.at()` method helps us to access an array items in a specific position:

```js
const arr = ["value1", "value2", "value3"];

console.log(arr[1]); // value2
console.log(arr.at(1)); // value2
```

---

---

## Copy arrays with the spread operator

We can copy arrays into another array using the spread operator:

```js
const arr1 = new Array("value1", "value2", "value3");
const arr2 = ["value1", "value2", "value3"];

const arr3 = [0, ...arr1, ...arr2];
console.log(arr3); // [ 0, "value1", "value2", "value3", "value1", "value2", "value3" ]
```

---

---

## `.pop()`

`.pop()` method deletes and returns the last array item:

```js
const arr = ["value1", "value2", "value3"];

const deletedLastItem = arr.pop();

console.log(arr); // ['value1', 'value2']
console.log(deletedLastItem); // value3
```

---

---

## `.push()`

`.push()` method inserts an item to the end of an array. It returns the length of the array:

```js
const arr = ["value1", "value2", "value3"];

const lengthOfArr = arr.push("value4");
console.log(lengthOfArr); // 4

arr.push("value5", "value6");
console.log(arr); // ['value1', 'value2', 'value3', 'value4', 'value5', 'value6']
```

---

---

## `.shift()`

`.shift()` deletes and returns the first item of an array:

```js
const arr = ["value1", "value2", "value3"];

const deletedFirstItem = arr.shift();

console.log(arr); // ['value2', 'value3']
console.log(deletedFirstItem); // value1
```

---

---

## `.unshift()`

`.unshift()` method inserts an item or items to the beginning of an array. It returns the length of the array:

```js
const arr = ["value1", "value2", "value3"];

arr.unshift("new value1");
arr.unshift("new value2", "new value3");

console.log(arr); // ['new value2', 'new value3', 'new value1', 'value1', 'value2', 'value3']
```

---

---

## Return values of `.push()` and `.unshift()`

Remember `.push()` and `.unshift()` returns the length of an array:

```js
const array = ["value1", "value2", "value3"];

const newLength1 = array.push("value4");
const newLength2 = array.push("value5", "value6");

console.log(newLength1); // 4
console.log(newLength2); // 6
```

```js
const array = ["value1", "value2", "value3"];

const newLength1 = array.unshift("new value1");
const newLength2 = array.unshift("new value2", "new value3");

console.log(newLength1); // 4
console.log(newLength2); // 6
```

---

---

## Cutting out arrays with `.length`

If there is an array with several items, we can keep specific number of them and cut the rest out by specifying the `.length`:

```js
const arr = ["value1", "value2", "value3"];

// keeps only first 2 values of the array
arr.length = 2;

console.log(arr); // ['value1', 'value2']
```

---

---

## `.splice()`

`.splice()` helps to remove given number of array items starting from a given index:

```js
const arr = ["value1", "value2", "value3"];

// removes 2 values from index 1
arr.splice(1, 2);

console.log(arr); // ['value1']
```

We can also use `.splice()` to add items to a specific position in an array without deleting any existing items:

```js
const arr = ["value1", "value2", "value3"];

// removes 0 values from index 2, and adds 2 values
arr.splice(2, 0, "splice 1", "splice 2");

console.log(arr); // ['value1', 'value2', 'splice 1', 'splice 2', 'value3']
```

---

---

## `.concat()`

`.concat()` method merges two or more arrays. It does not change the existing arrays, but instead **returns a new array**.

```js
const arr1 = new Array();
const arr2 = ["value2"];
const arr3 = ["value3"];

const newArr = arr1.concat([1, 2], 3, 4, [5, 6], arr2, arr3);

console.log(newArr); // [1, 2, 3, 4, 5, 6, 'value2', 'value3']
```

---

---

## `.forEach()`

`forEach` method loops through an array and gives access to the **array item**, **index** of the item and the **array** itself:

```js
const arr = ["value1", "value2", "value3"];

arr.forEach((item, index, array) => {
  console.log(
    `${item} is at index ${index} in an array with these items: ${array}`,
  );
});
```

---

---

## `.indexOf()` and `.lastIndexOf`

`.indexOf()` method looks for an item starting from a given index, returns either the index or `-1`. The method `arr.lastIndexOf` is the same as `.indexOf()`, but looks for an item from right to left.

```js
const arr = ["value1", "value2", "value3"];

// looks for "looked up item" starting from index 2 to the right
console.log(arr.indexOf("looked up item", 2)); // -1

// looks for "value1" starting from index 0 to the right
console.log(arr.indexOf("value1", 0)); // 0

// looks for "value1" starting from index 1 to the right
console.log(arr.indexOf("value1", 1)); // -1

// looks for "value1" starting from index 0 to the left
console.log(arr.lastIndexOf("value1", 0)); // 0

// looks for "value1" starting from index 1 to the left
console.log(arr.lastIndexOf("value1", 1)); // 0
```

---

---

## `.includes()`

`.includes()` looks for an array item starting from a given `index`, and returns `true` or `false`.

```js
const arr = ["value1", "value2", "value3"];

console.log(arr.includes("looked up item", 2)); // false
```

---

---

## `.find()`

`.find()` method returns the **first array item** that meets a given condition, and returns `undefined` otherwise. It gives access to the **array item**, **index** of the item and the **array** itself:

```js
const arr = [1, 2, 3, 4, 5];

const foundItem = arr.find(function (item, index, array) {
  return item < 3;
});

console.log(foundItem); // 1
```

```js
const arr = [1, 2, 3, 4, 5];

const foundItem = arr.find(function (item, index, array) {
  return item > 3;
});

console.log(foundItem); // 4
```

---

---

## `.findIndex()` and `.findLastIndex`

`.findIndex()` method returns **index** that meets a given condition. It gives an access to the **array item**, **index** of the item and the **array** itself. The `findLastIndex` method is like `.findIndex()`, but searches from right to left:

```js
const arr = [1, 2, 3, 4, 3, 2, 1];

const result = arr.findIndex(function (item, index, array) {
  return item === 3;
});

console.log(result); // 2
```

```js
const arr = [1, 2, 3, 4, 3, 2, 1];

const result = arr.findLastIndex(function (item, index, array) {
  return item === 3;
});

console.log(result); // 4
```

---

---

## `.filter()`

`.filter()` method filters the array using the provided condition and returns a new array. It gives an access to the **array item**, **index** of the item and the **array** itself. _It doesn't change the original array_.

```js
const arr = ["value1", "value2", "value3"];

const result = arr.filter(function (item, index, array) {
  return item.startsWith("value") && (item.endsWith("2") || item.endsWith("3"));
});

console.log(result); // ['value2', 'value3']
console.log(arr); // ['value1', 'value2', 'value3']
```

---

---

## `.map()`

`.map()` method applies the provided function on every array item and returns a new array without changing the original one. It gives an access to the **array item**, **index** of the item and the **array** itself.

```js
const arr = ["value1", "value2", "value3"];

const result = arr.map(function (item, index, array) {
  return item + 0;
});

console.log(result); // ['value10', 'value20', 'value30']
```

---

---

## `.sort()`

The `.sort()` method of `Array` instances sorts the elements of an array in place and returns the reference to the same array, now sorted. The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code unit values.

```js
const arr = ["value3", "value1", "value2", 1, 2, 10, 23];

arr.sort();

console.log(arr); // [1, 10, 2, 23, 'value1', 'value2', 'value3']
```

`.sort()` method also accepts a function to compare the items in an array. The return value should be a number that indicates the relative order of the two array items that are compared: negative if `a` is less than `b`, positive if `a` is greater than `b`, and zero if they are equal.

```js
const array = ["value3", "value1", "value2", 1, 23, 10, 2];

// doesn't change the order of string items in the array
array.sort(function (a, b) {
  return a - b;
});

console.log(array); // ['value3', 'value1', 'value2', 1, 2, 10, 23]
```

---

---

## `.toSorted()`

The `.toSorted()` method of Array instances is the copying version of the `.sort()` method. It returns a new array with the elements sorted in ascending order.

```js
const arr = ["value3", "value1", "value2", 1, 2, 10, 23];

// returns new array without modifying the original one
const newArr = arr.toSorted();

console.log(arr); // ['value3', 'value1', 'value2', 1, 2, 10, 23]
console.log(newArr); // [1, 10, 2, 23, 'value1', 'value2', 'value3']
```

---

---

## `.reverse()`

The `.reverse()` method of Array instances reverses an array in place and returns the reference to the same array:

```js
const arr = ["value3", "value1", "value2", 1, 23, 10, 2];

arr.reverse();

console.log(arr); // [2, 10, 23, 1, 'value2', 'value1', 'value3']
```

---

---

## `.toReversed()`

The `.toReversed()` method of Array instances is the copying counterpart of the `.reverse()` method. It returns a new array with the elements in reversed order.

```js
const arr = ["value3", "value1", "value2", 1, 23, 10, 2];

// returns new array without modifying the original one
const newArr = arr.toReversed();

console.log(arr); // ['value3', 'value1', 'value2', 1, 23, 10, 2]
console.log(newArr); // [2, 10, 23, 1, 'value2', 'value1', 'value3']
```

---

---

## `.join()`

`.join()` method accepts a delimeter as an argument and joins the array items with the provided delimeter.

```js
const arr = ["value1", "value2", "value3"];

console.log(arr.join(", ")); // value1, value2, value3
console.log(arr.join("-")); // value1-value2-value3
```

---

---

## `.reduce()`

`.reduce()` method reduces the provided item to a single value:

```js
const arr = [1, 2, 3, 4];

const sum = array.reduce(function (acc, item, index, array) {
  return (acc += item);
}, 0); // 0 is initial value for accumulator

// logs 10 - the sum of all items in the array
console.log(sum);
```

---

---

## `.reduceRight()`

`.reduceRight()` method does the same thing as `.reduce()` but from right to left:

```js
const arr = [1, 2, 3, 4];

array.reduceRight(function (acc, item, index, array) {
  // does the same thing as above but in a descending order
  return (acc += item);
}, 0);

// logs 10 - the sum of all items in the array
console.log(sum);
```

---

---

## Higher order functions and `this`

Almost all array methods that call functions – like `find`, `filter`, `map` with a notable exception of `sort`, accept an optional additional parameter `this`. This parameter determines what `this` refers to inside the callback function:

```js
arr.find(func, thisArg);
arr.filter(func, thisArg);
arr.map(func, thisArg);
```

```js
const user = {
  role: "admin",
};

const people = [
  { name: "Name1", role: "admin" },
  { name: "Name2", role: "user" },
  { name: "Name3", role: "admin" },
];

function func(item, index, array) {
  return item.role === this.role;
}

const result = people.filter(func, user);

console.log(result);
/* 
0: {name: 'Name1', role: 'admin'}
1: {name: 'Name3', role: 'admin'}
*/
```

---

---

## `Array.isArray()`

`Array.isArray()` method returns `true`, if the provided argument is an array, or `false` otherwise:

```js
const arr = [1, 2, 3, 4];

console.log(Array.isArray(arr)); // true
```

---

---

## `.some()`

If a function returns a truthy value, `.some()` immediately returns `true` and stops iterating over the rest of the items:

```js
const arr = [1, 2, 3, 4];

const result = arr.some(function (item, index, array) {
  return item >= 2;
});

// logs true after the first item that met the condition
console.log(result); // true.
```

---

---

## `.every()`

If a function returns a falsy value, `.every()` immediately returns `false` and stops iterating over the rest of the items:

```js
const arr = [1, 2, 3, 4];

const result = arr.every(function (item, index, array) {
  return item <= 1;
});

// logs false after the first item that returned a falsy value
console.log(result); // false.
```

---

---

## `Array.from()`

`Array.from(<obj>)` takes an iterable or array-like value and makes a “real” array from it.

```js
const arrayLike = {
  0: "Hello",
  1: "World",
  length: 2,
};

const arrayFromObject = Array.from(arrayLike);

console.log(arrayFromObject); // ['Hello', 'World']
```

```js
const arrFromStrings = Array.from("Hello");

console.log(arrFromStrings); // ['H', 'e', 'l', 'l', 'o']
```

---

---

## `.fill()`

`.fill(<value> [, <beginning_index>, <ending_index>])` fills the array with a given value.

```js
const arr = [1, 2, 3, 4];

arr.fill(100, 2, 3);
console.log(arr); // [1, 2, 100, 4]

arr.fill(100, 2, 8);
console.log(arr); // [1, 2, 100, 100]

arr.fill(100);
console.log(arr); // [100, 100, 100, 100]
```

---

---

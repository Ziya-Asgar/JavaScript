# Number Methods

- [Number Methods](#number-methods)
  - [`.toFixed()`](#tofixed)
  - [define numbers using `e`](#define-numbers-using-e)
  - [`isNaN()` and `Number.isNaN()`](#isnan-and-numberisnan)
  - [`isFinite()` and `Number.isFinite()`](#isfinite-and-numberisfinite)
  - [`Number.isInteger()`](#numberisinteger)
  - [`parseInt()` and `Number.parseInt()`](#parseint-and-numberparseint)
  - [`parseFloat()` and `Number.parseFloat()`](#parsefloat-and-numberparsefloat)

---

---

## `.toFixed()`

`toFixed([<decimal place>])` method rounds a number to given (optional) decimal places:

```js
const num = 123456.789;

num.toFixed(); // 123457, rounds to 0 decimal places
num.toFixed(2); // 123456.79, rounds to 2 decimal places
```

---

---

## define numbers using `e`

We can define numbers using `e`:

```js
const thousand = 1e3; // same as 1000 (10^3)
const oneThousandth = 1e-3; // same as 1/1000
```

---

---

## `isNaN()` and `Number.isNaN()`

`isNaN()` tells if the provided argument is not a number (`NaN`), after trying to convert the provided argument to a number, if necessary. Returns `true` or `false`:

```js
const num = 123456.789;
const numString = "123456.789";
const halfNum = "45.34tgy6";

isNaN(num); // false. num is a number
isNaN(numString); // false. numString is a number, because isNaN converted it to a number
isNaN(halfNum); // true. halfNum is not a number
isNaN(NaN); // true. NaN is not a number
```

`Number.isNaN()` tells if the provided argument is precisely the value `NaN`. Returns `true` or `false`:

```js
const num = 123456.789;
const numString = "123456.789";
const halfNum = "45.34tgy6";

Number.isNaN(num); // false. num is not NaN
Number.isNaN(numString); // false. numString is not NaN
Number.isNaN(halfNum); // false. halfNum is not NaN
Number.isNaN(NaN); // true. NaN is NaN
```

---

---

## `isFinite()` and `Number.isFinite()`

`isFinite()` tells if a number is finite or not, after trying to convert the provided argument to a number, if necessary. Returns `true` or `false`:

```js
isFinite(15); // true
isFinite("15"); // true
isFinite(NaN); // false
isFinite(Infinity); // false
isFinite(-Infinity); // false
```

`Number.isFinite()` tells if a number is finite or not, without converting the provided argument to a number. It checks that a given value is a number, and the number is neither positive `Infinity`, negative `Infinity`, nor `NaN`:

```js
Number.isFinite(15); // true
Number.isFinite("15"); // false
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
```

---

---

## `Number.isInteger()`

`Number.isInteger()` tells if a provided number is integer or not:

```js
Number.isInteger(123456); // true
Number.isInteger(123456.789); // false
Number.isInteger(NaN); // false
Number.isInteger(Infinity); // false
Number.isInteger(-Infinity); // false
Number.isInteger("10"); // false
Number.isInteger(true); // false
Number.isInteger(false); // false
```

---

---

## `parseInt()` and `Number.parseInt()`

`parseInt()` and `Number.parseInt()` parses a string to an integer. They have the same functionality:

```js
const halfNum = "45.34tgy6";

parseInt("100px"); // 100
parseInt("12.3.4"); // 12
parseInt(halfNum); // 45

Number.parseInt("100px"); // 100
Number.parseInt("12.3.4"); // 12
Number.parseInt(halfNum); // 45
```

---

---

## `parseFloat()` and `Number.parseFloat()`

`parseFloat()` and `Number.parseFloat()` parses a string to a number. They have the same functionality:

```js
const halfNum = "45.34tgy6";

parseFloat("100px"); // 100
parseFloat("12.3.4"); // 12.3
parseFloat(halfNum); // 45.34

Number.parseFloat("100px"); // 100
Number.parseFloat("12.3.4"); // 12.3
Number.parseFloat(halfNum); // 45.34
```

---

---

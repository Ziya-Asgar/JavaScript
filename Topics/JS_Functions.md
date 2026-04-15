# Functions

- [Functions](#functions)
  - [Creating a function](#creating-a-function)
  - [Set a default value to a parameter in a function](#set-a-default-value-to-a-parameter-in-a-function)
  - [Access all arguments of a function](#access-all-arguments-of-a-function)
  - [Using the spread operator inside a function](#using-the-spread-operator-inside-a-function)
  - [Get the number of parameters of a function](#get-the-number-of-parameters-of-a-function)
  - [Returns from a function](#returns-from-a-function)
  - [Copying a function](#copying-a-function)
  - [Add a property to a function from outside](#add-a-property-to-a-function-from-outside)
  - [`setTimeout()` and `clearTimeout()`](#settimeout-and-cleartimeout)
  - [`setInterval()` and `clearInterval()`, and nested `setTimeout()`](#setinterval-and-clearinterval-and-nested-settimeout)
  - [`.call()`, `.apply()`, `.bind()`](#call-apply-bind)
  - [`eval()`](#eval)
  - [Currying](#currying)

---

---

## Creating a function

There are several ways to create a function:

1. This type of creating a function is called a function declaration:

```js
function declaration() {
  console.log(
    `This type of creating a function is called function declaration`,
  );
  // you don't need ; after a function declaration
}

declaration();
```

2. This type of creating a function is called a function expression:

```js
const functionName = function () {
  console.log(
    `This type of creating a function is called a function expression`,
  );
};

functionName();
```

3. This type of function is called an arrow function:

```js
const arrowFunctionName = () =>
  `This type of function is called an arrow function`;

console.log(arrowFunctionName());
```

When an arrow function has a single parameter, it doesn't need parentheses, curly braces, and the `return` statement:

```js
const arrowFunctionWithSingleParameter = (singleParameter) =>
  `${singleParameter} doesn't need parentheses, curly braces, and an explicit return`;

console.log(arrowFunctionWithSingleParameter);
```

A multiline arrow function needs curly braces and the `return` statement:

```js
const multilineArrowFunction = () => {
  // multiline arrow function needs curly braces and an explicit return statement, if we want to return something
  return `something`;
};

console.log(multilineArrowFunction);
```

4. Another way to declare a function is to use `new Function()`:

   ```js
   const functionName = new Function(
     `console.log("this is a code inside the function")`,
   );

   functionName();
   ```

   ```js
   const functionName = new Function(
     "parameter1",
     "parameter2",
     "return parameter1 + parameter2",
   );

   console.log(functionName(1, 2)); // 3
   ```

---

---

## Set a default value to a parameter in a function

We can set a default value to a parameter, when we are creating a function:

```js
function declaration(parameter1, parameterWithDefaultValue = `Default value`) {
  // this parameter will be undefined, if it won't be set while calling the function
  console.log(`parameter1: ${parameter1}`);

  //  - this parameter will have the default value, if nothing is set while calling the function
  console.log(`parameterWithDefaultValue: ${parameterWithDefaultValue}`);
}

declaration();
declaration(10);
declaration(10, 20);
```

---

---

## Access all arguments of a function

We can access all arguments of a function using the spread operator like this:

```js
function threeDots(...args) {
  for (let arg of args) console.log(`${arg} is part of ${args} array`);

  return args;
}

function threeDots2(...anyWord) {
  for (let arg of anyWord) console.log(`${arg} is part of ${anyWord} array`);

  return anyWord;
}

console.log(threeDots(1, 2, 3));
console.log(threeDots2(1, 2, 3));

// both functions log
// 1 is part of 1, 2, 3 array
// 2 is part of 1, 2, 3 array
// 3 is part of 1, 2, 3 array
// finally, both functions return [1, 2, 3] in the end.
```

We can use the `...` operator together with other parameters as well:

```js
function twoParametersAndTheRest(parameter1, parameter2, ...theRest) {
  console.log(
    `Here is parameter1: ${parameter1},\nhere is parameter2: ${parameter2},\nand here are the rest of the parameters: ${theRest}`,
  );

  return theRest;
}

console.log(twoParametersAndTheRest(1, 2, 3, 4, 5));
// logs
// Here is parameter1: 1,
// here is parameter2: 2,
// and here are the rest of the parameters: 3,4,5
// finally, returns [3, 4, 5]
```

---

`arguments` is a keyword to access all the arguments provided to a function:

```js
function accessingAllArguments() {
  console.log(`${arguments} is an array-like object`);
  console.log(`${arguments[0]} is the first argument of the function`);
  console.log(
    `${arguments.length} is the number of arguments called with the function`,
  );
}

accessingAllArguments(1, 2);
// logs
// [object Arguments] is an array-like object
// 1 is the first argument of the function
// 2 is the number of arguments called with the function
```

---

---

## Using the spread operator inside a function

Using the spread operator inside a function, turns an iterable into a list of arguments:

```js
function callWith3Dots(arr) {
  console.log(...arr); // 3 Dots in a function call turns an iterable into a list of arguments
  return Math.max(...arr);
}
callWith3Dots([3, 5, 8]);
// logs 1 2 3
// returns 8
```

---

---

## Get the number of parameters of a function

We can access how many parameters a function has using the `length`:

```js
function functionWith2Parameters(a, b) {}
function functionWithManyParameters(a, b, ...more) {}

console.log(functionWith2Parameters.length); // returns 2
console.log(functionWithManyParameters.length); // still returns 2
```

---

---

## Returns from a function

When a function is not set to return anything explicitly, it returns `undefined`:

```js
function returnsUndefined() {
  // nothing is happening, so function returns undefined
}
```

```js
function returnsUndefined() {
  let a = 0;
  let b = 0;
  a + b;
  // again, function returns undefined
}
```

A function with an empty `return` also returns `undefined`:

```js
function emptyReturnGivesUndefined() {
  return; // returns undefined
}
```

---

---

## Copying a function

Here is a quick way to copy a function:

```js
function func1() {
  console.log(`copied`);
}
const func2 = func1; // both are functions now

func1(); // copied
func2(); // copied
```

---

---

## Add a property to a function from outside

We can also add a property to a function from the outside of the function:

```js
function withExternalProperty() {}

withExternalProperty.addedExternally = `you can add a property to a function from the outside`;

console.log(withExternalProperty.addedExternally);
```

---

---

## `setTimeout()` and `clearTimeout()`

Here is how to use `setTimeout` and `clearTimeout`:

```js
const functionName = function () {
  console.log(`function has run`);
};

const timerId = setTimeout(functionName, 1000); // runs after 1 second (1000 milliseconds)
```

```js
setTimeout(() => {
  console.log(`this also works`);
}, 1000);
```

```js
setTimeout(`console.log("this also works)`, 1000);
```

`clearTimeout` clears the timeout and stops the `setTimeout` from running:

```js
const condition = true;

const timerId = setTimeout(() => {
  console.log(`this function doesn't run`);
}, 1000);

if (condition) {
  clearTimeout(timerId);
}
```

Here is a way to provide arguments to a function used inside `setTimeout`:

```js
const functionName = function (arg1, arg2) {
  console.log(`function has run with arguments: ${arg1} and ${arg2}`);
};

const timerId = setTimeout(functionName, 1000, `argument1`, `argument2`);
```

---

---

## `setInterval()` and `clearInterval()`, and nested `setTimeout()`

Here is how to use `setInterval` and `clearInterval`:

```js
const functionName = function () {
  console.log(`function has run`);
};

const timerId = setInterval(functionName, 2000); // runs every 2 seconds
// not exactly 2 seconds. As it runs more, the call to a function is being delayed
```

`clearInterval` clears the interval and stops the `setInterval` from running:

```js
const functionName = function () {
  console.log(`function has run`);
};

const timerId = setInterval(functionName, 2000); // runs every 2 seconds

// clears the interval after 5 seconds
setTimeout(clearInterval, 5000, timerId);
```

Nested `setTimeout` is more preferred than `setInterval`:

```js
const nestedSetTimeoutId = setTimeout(function tick() {
  console.log(`tick`);
  setTimeout(tick, 2000);
}, 2000); // this works more precisely than setInterval
```

Here is an example of clearing a nested `setTimeout`:

```js
let count = 0;

const timerID = setTimeout(function tick() {
  count++;
  if (count > 3) {
    return;
  }
  console.log(`tick`);
  setTimeout(tick, 1000);
}, 1000);
```

---

---

## `.call()`, `.apply()`, `.bind()`

`.call()` method of the `Function` instance applies `this` keyword to a provided argument:

```js
function func(parameter1) {
  console.log(`${param1}, ${this.name}`);
}

const user = { name: `some name` };

// function.call(setThis, arguments)
func.call(user, "Hi"); // "this" in func now refers to the user object
```

`.apply()` method is similar to `.call()`. But the arguments provided to the function using `.apply()` should be either in an array or an array-like object:

```js
function func(parameter1, parameter2) {
  console.log(this.name + parameter1 + parameter2);
}

const user = { name: `some name` };

// function.apply(setThis, arrayLikeObjectOfArguments);
func.apply(user, [" hi", " bye"]);
```

`.bind()` method binds `this` keyword of a function (or method) to a provided object:

```js
function func() {
  console.log(this.name);
}

const user = { name: `some name` };

// function.bind(this)
const bindUser = func.bind(user);

bindUser(); // logs some name
```

```js
const user = {
  firstName: "John",
  sayHi() {
    alert(`Hello, ${this.firstName}!`);
  },
};

const sayHi = user.sayHi.bind(user);

// can now run it without an object
sayHi(); // Hello, John!

const user2 = {
  firstName: "Jack",
};

const sayHi2 = user.sayHi.bind(user2);

sayHi2(); // Hello, Jack!
```

```js
function test(arg) {
  console.log(this.number, arg);
}

const bindedFn = test.bind({ number: 99 }, "argument");

bindedFn(); // 99, "argument"
```

> Summary:
>
> - `.call()`: binds `this` keyword value, **invokes the function**, and allows you to pass **a list of arguments**.
> - `.apply()`: binds `this` keyword value, **invokes the function**, and allows you to pass arguments as an **array**.
> - `.bind()`: binds `this` keyword value, **returns** a new function, and allows you to pass **a list of arguments**.

---

---

## `eval()`

`eval()` evaluates a code provided to it as a string, and executes it:

```js
eval(`console.log("Hello")`); // Hello
```

`eval` returns the last statement, if more than one statement is provided to it:

```js
const evalReturnsLastValue = eval(`let i = 0; ++i`);
console.log(evalReturnsLastValue); // 1
```

---

---

## Currying

Here is an example of currying:

```js
function add(a) {
  return function (b) {
    return a + b;
  };
}

console.log(add(5)(3)); // 8

let addFive = add(5);

console.log(addFive(3)); // 8
```

---

---

# JavaScript Cheatsheet

<hr>

- [JavaScript Cheatsheet](#javascript-cheatsheet)
  - [Useful Links](#useful-links)
  - [`use strict`](#use-strict)
  - [String Methods](#string-methods)
  - [Number Methods](#number-methods)
  - [Math Object](#math-object)
  - [Type Conversion](#type-conversion)
    - [`String()`](#string)
    - [`Number()`](#number)
      - [`+` operator](#-operator)
    - [`Boolean()`](#boolean)
  - [Conditionals](#conditionals)
  - [Loops](#loops)
  - [Functions](#functions)
  - [Objects](#objects)
  - [Symbols](#symbols)
  - [Arrays](#arrays)
  - [Maps](#maps)
  - [WeakMaps](#weakmaps)
  - [Sets](#sets)
  - [WeakSets](#weaksets)
  - [Destructuring](#destructuring)
  - [Date Object](#date-object)
  - [JSON](#json)
  - [Classes](#classes)
  - [Error Handling](#error-handling)
  - [Promises, async/await](#promises-asyncawait)
  - [Generators](#generators)
  - [Modules](#modules)
  - [DOM](#dom)
  - [DOM Events](#dom-events)
  - [Forms](#forms)
  - [Window object](#window-object)
  - [Fetch](#fetch)
  - [Regular Expressions](#regular-expressions)
  - [URL](#url)
  - [Binary files](#binary-files)

<hr>
<hr>

## Useful Links

- https://javascript.info
- https://developer.mozilla.org
- https://www.smashingmagazine.com/2012/06/all-about-unicode-utf8-character-sets/
- https://blog.hubspot.com/website/what-is-utf-8

<hr>
<hr>

## `use strict`

Strict mode makes several changes to normal JavaScript semantics:

- Eliminates some JavaScript silent errors by changing them to throw errors.
- Fixes mistakes that make it difficult for JavaScript engines to perform optimizations: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
- Prohibits some syntax likely to be defined in future versions of ECMAScript.

To invoke strict mode for an entire script, put the exact statement `"use strict"` before any other statements.

```js
"use strict";
```

<hr>
<hr>

## String Methods

[String Methods](./JS_StringMethods.md)

<hr>
<hr>

## Number Methods

[Number Methods](./JS_NumberMethods.md)

<hr>
<hr>

## Math Object

[Math Object](./JS_MathObject.md)

<hr>
<hr>

## Type Conversion

### `String()`

`String()` turns the provided argument into a string:

```js
typeof String(10); // string
```

### `Number()`

`Number()` turns the provided argument into a number:

```js
typeof Number("10"); // number
```

#### `+` operator

As well as adding numbers, `+` operator, can be used to convert a variable to a number:

```js
typeof +"10"; // number
```

### `Boolean()`

`Boolean()` turns the provided argument to either `true` or `false`:

```js
Boolean(" "); // true
Boolean(""); // false
```

<hr>
<hr>

## Conditionals

[Conditionals](./JS_Conditionals.md)

<hr>
<hr>

## Loops

[Loops](./JS_Loops.md)

<hr>
<hr>

## Functions

[Functions](./JS_Functions.md)

<hr>
<hr>

## Objects

[Objects](./JS_Objects.md)

<hr>
<hr>

## Symbols

[Symbols](./JS_Symbols.md)

<hr>
<hr>

## Arrays

[Arrays](./JS_Arrays.md)

<hr>
<hr>

## Maps

[Maps](./JS_Maps.md)

<hr>
<hr>

## WeakMaps

[WeakMaps](./JS_WeakMaps.md)

<hr>
<hr>

## Sets

[Sets](./JS_Sets.md)

<hr>
<hr>

## WeakSets

[WeakSets](./JS_WeakSets.md)

<hr>
<hr>

## Destructuring

[Destructuring](./JS_Destructuring.md)

<hr>
<hr>

## Date Object

[Date Object](./JS_Date_Object.md)

<hr>
<hr>

## JSON

[JSON](./JS_JSON.md)

<hr>
<hr>

## Classes

[Classes](./JS_Classes.md)

<hr>
<hr>

## Error Handling

[Error Handling](./JS_ErrorHandling.md)

<hr>
<hr>

## Promises, async/await

[Promises](./JS_Promises.md)

<hr>
<hr>

## Generators

[Generators](./JS_Generators.md)

<hr>
<hr>

## Modules

[Modules](./JS_Modules.md)

<hr>
<hr>

## DOM

[DOM](./JS_DOM.md)

<hr>
<hr>

## DOM Events

[Dom Events](./JS_DomEvents.md)

<hr>
<hr>

## Forms

[Forms](./JS_Forms.md)

<hr>
<hr>

## Window object

[Window object](./JS_WindowObject.md)

<hr>
<hr>

## Fetch

[Fetch](./JS_Fetch.md)

<hr>
<hr>

## Regular Expressions

[Regular Expressions](./JS_RegularExpressions.md)

<hr>
<hr>

## URL

[URL](./JS_URL.md)

<hr>
<hr>

## Binary files

[Binary files](./JS_BinaryFiles.md)

<hr>
<hr>

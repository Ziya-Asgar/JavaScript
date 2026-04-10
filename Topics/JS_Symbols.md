# Symbols

- [Symbols](#symbols)
  - [Create a `Symbol()`](#create-a-symbol)
  - [`description` property](#description-property)
  - [Converting symbols to a string](#converting-symbols-to-a-string)
  - [Symbols in an object literal](#symbols-in-an-object-literal)
  - [Symbol properties and looping](#symbol-properties-and-looping)
  - [`Object.getOwnPropertySymbols()`](#objectgetownpropertysymbols)
  - [`Object.assign()` and symbols](#objectassign-and-symbols)
  - [`Symbol.for()`](#symbolfor)
  - [`Symbol.keyFor()`](#symbolkeyfor)

---

## Create a `Symbol()`

Here is how to create a `Symbol()`.

```JS
const id = Symbol();

console.log(id); // Symbol()
```

<hr>

Note that 2 different symbols do not equal each other, even if they have the same description:

```js
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1); // Symbol(id)
console.log(id2); // Symbol(id)

console.log(id1 == id2); // false
console.log(id1 === id2); // false
```

<hr>

## `description` property

All symbols have the `description` property:

```js
const id = Symbol("test");

console.log(id.description); // test
```

<hr>

## Converting symbols to a string

To convert the symbols to a string, we can either use the `String()` function or call `.toString()` method on them:

```js
const id = Symbol("id");

console.log(String(id)); // Symbol(id)
console.log(id.toString()); // Symbol(id)
```

<hr>

## Symbols in an object literal

If we want to use a symbol in an object literal `{...}`, we need square brackets around it:

```js
const id = Symbol("id");

const obj = {
  name: "SomeName",
  [id]: 123,
};

console.log(obj); // {name: 'some name', Symbol(id): 123}
```

<hr>

## Symbol properties and looping

Symbolic properties do not participate in the `for...in` loop and `Object.keys()` also ignores them:

```js
const id = Symbol("id");

const obj = {
  name: "SomeName",
  [id]: 123,
};

for (key in obj) {
  console.log(key);
} // name

console.log(Object.keys(obj)); // ['name']
```

<hr>

## `Object.getOwnPropertySymbols()`

There is a built-in method `Object.getOwnPropertySymbols(<obj>)` that allows us to get all symbols of an object.

```js
const id = Symbol("id");

const obj = {
  name: "SomeName",
  [id]: 123,
};

console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(id)]
```

<hr>

## `Object.assign()` and symbols

`Object.assign()` copies both string and symbol properties:

```js
const id = Symbol("id");

const obj = {
  name: "SomeName",
  [id]: 123,
};

const copyWithSymbols = Object.assign({}, obj);

console.log(copyWithSymbols[id]); // 123
```

<hr>

## `Symbol.for()`

As we’ve seen, usually all symbols are different, even if they have the same description. But sometimes we want the symbols with the same description to be the same entities. To achieve that, there exists a global symbol registry. In order to read (create if absent) a symbol from the registry, use `Symbol.for(<key>)`.

```js
// creates id Symbol in the global registry
const idGlobal = Symbol.for("id");

// reads the same Symbol as the above line
const idGlobal2 = Symbol.for("id");

console.log(idGlobal === idGlobal2); //true
```

<hr>

## `Symbol.keyFor()`

`Symbol.for(<key>)` returns a symbol by description. To do the opposite – to return a description by a global symbol – we can use `Symbol.keyFor(<sym>)`:

```js
// get (or create) a symbol by name
const sym = Symbol.for("name");
const sym2 = Symbol.for("id");

// get name by symbol
console.log(Symbol.keyFor(sym)); // name
console.log(Symbol.keyFor(sym2)); // id
```

<hr>
<hr>

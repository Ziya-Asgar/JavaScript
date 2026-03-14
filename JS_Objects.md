# Objects

- [Objects](#objects)
  - [Creating an object](#creating-an-object)
  - [Object keys and values, and accessing them](#object-keys-and-values-and-accessing-them)
  - [Delete a key-value pair](#delete-a-key-value-pair)
  - [Test if a property exists in an object](#test-if-a-property-exists-in-an-object)
  - [Looping through object](#looping-through-object)
  - [Copy an object](#copy-an-object)
    - [`Object.assign()`](#objectassign)
    - [`structuredClone()`](#structuredclone)
  - [optional chaining `?.`](#optional-chaining-)
  - [`Object.fromEntries()`](#objectfromentries)
  - [`Object.keys()` and `Object.values()`](#objectkeys-and-objectvalues)
  - [`Object.entries()`](#objectentries)
  - [`Object.getOwnPropertyDescriptor()`](#objectgetownpropertydescriptor)
  - [`Object.getOwnPropertyDescriptors()`](#objectgetownpropertydescriptors)
  - [`Object.defineProperty`](#objectdefineproperty)
  - [`Object.defineProperties`](#objectdefineproperties)
  - [Copy an object together with all of its properties' flags](#copy-an-object-together-with-all-of-its-properties-flags)
  - [`Object.preventExtension()` and `Object.isExtensible()`](#objectpreventextension-and-objectisextensible)
  - [`Object.seal()` and `Object.isSealed()`](#objectseal-and-objectissealed)
  - [`Object.freeze()` and `Object.isFrozen()`](#objectfreeze-and-objectisfrozen)
  - [Accessor properties](#accessor-properties)
  - [Set the prototype of an object](#set-the-prototype-of-an-object)
  - [Add a method to a native prototype](#add-a-method-to-a-native-prototype)
  - [`.isPrototypeOf()`](#isprototypeof)
  - [Looping and prototypes](#looping-and-prototypes)
    - [`.hasOwnProperty()`](#hasownproperty)
    - [`Object.getOwnPropertyNames()`](#objectgetownpropertynames)

---

## Creating an object

This way of creating an object is called "object constructor" syntax:

```js
const obj = new Object();
```

This way of creating an object is called "object literal" syntax:

```js
const obj = {};
```

<hr>

Here is an example of creating an object with a custom constructor function:

```js
function ConstructorFunction(name) {
  this.name = name;
  this.someProperty = "someProperty";
}

const obj = new ConstructorFunction("some name");

console.log(obj); // ConstructorFunction {name: 'some name', someProperty: 'someProperty'}
console.log(typeof obj); // object
```

<hr>

## Object keys and values, and accessing them

Objects consist of key-value pairs separated with a colon. If object keys have more than one word, they need to be written in quotes:

```js
const obj = {
  name: "some name",
  surname: "some surname",
  "multi-word property": "some value",
};
```

<hr>

To get the value of an object property, we can use the below ways:

```js
const obj = {
  name: "some name",
  surname: "some surname",
  "multi-word property": "some value",
};

obj.name;
obj["name"];
obj["multi-word property"];
```

<hr>

We can also use string concatenation while referring to or creating an object property:

```js
const obj = {
  name: "some name",
  surname: "some surname",
  "multi-word property": "some value",
};

const multi = "multi-";
obj[multi + "word property"];
```

```js
const prop = "property";
const obj = {
  [prop + "Name"]: "some value",
};

console.log(obj["propertyName"]);
```

<hr>

Instead of writing `name: name` in an object, we can simply write `name`:

```js
const name = "some name";

const obj = {
  name, // same as name:name
  age: 30,
};
```

```js
const obj = {
  name, // same as name: ""
  age: 30,
};
```

<hr>

## Delete a key-value pair

To delete a key-value pair from an object, we use `delete`:

```js
const obj = {
  name,
  age: 30,
};

console.log(obj); // {name: '', age: 30}

delete obj.name;

console.log(obj); // {age: 30}
```

<hr>

## Test if a property exists in an object

Here is one way to test if a property exists in an object:

```js
const obj = {
  name,
  age: 30,
};

console.log("name" in obj); // true

delete obj.name;

console.log("name" in obj); // false
```

<hr>

## Looping through object

Here is one way to loop through an object's keys and values:

```js
const obj = {
  name: "some name",
  age: 30,
};

for (let key in obj) {
  console.log(`${key}: ${obj[key]}`);
}
```

<hr>

## Copy an object

Here is one way to copy an object:

```js
const obj = {
  name: "some name",
  age: 30,
};

const copyOfObj = {};

for (let key in obj) {
  copyOfObj[key] = obj[key];
}
```

### `Object.assign()`

`Object.assign()` accepts an object as a first argument, and copies all the properties of other objects given to it, into the first argument:

```js
const obj = {
  name: "some name",
  age: 30,
};

const copyOfObj = {};

Object.assign(copyOfObj, obj, {
  "key in another object": "some value",
});
```

### `structuredClone()`

The global `structuredClone()` method creates a deep copy of an object. If there is a nested object this function copies the nested object as well, and not just a reference to that nested object. It copies together with all the nested objects, and properties, except functions:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const copyOfObj = structuredClone(obj);
```

<hr>

## optional chaining `?.`

The optional chaining `?.` syntax constructor is like the `.` chaining operator, except that instead of causing an error if a reference is nullish (`null` or `undefined`), the expression returns `undefined`.

- We can use `?.` for safely reading and deleting, but not writing.
- When used with function calls, it returns `undefined`, if the given function does not exist.
- The variable before `?.` must be declared. Otherwise, if there’s no variable at all, then `?.` also triggers an error.

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

// console.log(obj.fullName.surname); // this would cause an error
console.log(obj.fullName?.surname); // undefined

// returns undefined even though obj.func() doesn't exist
console.log(obj.func?.()); // undefined

const anotherObj = null;

// console.log(anotherObj.someProp); // this would cause an error
console.log(anotherObj?.someProp); // undefined
```

<hr>

## `Object.fromEntries()`

Given an array that consists of arrays that have key-value pairs (`[key, value]`), `Object.fromEntries()` creates an object:

```js
const objFromArr = Object.fromEntries([
  ["some property", 1],
  ["another property", 4],
]);
```

We can also create an object from a Map using `Object.fromEntries()`:

```js
const map = new Map();
map.set("property1", 1);
map.set("property2", "value 2");

const obj = Object.fromEntries(map); // create an object from a map

// this also works
console.log(map.entries()); // map iterator
const obj2 = Object.fromEntries(map.entries());
```

<hr>

## `Object.keys()` and `Object.values()`

`Object.keys()` returns an array of object keys. `Object.values()` returns an array of object values:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.keys(obj); // returns an array of keys
Object.values(obj); // returns an array of values
```

These 2 methods provide another way for us to loop through an object. Here is an example of looping through an object's values:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

for (let value of Object.values(obj)) {
  console.log(value); // loop over values
}
```

<hr>

## `Object.entries()`

`Object.entries()` returns an array that includes arrays consisting of key-value pairs:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.entries(obj); // returns an array of [key, value] pairs.
```

<hr>

## `Object.getOwnPropertyDescriptor()`

The method `Object.getOwnPropertyDescriptor()` allows to query the full information about an object's property, including its flags:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const descriptor = Object.getOwnPropertyDescriptor(obj, "name");
```

## `Object.getOwnPropertyDescriptors()`

The method `Object.getOwnPropertyDescriptors()` allows to query the full information about **all** the properties of an object, including their flags:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const allDescriptors = Object.getOwnPropertyDescriptors(obj);
```

<hr>

## `Object.defineProperty`

To change the flags of an object's property, we can use the `Object.defineProperty()` method:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.defineProperty(obj, "name", {
  value: "new name",

  writable: true,

  enumerable: false, // Non-enumerable properties are excluded from Object.keys, and for...in

  configurable: true,
  // Non-configurable property can’t be deleted, its attributes can’t be modified.
  // Making a property non-configurable is a one-way road.
  // configurable: false prevents changes of property flags and its deletion, while allowing to change its value.
});
```

If we define a new property with `Object.defineProperty`, by default, all the flags will be false. We need to explicitly list which flag is true.

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.defineProperty(obj, "newProp", {
  value: "new property",
  writable: true,
});
```

## `Object.defineProperties`

To change the flags of several properties at once, we can use `Object.defineProperties`:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

Object.defineProperties(obj, {
  name: { value: "new name", writable: false, enumerable: true },
  surname: { value: "new surname", writable: false, configurable: true },
});
```

<hr>

## Copy an object together with all of its properties' flags

Previous methods provide a new way for us to copy an object. To copy an object together with all of its properties' flags, we can use the below code:

```js
const obj = {
  name: "name",
  sizes: {
    height: 182,
    width: 50,
  },
};

const copyOfObjectWithFlags = Object.defineProperties(
  {},
  Object.getOwnPropertyDescriptors(obj),
);
```

<hr>

## `Object.preventExtension()` and `Object.isExtensible()`

`Object.preventExtension()` prevents the addition of new properties to an object:

```js
Object.preventExtensions(obj);
```

We can check if we can add properties to an object using `Object.isExtensible()`:

```js
Object.isExtensible(obj);
```

## `Object.seal()` and `Object.isSealed()`

`Object.seal()` forbids adding or removing properties. This means that it sets `configurable: false` for all existing properties.

```js
Object.seal(obj);
```

We can check if an object is sealed, using `Object.isSealed()`:

```js
Object.isSealed(obj);
```

## `Object.freeze()` and `Object.isFrozen()`

`Object.freeze()` forbids adding, removing, and changing properties. This means that it sets `configurable: false`, and `writable: false` for all existing properties.

```js
Object.freeze(obj);
```

We can check if an object is frozen using `Object.isFrozen()`:

```js
Object.isFrozen(obj);
```

<hr>

## Accessor properties

Accessor properties are essentially functions that execute on getting and setting a value, but look like regular properties to an external code. In an object literal they are denoted by `get` and `set`:

```js
const objectWithAccessorProperties = {
  name: "John",
  surname: "Doe",

  get fullName() {
    return `${this.name} ${this.surname}`;
  },

  // setter must have exactly one parameter
  set fullName(value) {
    [this.name, this.surname] = value.split(" ");
  },
};

// using the getter
console.log(objectWithAccessorProperties.fullName); // John Doe

// using the setter
objectWithAccessorProperties.fullName = "differentName differentSurname";

// using the getter
console.log(objectWithAccessorProperties.fullName); // differentName differentSurname
```

Note that while using the `defineProperty` method on accessor properties, there is no `value` or `writable`:

```js
const objectWithAccessors = {
  name: "name",
  surname: "surname",
};

Object.defineProperty(objectWithAccessors, "fullName", {
  // For accessor properties, there is no value or writable,
  // but instead there are get and set functions.
  get() {
    return `${this.name} ${this.surname}`;
  },

  set(value) {
    [this.name, this.surname] = value.split(" ");
  },
});

console.log(objectWithAccessors.fullName); // name surname

obj.fullName = "differentName differentSurname";
console.log(obj.fullName); // differentName differentSurname
```

<hr>

## Set the prototype of an object

We can set the prototype of an object with the `__proto__`. Here are 2 ways to do that:

```js
// Object that will be used as a prototype
const Prototype1 = {
  prototypeProp: "prototypeValue",
};

const ChildOfPrototype1 = {
  childProp: "childValue",
};

// Set the Prototype1 object as the prototype
ChildOfPrototype1.__proto__ = Prototype1;

// child object inherits the property from Prototype1
console.log(ChildOfPrototype1.prototypeProp); // prototypeValue

// Another way to set the Prototype_1 object as the prototype
const anotherChildOfPrototype1 = {
  anotherChildProp: "anotherChildValue",
  __proto__: Prototype1,
};

// Property from the Prototype1 can now be accessed in the child object
console.log(anotherChildOfPrototype1.prototypeProp); // prototypeValue
```

<hr>

Here is another way to set the prototype of an object:

```js
// Object that will be used as a prototype
const Prototype1 = {
  prototypeProp: "prototypeValue",
};

function ConstructorFunction(name) {
  this.name = name;
}

// Set the Prototype1 object as the prototype
ConstructorFunction.prototype = Prototype1;
const obj = new ConstructorFunction("new name");

console.log(obj.prototypeProp); // true
```

<hr>

We can create a new object and provide a prototype for it using the `Object.create()` method:

```js
// Object that will be used as a prototype
const Prototype1 = {
  prototypeProp: "prototypeValue",
};

// creates an object with the prototype Prototype_1
const obj = Object.create(Prototype1, {
  objProp: {
    value: "objValue",
    writable: false,
  },
});

console.log(obj.objProp); // objValue
console.log(obj.prototypeProp); // prototypeValue
```

`Object.setPrototypeOf()` helps to set the prototype of an object:

```js
// Objects that will be used as a prototype
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Prototype2 = {
  prototypeProp2: "prototypeValue2",
};

const obj = {};

// Set the Prototype1 as the prototype of obj
Object.setPrototypeOf(obj, Prototype1);
console.log(obj.prototypeProp1); // prototypeValue1

// change the prototype of obj to Prototype2
Object.setPrototypeOf(obj, Prototype2);
console.log(obj.prototypeProp1); // undefined
console.log(obj.prototypeProp2); // prototypeValue2
```

The `Object.getPrototypeOf()` static method returns the prototype (i.e. the value of the internal `[[Prototype]]` property) of the specified object:

```js
// Objects that will be used as a prototype
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Prototype2 = {
  prototypeProp2: "prototypeValue2",
};

const obj = {};

// Set the Prototype1 as the prototype of obj
Object.setPrototypeOf(obj, Prototype1);
console.log(Object.getPrototypeOf(obj)); // {prototypeValue1: 'prototypeValue1'}

// change the prototype of obj to Prototype2
Object.setPrototypeOf(obj, Prototype2);
console.log(Object.getPrototypeOf(obj)); // {prototypeValue2: 'prototypeValue2'}
```

Combining `Object.create()`, `Object.getPrototypeOf()`, and `Object.getOwnPropertyDescriptors()` helps us to copy an object with all of its properties and descriptors:

```js
// Object that will be used as a prototype
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const obj = {};

// Set the Prototype1 as the prototype of obj
Object.setPrototypeOf(obj, Prototype1);
console.log(Object.getPrototypeOf(obj)); // {prototypeValue1: 'prototypeValue1'}

const powerfulCopyOfObj = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(Prototype1),
);

console.log(Object.getPrototypeOf(powerfulCopyOfObj)); // {prototypeValue1: 'prototypeValue1'}
```

<hr>

## Add a method to a native prototype

Here is how we can add a method to a native prototype:

```js
String.prototype.newMethodToNativePrototype = function () {
  return `this adds a method to the native String prototype`;
};

console.log("any string".newMethodToNativePrototype());
// this adds a method to the native String prototype
```

<hr>

## `.isPrototypeOf()`

There’s also a method `objA.isPrototypeOf(objB)`, that returns `true`, if `objA` is somewhere in the chain of prototypes for `objB`.

```js
// Objects that will be used as a prototype
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Prototype2 = {
  prototypeProp2: "prototypeValue2",
};

const Prototype3 = {
  prototypeProp3: "prototypeValue3",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Prototype2, Prototype1);
Object.setPrototypeOf(Child1, Prototype2);

console.log(Prototype2.isPrototypeOf(Child1)); // true
console.log(Prototype1.isPrototypeOf(Child1)); // true

console.log(Prototype3.isPrototypeOf(Child1)); // false
```

<hr>

## Looping and prototypes

`Object.keys` only returns own keys of an object:

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

console.log(Object.keys(Child1)); // ['childProp1']
```

`for ... in` loop loops over both own and inherited keys (from a prototype) of an object:

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

for (let key in Child1) {
  console.log(key); // childProp1 prototypeProp1
}
```

### `.hasOwnProperty()`

`hasOwnProperty()` accepts property as an argument and returns `true`, if the property is own, not an inherited one:

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

for (let key in Child1) {
  // returns true if the property is own property, not an inherited one
  console.log(key, Child1.hasOwnProperty(key));
  // childProp1 true
  // prototypeProp1 false
}
```

<hr>

### `Object.getOwnPropertyNames()`

`Object.getOwnPropertyNames()` returns all own property names in an array:

```js
const Prototype1 = {
  prototypeProp1: "prototypeValue1",
};

const Child1 = {
  childProp1: "childValue1",
};

Object.setPrototypeOf(Child1, Prototype1);

console.log(Object.getOwnPropertyNames(Child1)); // ['childValue1']
```

<hr>
<hr>

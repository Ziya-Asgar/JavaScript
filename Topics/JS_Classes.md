# Classes

- [Classes](#classes)
  - [Define a class and create objects based on a class](#define-a-class-and-create-objects-based-on-a-class)
  - [Classes are functions](#classes-are-functions)
  - [Named class expressions](#named-class-expressions)
  - [getters/setters, and computed properties in classes](#getterssetters-and-computed-properties-in-classes)
  - [Class fields](#class-fields)
  - [Class inheritance](#class-inheritance)
  - [Override a method in a parent class](#override-a-method-in-a-parent-class)
  - [Extend the method in a parent class](#extend-the-method-in-a-parent-class)
  - [Static methods and properties](#static-methods-and-properties)
  - [Protected properties](#protected-properties)
  - [Private properties](#private-properties)
  - [Extend built-in classes](#extend-built-in-classes)
  - [`instanceof`](#instanceof)
  - [Mixin](#mixin)

---

---

## Define a class and create objects based on a class

We use the `class` keyword to define a new class, and then use that class with the `new` keyword to create a new object based on that class:

```js
class ClassName {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log(`Hi, ${this.name}`);
  }
}

new ClassName("test").sayHi(); // Hi, test

// create an object based on ClassName
const obj = new ClassName("Ziya");

obj.sayHi(); // Hi, Ziya
```

<hr>

## Classes are functions

A class is actually a function in JavaScript:

```js
class ClassName {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log(this.name);
  }
}

console.log(typeof ClassName); // function
```

<hr>

## Named class expressions

Similar to Named Function Expressions, class expressions may have a name.

If a class expression has a name, the name used with the `class` keyword is visible inside the class only:

```js
// "Named Class Expression"
// (no such term in the spec, but that's similar to Named Function Expression)
const User = class MyClass {
  sayHi() {
    console.log(MyClass); // MyClass name is visible only inside the class
  }
};

new User().sayHi();
/* logs 
class MyClass {
  sayHi() {
    console.log(MyClass); // MyClass name is visible only inside the class
  }
} */

console.log(MyClass); // error, MyClass name isn't visible outside of the class
```

<hr>

## getters/setters, and computed properties in classes

Just like literal objects, classes may include getters/setters, computed properties etc. These are helpful because they let us have more control.

```js
class User {
  constructor(name) {
    // this code invokes the setter function below
    this.name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    if (value.length < 4) {
      console.log("Name is too short.");
      return;
    }
    this._name = value;
  }
}

let user = new User("John");
console.log(user.name); // John

user = new User(""); // Name is too short.
```

Note that we have used underscore in getter and setter functions, while referring to a variable. This is because if we don't use underscore, and refer to `this.name`, we will trigger the setter function, which will try to set the `name`, which will further trigger the setter function, causing endless loop.

<hr>

## Class fields

In the past, our classes only had methods. “Class fields” is a syntax that allows to add any properties:

```js
class User {
  name = "Some Name";

  sayHi() {
    console.log(`Hello, ${this.name}!`);
  }
}

new User().sayHi(); // Hello, Some Name!
```

<hr>

When a class is created, its methods are stored in the prototype. So, `class User {...}` would store its methods in the `User.prototype`. The important difference of class fields is that they are set on individual objects, not `User.prototype`:

```js
class User {
  name = "Some Name";

  sayHi() {
    console.log(`Hi, ${this.name}`);
  }
}

const user = new User();
console.log(user.name); // Some Name
console.log(User.prototype.name); // undefined
console.log(User.prototype.sayHi); // function sayHi()

console.log(user.name === User.prototype.name); // false
console.log(user.sayHi === User.prototype.sayHi); // true
```

<hr>

## Class inheritance

Class inheritance is a way for one class to extend another class. So we can create a new functionality on top of the existing one. We use the `extends` keyword for this:

```js
class Parent {
  constructor(name) {
    this.name = name + ` this is a parent class`;
  }
  parentMethod() {
    console.log(`hi from parent`);
  }
}

class Child extends Parent {
  childMethod() {
    console.log(`hi from child`);
  }
}

const child = new Child();

child.childMethod(); // hi from child

// the parent method is also available in the Child class, as the Child extends the Parent class
child.parentMethod(); // hi from parent
```

## Override a method in a parent class

We can also override a method in a parent class:

```js
class Parent {
  constructor(name) {
    this.name = name + ` this is a parent class`;
  }
  method() {
    console.log(`This will be overridden`);
  }
}

class Child extends Parent {
  method() {
    console.log(`Child method overrode the parent method`);
  }
}

const child = new Child();

child.method(); // Child method overrode the parent method
```

## Extend the method in a parent class

What if we don't want to override the parent method, but to extend the functionality of it. We can use `super.<method>` to call the method and then add more functionality to it:

```js
class Parent {
  constructor(name) {
    this.name = name + ` this is a parent class`;
  }
  sayHi() {
    console.log(`hi from parent`);
  }
}

// super.method(...) to call a parent method.
class Child extends Parent {
  bye() {
    console.log(`bye from child`);
  }

  sayBye() {
    super.sayHi();
    this.bye();
  }
}

const child = new Child();
child.sayBye(); // hi from parent, bye from child
```

Constructors in **inheriting classes** must call `super(...)` before using `this`.

```js
class Animal {
  constructor(name) {
    this.speed = 0;
    this.name = name;
  }

  // ...
}

class Rabbit extends Animal {
  constructor(name, earLength) {
    // super(...) to call a parent constructor (inside our constructor only).
    super(name);
    this.earLength = earLength;
  }

  // ...
}

const rabbit = new Rabbit("White Rabbit", 10);

console.log(rabbit.speed); // 0
console.log(rabbit.name); // White Rabbit
console.log(rabbit.earLength); // 10
```

<hr>

## Static methods and properties

We can also assign a method to the class that won't be inherited by objects. Such methods are called **static**. Usually, static methods are used to implement functions that belong to the class as a whole, but not to any particular object of it. Static methods and properties are inherited by extended classes. In a class declaration, they are prepended by `static` keyword like this:

```js
class User {
  static staticMethod() {
    console.log(`this is a STATIC method in the User class constructor`);
  }
}

class User2 extends User {
  method() {
    console.log(`this is a method in the User2 class constructor`);
  }
}

User.staticMethod(); // this is a STATIC method in the User class constructor
User2.staticMethod(); // this is a STATIC method in the User class constructor

const user = new User();
// this throws an error
user.staticMethod();
```

Static properties are also possible, they look like regular class properties, but prepended by the keyword `static`:

```js
class User {
  static prop = "Some Name";
}

class User2 extends User {
  method() {
    console.log(`this is a method in the User2 class constructor`);
  }
}

console.log(User.prop); // Some Name
console.log(User2.prop); // Some Name

const user = new User();
console.log(user.prop); // undefined
```

<hr>

## Protected properties

We can have **protected properties** in classes. Protected properties are usually prefixed with an underscore `_`. Here is an example of a protected property. Here we control that the `wateramount` is not below zero:

```js
class CoffeeMachine {
  constructor(power) {
    this.power = power;
  }

  _waterAmount = 0;

  set waterAmount(value) {
    this._waterAmount += value;
    if (this._waterAmount < 0) {
      this._waterAmount = 0;
    }
  }

  get waterAmount() {
    return this._waterAmount;
  }
}

// create the coffee machine
const coffeeMachine = new CoffeeMachine(100);

// add water
coffeeMachine.waterAmount = -10; // _waterAmount will become 0, not -10
```

<hr>

It sometimes happens that a property must be set at creation time only, and then never be modified. To do so, we only need to make a getter, but not a setter. Here the `power` property becomes read-only:

```js
class CoffeeMachine {
  constructor(power) {
    this._power = power;
  }

  get power() {
    return this._power;
  }
}

// create the coffee machine
const coffeeMachine = new CoffeeMachine(100);
console.log(`Power is: ${coffeeMachine.power}W`); // Power is: 100W

coffeeMachine.power = 25; // Error (no setter)
```

But most of the time `get...`/`set...` functions are preferred to be like this:

```js
class CoffeeMachine {
  constructor(power) {
    this._power = power;
  }

  getPower() {
    return this._power;
  }

  _waterAmount = 0;

  setWaterAmount(value) {
    this._waterAmount += value;
    this._waterAmount < 0 ? (this._waterAmount = 0) : this._waterAmount;
  }

  getWaterAmount() {
    return this._waterAmount;
  }
}

const coffeeMachine = new CoffeeMachine(100);
console.log(coffeeMachine.getPower());

coffeeMachine.setWaterAmount(-1000);
console.log(coffeeMachine.getWaterAmount());
```

<hr>

## Private properties

There are also private properties. Privates should start with `#`. They are only accessible from inside the class.

```js
class CoffeeMachine {
  #waterLimit = 200;

  _waterAmount = 0;

  #fixWaterAmount(value) {
    this._waterAmount += value;

    this._waterAmount < 0 ? (this._waterAmount = 0) : this._waterAmount;
    this._waterAmount > this.#waterLimit
      ? (this._waterAmount = this.#waterLimit)
      : this._waterAmount;

    return this._waterAmount;
  }

  setWaterAmount(value) {
    this._waterAmount = this.#fixWaterAmount(value);
  }

  getWaterAmount() {
    return this._waterAmount;
  }
}

const coffeeMachine = new CoffeeMachine();

coffeeMachine.setWaterAmount(100);
console.log(coffeeMachine.getWaterAmount()); // 100

coffeeMachine.setWaterAmount(-100);
console.log(coffeeMachine.getWaterAmount()); // 0

coffeeMachine.setWaterAmount(300);
console.log(coffeeMachine.getWaterAmount()); // 200

// can't access privates from outside of the class
coffeeMachine.#fixWaterAmount(13); // Error
coffeeMachine.#waterLimit = 1000; // Error
```

<hr>

## Extend built-in classes

We can add more functionality to the built-in classes like Array, Map and others using the `extends` keyword.

```js
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }
}

const arrClass = new PowerArray(1, 2, 3, 4, 5);
console.log(arrClass.isEmpty()); // false
```

<hr>

## `instanceof`

The `instanceof` operator allows to check whether an object belongs to a certain class. It also takes inheritance into account.

```js
class Rabbit {}
const rabbit = new Rabbit();

// is it an object of Rabbit class?
console.log(rabbit instanceof Rabbit); // true
```

It also works with constructor functions instead of classes.

```js
function Rabbit() {}

console.log(new Rabbit() instanceof Rabbit); // true
```

It also works with built-in classes like Array:

```js
const arr = [1, 2, 3];

console.log(arr instanceof Array); // true
```

<hr>

## Mixin

A **mixin** is a class, containing methods that can be used by other classes, without a need to inherit from it.

```js
const sayHiMixin = {
  sayHi() {
    console.log(`Hello ${this.name}`);
  },
  sayBye() {
    console.log(`Bye ${this.name}`);
  },
};

// usage:
class User {
  constructor(name) {
    this.name = name;
  }
}

// copy the methods
Object.assign(User.prototype, sayHiMixin);

// now User can say hi
new User("someone").sayHi(); // Hello, someone
```

<hr>
<hr>

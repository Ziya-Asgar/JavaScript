# Modules

- [Modules](#modules)
  - [`import.meta`](#importmeta)
  - [`this` in modules](#this-in-modules)
  - [Browser-specific differences of scripts with `type="module"`](#browser-specific-differences-of-scripts-with-typemodule)
  - [Fallback for old browsers](#fallback-for-old-browsers)
  - [Exporting and importing variables](#exporting-and-importing-variables)
    - [`export` while declaring a variable](#export-while-declaring-a-variable)
    - [`export` after declaring a variable](#export-after-declaring-a-variable)
    - [`import` by name](#import-by-name)
    - [`import` everything at once](#import-everything-at-once)
    - [`import` under different names](#import-under-different-names)
    - [`export` under different names](#export-under-different-names)
  - [`export default`](#export-default)
  - [Re-export](#re-export)
  - [Dynamic imports](#dynamic-imports)

---

---

- A module is a javascript file.
- Modules always work in strict mode.
- Each module has its own top-level scope. In other words, top-level variables and functions from a module are not seen in other scripts. Modules should `export` what they want to be accessible from outside and `import` what they need.

---

---

## `import.meta`

The object `import.meta` contains the information about the current module.

Its content depends on the environment. In the browser, it contains the URL of the script, or a current webpage URL if inside HTML:

```html
<script type="module">
  console.log(import.meta.url); // script URL
  // for an inline script - the URL of the current HTML-page
</script>
```

If you are using the `import.meta` inside a JS file, make sure that the `script` tag, within the html file, referring to the JS file include `type="module"`. Otherwise, an error will pop up saying "Cannot use `'import.meta'` outside a module.

---

---

## `this` in modules

In a module, top-level `this` is undefined. In non-module scripts, `this` is a global object:

```html
<script>
  console.log(this); // window
</script>

<script type="module">
  console.log(this); // undefined
</script>
```

---

---

## Browser-specific differences of scripts with `type="module"`

There are several browser-specific differences of scripts with `type="module"` compared to regular scripts.

- Module scripts are always deferred, same effect as `defer` attribute, for both external and inline scripts.
  - downloading external module scripts `<script type="module" src="...">` doesn’t block HTML processing, they load in parallel with other resources.
  - module scripts wait until the HTML document is fully ready, and then run.
  - relative order of scripts is maintained: scripts that go first in the document, execute first.

```html
<script type="module">
  const button = document.querySelector("button");
  console.log(button);
  // as modules are deferred, the script runs after the whole page is loaded
</script>
<button id="button">Button</button>
```

Compare to regular script below:

```html
<script>
  const button = document.querySelector("button");
  console.log(button);
  // button is null, the script can't see elements below
  // regular scripts run immediately, before the rest of the page is processed
</script>

<button id="button">Button</button>
```

- For non-module scripts, the `async` attribute only works on external scripts. Async scripts run immediately when ready, independently of other scripts or the HTML document. For module scripts, it works on inline scripts as well.

---

---

## Fallback for old browsers

Old browsers do not understand `type="module"`. Scripts of an unknown type are just ignored. For them, it’s possible to provide a fallback using the `nomodule` attribute:

```html
<script type="module">
  console.log("Runs in modern browsers");
</script>

<script nomodule>
  console.log(
    "Modern browsers know both type=module and nomodule, so skip this",
  );
  console.log(
    "Old browsers ignore script with unknown type=module, but execute this.",
  );
</script>
```

---

---

## Exporting and importing variables

### `export` while declaring a variable

We can label any declaration as exported, by placing `export` before it, be it a variable, function or a class.

```js
// module.js

// export an array
export const numbers = [1, 2, 3, 4, 5];

// export a constant
export const simpleVar = "simpleVar";

// export a class
export class ClassName {
  constructor(name) {
    this.name = name;
  }
}
```

### `export` after declaring a variable

We can put `export` after declaring the variable, as well.

```js
// module.js
function sayHi(user) {
  console.log(`Hello, ${user}`);
}

function sayBye(user) {
  console.log(`Bye, ${user}`);
}

export { sayHi, sayBye }; // a list of exported variables
```

### `import` by name

In the above example, the exports are called named exports, as the variables were not default exported. To import named exports, we can put a list of what to import in curly braces in `import {...}`, like this:

```js
// index.js
// index.js should have type="module" in the script tag of the html file that downloads it
import { sayHi, sayBye } from "./say.js";

sayHi("Ziya"); // Hello, Ziya!
sayBye("Ziya"); // Bye, Ziya!
```

### `import` everything at once

If there’s a lot to import, we can import everything as an object using `import * as <obj>`, for instance:

```js
// index.js
import * as obj from "./module.js";

obj.sayHi("Ziya");
obj.sayBye("Ziya");
```

### `import` under different names

We can also use `as` to import under different names.

```js
// index.js
import { sayHi as hi, sayBye as bye } from "./module.js";

hi("Ziya");
bye("Ziya");
```

### `export` under different names

We can also use `as` to export under different names:

```js
// module.js
function sayHi(user) {
  console.log(`Hello, ${user}`);
}

function sayBye(user) {
  console.log(`Bye, ${user}`);
}

export { sayHi as hi, sayBye as bye };
```

After the above change, now `hi` and `bye` could be used in imports:

```js
// index.js
import * as say from "./module.js";

say.hi("Ziya"); // Hello, Ziya!
say.bye("Ziya"); // Bye, Ziya!
```

---

---

## `export default`

Sometimes, it's preferred to export one entity in a module rather than several variables. Modules provide a special `export default` (“the default export”) syntax to make the “one thing per module” way look better. There may be only one `export default` per file.

You can put `export default` before the entity to export:

```js
// module.js
export default class ClassName {
  constructor(name) {
    this.name = name;
  }
}
```

The default exports could be imported without curly braces:

```js
// index.js
import ClassName from "./module.js"; // not {ClassName}, just ClassName

const className = new ClassName("Name");
console.log(className.name);
```

**Note: `import` needs curly braces for named exports and doesn’t need them for the default one.**

As there may be at most one default export per file, the exported entity may have no name.

```js
// module.js
export default class {
  // no class name
  constructor(name) {
    this.name = name;
  }
}
```

```js
// module.js
export default function (user) {
  // no function name
  console.log(`Hello, ${user}!`);
}
```

```js
// module.js
export default ["Jan", "Feb", "Mar", "Apr", "Aug", "Sep", "Oct", "Nov", "Dec"]; // no array name
```

<hr>

`default` keyword could be used to export a variable after it's declaration:

```js
// module.js
function sayHi(user) {
  console.log(`Hello, ${user}!`);
}

// same as if we added "export default" before the function
export { sayHi as default };
```

If a file exports one “default” item, and a few named ones, we can import the default export along with a named one:

```js
// module.js
export default class User {
  constructor(name) {
    this.name = name;
  }
}

export function sayHi(user) {
  console.log(`Hello, ${user}!`);
}
```

This is how we would import the above exports:

```js
// index.js
import { default as ClassName, sayHi } from "./module.js";

console.log(new ClassName("Ziya").name);
sayHi("test");
```

If we import everything with `*` as an object, then the `default` property is exactly the default export:

```js
// index.js
import * as obj from "./module.js";

const ClassName = obj.default; // the default export
console.log(new ClassName("Ziya").name);
```

---

---

## Re-export

“Re-export” syntax `export ... from ...` allows to import things and immediately export them:

```js
export { sayHi } from "./module.js"; // re-export sayHi
export { default as ClassName } from "./module.js"; // re-export default
```

`export ... from ...` is just a shorter form of the below way of importing and exporting:

```js
// import default as ClassName and export it
import ClassName from "./module.js";
export { ClassName };
```

The notable difference of `export ... from` compared to `import`/`export` is that re-exported modules aren’t available in the current file. So inside the above file, we can’t use the `sayHi` function.

We need to be careful about using `export ... from` with a default export.

- `export ClassName from './module.js'` won’t work. We need to use `export {default as ClassName}`
- `export * from './module.js'` re-exports only named exports, but ignores the default one. If we’d like to re-export both named and default exports, then two statements are needed:

```js
export * from "./module.js"; // to re-export named exports
export { default } from "./module.js"; // to re-export the default export
```

---

---

## Dynamic imports

The `import()` syntax, also called dynamic import, is an expression that allows loading an ECMAScript module asynchronously and dynamically. The `import()` call is a syntax that closely resembles a function call, but `import` itself is a keyword, not a function (You cannot assign it to a variable the way you could do with a function).

The import declaration syntax (`import something from "somewhere"`) is static and will always result in the imported module being evaluated at load time. Dynamic imports allow to load a module conditionally or on demand. Use dynamic import only when necessary. The static form is preferable for loading initial dependencies, and can benefit more readily from static analysis tools and tree shaking.

If a file is referenced in an HTML file, but it doesn't have the script tag `type="module"`, then you can't use static import declaration but the asynchronous dynamic import syntax will always be available, allowing you to import modules even into non-module environments.

The `import(<module>)` expression loads the module and **returns a promise** that resolves into a module object that contains all its exports.

```js
import * as mod from "/module.js";

import("/module.js").then((mod2) => {
  console.log(mod === mod2); // true
});
```

The dynamic import syntax allows to use importing with an `if` statement. As it returns a promise, we need to use `await` with it, inside an `async` function.

```js
const condition = true;

(async () => {
  if (condition) {
    const mod = await import("./module.js");
    console.log(mod);
  }
})();
```

To dynamically import a default export, we need to use `default` keyword. For example, here we destructure and assign a different name to a default export:

```js
const condition = true;

(async () => {
  if (condition) {
    const { default: myDefault } = await import("./module.js");
    console.log(myDefault);
  }
})();
```

---

---

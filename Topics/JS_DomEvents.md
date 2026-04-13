# DOM Events

- [DOM Events](#dom-events)
  - [Pointer events](#pointer-events)
    - [Pointer event properties](#pointer-event-properties)
    - [Capturing pointer id](#capturing-pointer-id)
  - [Mouse events](#mouse-events)
    - [The properties of mouse events](#the-properties-of-mouse-events)
  - [Keyboard events](#keyboard-events)
  - [`<form>` element events](#form-element-events)
  - [`transitionend`](#transitionend)
  - [Clipboard events](#clipboard-events)
  - [Scroll events](#scroll-events)
  - [`input` and `change` events](#input-and-change-events)
  - [Ways to assign an event handler](#ways-to-assign-an-event-handler)
  - [`this` in the DOM event](#this-in-the-dom-event)
  - [Properties of the event object](#properties-of-the-event-object)
  - [Preventing the default event action](#preventing-the-default-event-action)
  - [Custom events](#custom-events)
  - [Events that come from real user actions](#events-that-come-from-real-user-actions)
  - [Document and resource loading](#document-and-resource-loading)
    - [`DOMContentLoaded`](#domcontentloaded)
    - [`load`](#load)
    - [`unload`](#unload)
    - [`beforeunload`](#beforeunload)
    - [`async`, `defer`](#async-defer)
    - [Tracking the loading scripts and other external resources](#tracking-the-loading-scripts-and-other-external-resources)

---

---

## Pointer events

Pointer event is newer and should be used instead of mouse events.

| Pointer event        | Similar mouse event |
| -------------------- | ------------------- |
| `pointerdown`        | `mousedown`         |
| `pointerup`          | `mouseup`           |
| `pointermove`        | `mousemove`         |
| `pointerover`        | `mouseover`         |
| `pointerout`         | `mouseout`          |
| `pointerenter`       | `mouseenter`        |
| `pointerleave`       | `mouseleave`        |
| `pointercancel`      | -                   |
| `gotpointercapture`  | -                   |
| `lostpointercapture` | -                   |

```html
<body>
  <section style="border: 1px solid red; height: 100px;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");
    const button = document.querySelector("button");

    button.addEventListener("pointerdown", () => {
      console.log("clicked the button");
    });

    button.addEventListener("pointerup", () => {
      console.log("ended clicking the button");
    });

    section.addEventListener("pointerover", () => {
      console.log(
        "hovering over the section. Happens each time when you bring the cursor over the section. Even if you hover over the element within the section and then over the section itself",
      );
    });

    section.addEventListener("pointermove", () => {
      console.log(
        "moving the cursor within the section, including the elements within the section",
      );
    });

    section.addEventListener("pointerout", () => {
      console.log("out from the section");
    });

    section.addEventListener("pointerenter", () => {
      console.log(
        "enter into the section. Happens each time when you get the cursor into the section. Unlike, 'pointerover' doesn't fire when you enter the section, then hover over the element within the section, and then hover over the section again",
      );
    });

    section.addEventListener("pointerleave", () => {
      console.log("left the section");
    });
  </script>
</body>
```

### Pointer event properties

Pointer events have the same properties as mouse events plus others:

- `pointerId` – the unique identifier of the pointer causing the event.
- `pointerType` – the pointing device type. Must be a string, one of: “mouse”, “pen” or “touch”.
- `isPrimary` – is `true` for the primary pointer (the first finger in multi-touch).
- `width` – the width of the area where the pointer (e.g. a finger) touches the device. Where unsupported, e.g. for a mouse, it’s always 1.
- `height` – the height of the area where the pointer touches the device. Where unsupported, it’s always 1.
- `pressure` – the pressure of the pointer tip, in range from 0 to 1. For devices that don’t support pressure must be either 0.5 (pressed) or 0.
- `tangentialPressure` – the normalized tangential pressure.
- `tiltX`, `tiltY`, `twist` – pen-specific properties that describe how the pen is positioned relative the surface.

```html
<body>
  <section style="border: 1px solid red; height: 100px;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");
    const button = document.querySelector("button");

    button.addEventListener("pointerdown", (event) => {
      console.log("clicked the button");
      console.log(event.pointerId);
      console.log(event.pointerType);
    });
  </script>
</body>
```

### Capturing pointer id

`<element>.setPointerCapture(pointerId)` binds events with the given `pointerId` to `<element>`. In other words, `<element>.setPointerCapture(pointerId)` retargets all subsequent events with the given `pointerId` to `<element>`.

`<element>.releasePointerCapture(pointerId)` removes the binding.

---

---

## Mouse events

Mouse events:

- `click`
- `dblclick`
- `contextmenu`
- `mousedown`
- `mouseup`
- `mouseover`
- `mousemove`
- `mouseout`
- `mouseenter`
- `mouseleave`

```html
<body>
  <section style="border: 1px solid red; height: 100px;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");
    const button = document.querySelector("button");

    button.addEventListener("mousedown", () => {
      console.log("clicked the button");
    });

    button.addEventListener("mouseup", () => {
      console.log("ended clicking the button");
    });

    section.addEventListener("mouseover", () => {
      console.log(
        "hovering over the section. Happens each time when you bring the cursor over the section. Even if you hover over the element within the section and then over the section itself",
      );
    });

    section.addEventListener("mousemove", () => {
      console.log(
        "moving the cursor within the section, including the elements within the section",
      );
    });

    section.addEventListener("mouseout", () => {
      console.log("out from the section");
    });

    section.addEventListener("mouseenter", () => {
      console.log(
        "enter into the section. Happens each time when you get the cursor into the section. Unlike, 'mouseover' doesn't fire when you enter the section, then hover over the element within the section, and then hover over the section again",
      );
    });

    section.addEventListener("mouseleave", () => {
      console.log("left the section");
    });
  </script>
</body>
```

### The properties of mouse events

There is a `button` property that indicates which button was clicked. This property only guarantees to indicate which buttons are pressed during events caused by pressing or releasing one or multiple buttons. Here is a table of its outputs:

| Button state              | `event.button` |
| ------------------------- | -------------- |
| Left button (primary)     | 0              |
| Middle button (auxiliary) | 1              |
| Right button (secondary)  | 2              |
| X1 button (back)          | 3              |
| X2 button (forward)       | 4              |

```html
<body>
  <section style="border: 1px solid red; height: 100px;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");
    const button = document.querySelector("button");

    button.addEventListener("mouseup", (event) => {
      switch (event.button) {
        case 0:
          console.log("Left click");
          break;
        case 2:
          console.log("Right click");
          break;
      }
    });
  </script>
</body>
```

All mouse events include the information about pressed modifier keys. For example:

- `event.shiftKey` - Shift
- `event.altKey` - Alt (or Opt for Mac)
- `event.ctrlKey` - Ctrl
- `event.metaKey` - Cmd for Mac

```js
<body>

  <section style="border: 1px solid red; height: 100px; background-color: aliceblue;" height="200px"></section>

  <script src="./index.js"></script>
  <script>

    const section = document.querySelector("section")

    section.addEventListener("mousedown", (event) => {
      if (event.shiftKey) {
        console.log(`shift key was pressed`)
      } else if (event.altKey) {
        console.log(`alt key was pressed`)
      } else if (event.ctrlKey) {
        console.log(`ctrl key was pressed`)
      } else if (event.metaKey) {
        console.log(`meta key was pressed`)
      } else {
        console.log(`some other key was pressed`)
      }
    })

  </script>
</body>
```

For `mouseover` event, we have these properties:

- `event.target` - the element where the mouse came over.
- `event.relatedTarget` - the element from which the mouse came (`relatedTarget` → `target`).

For `mouseout`, event, we have these properties:

- `event.target` - the element that the mouse left.
- `event.relatedTarget` - the new under-the-pointer element, that mouse left for (`target` → `relatedTarget`).

```js
<body>

  <section style="border: 1px solid red; height: 100px; background-color: aliceblue;" height="200px"></section>

  <script src="./index.js"></script>
  <script>

    const section = document.querySelector("section")

    section.addEventListener("mouseover", (event) => {
      console.log("mouseover - event.target:", event.target)
      console.log("mouseover - event.relatedTarget:", event.relatedTarget)
    })

    section.addEventListener("mouseout", (event) => {
      console.log("mouseout - event.target:", event.target)
      console.log("mouseout - event.relatedTarget:", event.relatedTarget)
    })

  </script>
</body>
```

`mouseenter` and `mouseleave` properties have 2 important differences:

- Transitions inside the element, to/from descendants, are not counted.
- Events `mouseenter`/`mouseleave` do not bubble.

---

---

## Keyboard events

Here are keyboard events and their event properties:

- `keydown`
- `keyup`

- `event.key` - allows to get the character.
- `event.code` - allows to get the “physical key code”.

```js
<body>

  <script src="./index.js"></script>
  <script>

    document.body.addEventListener("keydown", (event) => {
      console.log("keydown:", event.key)
      console.log("keydown:", event.code)
    })

    document.body.addEventListener("keyup", (event) => {
      console.log("keyup:", event.key)
      console.log("keyup:", event.code)
    })

  </script>
</body>
```

---

---

## `<form>` element events

Here are `<form>` element events:

- `submit`
- `focus`
- `blur` – when the element loses the focus
- `focusin` and `focusout` events – exactly the same as `focus`/`blur`, but they bubble.

<br>

- Events `focus` and `blur` do not bubble, but propogate down during the capture phase.
- Methods `<element>.focus()` and `<element>.blur()` set/unset the focus on the element.
- `<form>.submit()` submits the form
- `focusin` and `focusout` events must be assigned using `addEventListener`.

```js
<body>

  <section>
    <form action="">
      <label for="name">Name</label>
      <input type="text" id="name">
    </form>

  </section>

  <script src="./index.js"></script>
  <script>

    const section = document.querySelector("section")
    const form = document.querySelector("form")

    console.log(form.elements[0])

    form.addEventListener("submit", (event) =>{
      event.preventDefault()
      console.log("form submitted")
    })

    form.elements[0].addEventListener("focus", (event) => {
      console.log("input is focused")
    })

    form.elements[0].addEventListener("focusin", (event) => {
      console.log("input is focused (this doesn't bubble)")
    })

    form.elements[0].addEventListener("blur", (event) => {
      console.log("input lost the focus")
    })

    form.elements[0].addEventListener("focusout", (event) => {
      console.log("input lost the focus (this doesn't bubble)")
    })

    const randomNum = Math.floor(Math.random() * 2)

    if (randomNum) {
      setTimeout(() => {
        form.submit()
        // if randomNum is 1, the form is submitted automatically and the page gets reloaded
        console.log(`the form was submitted automatically`)
      }, 500)
    }

    setTimeout(() => {
      console.log(`focused automatically`)
      form.elements[0].focus()
    }, 1000)

    setTimeout(() => {
      console.log(`lost the focus automatically`)
      form.elements[0].blur()
    }, 2000)

  </script>
</body>
```

---

---

## `transitionend`

`transitionend` event is fired when a CSS transition has completed. If the `transitioncancel` event is fired, the `transitionend` event will not fire.

```html
<head>
  <style>
    section {
      background-color: aquamarine;
      height: 200px;
    }

    section:hover {
      background-color: bisque;
      transition: background-color 1s;
    }
  </style>
</head>
<body>
  <section></section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");

    section.addEventListener("transitionend", () => {
      console.log("transition ended");
    });
  </script>
</body>
```

---

---

## Clipboard events

There are also some Clipboard events:

- `cut`
  - If the user attempts a cut action on uneditable content, the `cut` event still fires but the event object contains no data.
- `copy`
- `paste`

For the `paste` event the handler can get the access to data using the `<event>.clipboardData.getData('text/plain')` method.

A handler for `cut` and `copy` events can modify the clipboard contents by calling `setData(<format>, <data>)`. The handler cannot read the clipboard data. A handler for this event can modify the clipboard contents by calling `<event>.clipboardData.setData('text/plain')`.

```html
<body>
  <section>
    <p>
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Aperiam,
      dignissimos enim itaque exercitationem, cum rem voluptatibus soluta, magni
      ratione delectus laborum ut provident fugit quos. Reprehenderit iste
      consequatur consequuntur fugiat.
    </p>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");

    section.addEventListener("copy", (event) => {
      // If you want to set data yourself, you need to call `event.preventDefault()`
      event.preventDefault();

      // We are manually adding "Any text" to the clipboard
      event.clipboardData.setData("text/plain", "Any text");
      console.log("copied");
    });

    section.addEventListener("cut", (event) => {
      // Nothing will be added to clipboard as we are cutting on uneditable content
      console.log("cut");
    });

    section.addEventListener("paste", (event) => {
      console.log("pasted:", event.clipboardData.getData("text/plain"));
    });
  </script>
</body>
```

---

---

## Scroll events

- The `scroll` event fires when the document view has been scrolled.
- The `scrollend` event fires when scrolling has completed.

```html
<body>
  <section>
    <p>
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Aperiam,
      dignissimos enim itaque exercitationem, cum rem voluptatibus soluta, magni
      ratione delectus laborum ut provident fugit quos. Reprehenderit iste
      consequatur consequuntur fugiat.
    </p>
  </section>
  <section id="section2" style="overflow: scroll; max-height: 100px;">
    <p>Section 2</p>
    <p>
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Aperiam,
      dignissimos enim itaque exercitationem, cum rem voluptatibus soluta, magni
      ratione delectus laborum ut provident fugit quos. Reprehenderit iste
      consequatur consequuntur fugiat.
    </p>
  </section>

  <script src="./index.js"></script>
  <script>
    const section = document.querySelector("section");
    const section2 = document.querySelector("#section2");

    for (let paragraphs = 0; paragraphs <= 10; paragraphs++) {
      section.append(section.firstElementChild.cloneNode(true));
    }

    document.addEventListener("scroll", () => {
      console.log("document was scrolled");
    });

    document.addEventListener("scrollend", () => {
      console.log("document scroll ended");
    });

    section2.addEventListener("scrollend", () => {
      console.log("section scroll ended");
    });
  </script>
</body>
```

---

---

## `input` and `change` events

Here are some more events:

- `input`
  - The `input` event fires when the value of an `<input>`, `<select>`, or `<textarea>` element has been changed as a direct result of a user action.
- `change`
  - The `change` event is fired for `<input>`, `<select>`, and `<textarea>` elements when the user modifies the element's value. Unlike the `input` event, the `change` event is not necessarily fired for each alteration to an element's value.

```html
<body>
  <section>
    <input type="text" />
  </section>

  <script src="./index.js"></script>
  <script>
    const input = document.querySelector("input");

    input.addEventListener("change", () => {
      console.log("changed to:", input.value);
    });

    input.addEventListener("input", () => {
      console.log("input:", input.value);
    });
  </script>
</body>
```

---

---

## Ways to assign an event handler

There are several ways to assign an event handler:

- assign in HTML with an attribute `on<event>` (for example, `onclick`, `onkeydown`, etc.)

  ```js
  <body>

    <section>
      <input value="Click me" onclick="console.log('Click!')" type="button">
    </section>

    <script src="./index.js"></script>
  </body>
  ```

- assign using the DOM property `on<event>`

  ```js
  <body>

    <section>
      <input value="Click me" type="button">
    </section>

    <script src="./index.js"></script>
    <script>

      const input = document.querySelector("input")

      let clickCount = 0

      input.onclick = function(event) {
        if (clickCount >= 2) {
          input.onclick = null
        }

        console.log("click")
        clickCount++;
      }

    </script>
  </body>
  ```

- The best way to add a handler is `<element>.addEventListener(<event>, <handler>, [options])`. With this method, we can assign more than one handler to the same event and element.

  ```js
  <body>

    <section>
      <input value="Click me" type="button">
    </section>

    <script src="./index.js"></script>
    <script>

      const input = document.querySelector("input")

      function handler() {
        console.log("clicked");
      }

      input.addEventListener("click", handler);

      input.addEventListener("click", handler, { capture: true }); // if false the event bubbles
      input.addEventListener("click", handler, true); // same as the above

      // signals the browser that the handler is not going to call `event.preventDefault()`
      input.addEventListener("click", handler, { passive: true });

      // To remove a handler
      input.removeEventListener("click", handler);

    </script>
  </body>
  ```

- You can also assign an object or a class as an event handler. If an object or a class is assigned as a handler, when the event fires, their `handleEvent` method will be run.

  ```js
  <body>

    <section>
      <input value="Click me" type="button">
    </section>

    <script src="./index.js"></script>
    <script>
      const input = document.querySelector("input")

      const objForDOM = {
        handleEvent(event) {
          console.log(event.type + " event on ", event.currentTarget)
        }
      }

      input.addEventListener("click", objForDOM)

    </script>
  </body>
  ```

  ```js
  class ClassForDOM {
      handleEvent(event) {
        switch(event.type) {
          case 'mousedown':
            <element>.innerHTML = "Mouse button pressed";
            break;
          case 'mouseup':
            <element>.innerHTML += "...and released.";
            break;
        }
      }
  }

  const classForDOM = new ClassForDOM();
  <element>.addEventListener('mousedown', classForDOM);
  ```

---

---

## `this` in the DOM event

In the DOM event, the value of `this` is the element that has the handler for the event.

```js
<body>

  <section style="height: 200px; background-color: aquamarine;">
    <button>Button</button>
  </section>

  <script src="./index.js"></script>
  <script>

    const section = document.querySelector("section")
    const button = document.querySelector("button")

    section.addEventListener("click", function (event) {
      console.log(this);
      // <section style="height: 200px; background-color: aquamarine;">
    })

    button.addEventListener("click", function (event) {
      console.log(this);
      // <button>
    })

  </script>
</body>
```

---

---

## Properties of the event object

Event object has several useful properties:

- `event.currentTarget` - Element that has the handler. The same as `this`.
- `event.target` – the “target” element that initiated the event
- `event.type`
- `event.clientX`
- `event.clientY`
- `event.eventPhase` - tells the number of the phase on which the event was caught. This number represents the phase that the event is in:
  - none (`0`),
  - capture (`1`),
  - target (`2`),
  - bubbling (`3`).

`<event>.stopPropagation()` stops bubbling of an event. `event.stopImmediatePropagation()` stops bubbling and no other handler on the element runs.

```js
<body>

  <section style="height: 200px; background-color: aquamarine;">
    <button id="button1">Button</button>
    <button id="button2">Button</button>
  </section>

  <script src="./index.js"></script>
  <script>

    const section = document.querySelector("section")
    const button1 = document.querySelector("#button1")
    const button2 = document.querySelector("#button2")

    section.addEventListener("click", function (event) {
      console.log("section: currentTarget", event.currentTarget)
      console.log("section: target", event.target)
      console.log("section: type", event.type)
      console.log("section: clientX", event.clientX)
      console.log("section: clientY", event.clientY)
      console.log("section: eventPhase", event.eventPhase)
    })

    button1.addEventListener("click", function (event) {
      console.log("button: currentTarget", event.currentTarget)
      console.log("button: target", event.target)
      console.log("button: type", event.type)
      console.log("button: clientX", event.clientX)
      console.log("button: clientY", event.clientY)
      console.log("button: eventPhase", event.eventPhase)
    })

    button2.addEventListener("click", function (event) {
      event.stopPropagation()
      console.log("button: currentTarget", event.currentTarget)
      console.log("button: target", event.target)
      console.log("button: type", event.type)
      console.log("button: clientX", event.clientX)
      console.log("button: clientY", event.clientY)
      console.log("button: eventPhase", event.eventPhase)
    })

  </script>
</body>
```

---

---

## Preventing the default event action

We can use 2 ways to tell the browser to stop its default action:

- `<event>.preventDefault()`
- and if `on<event>` attribute or `on<event>` property was used then `"return false;"` would work
- `<event>.defaultPrevented` is `true` if an action was prevented.

```html
<body>
  <section style="height: 200px; background-color: aquamarine;">
    <a
      href="https://developer.mozilla.org"
      onclick="console.log('prevented the default behaviour.');return false; "
    >
      Link 1
    </a>
    <a id="link2" href="https://developer.mozilla.org">Link 2</a>
    <a href="https://developer.mozilla.org">Link 3</a>
  </section>

  <script src="./index.js"></script>
  <script>
    link2.addEventListener("click", (event) => {
      event.preventDefault();
      console.log("prevented the default behaviour.", event.defaultPrevented);
    });
  </script>
</body>
```

---

---

## Custom events

We can also generate our own custom events. Custom events can only be used with `<element>.addEventListener`. After an event object is created, we should “run” it on an element using `<element>.dispatchEvent(<Event>)`:

```html
<body>
  <section style="height: 200px; background-color: aquamarine;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const button = document.querySelector("button");

    // new Event(type[, options]);
    const someEvent = new Event("some event type", {
      bubbles: false,
      cancelable: false,
    });

    button.addEventListener("some event type", () => {
      console.log("custom event");
    });

    // Event runs after a second
    setTimeout(() => {
      button.dispatchEvent(someEvent);
    }, 1000);
  </script>
</body>
```

Instead of using `new Event`, we can use the `CustomEvent`. `CustomEvent` is better because it has an additional property `detail`, that we can use for a custom information.

```html
<body>
  <section style="height: 200px; background-color: aquamarine;">
    <button>Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const button = document.querySelector("button");

    const someEvent = new CustomEvent("some event type", {
      bubbles: false,
      cancelable: false,
      detail: { name: "Some Name" },
    });

    button.addEventListener("some event type", (event) => {
      console.log("custom event");
      console.log(event.detail);
    });

    // Event runs after a second
    setTimeout(() => {
      button.dispatchEvent(someEvent);
    }, 1000);
  </script>
</body>
```

---

Instead of using `new Event`, we should create specific type of events:

- `UIEvent`
- `FocusEvent`
- `MouseEvent`
- `WheelEvent`
- `KeyboardEvent`

Using specific events allows to specify some event-specific properties:

```js
const someMouseEvent = new MouseEvent("click", {
  bubbles: true,
  cancelable: true,
  clientX: 100,
  clientY: 100,
});
```

---

---

## Events that come from real user actions

`event.isTrusted` is `true` for events that come from real user actions.

```html
<body>
  <section style="height: 200px; background-color: aquamarine;">
    <button id="button">Click</button>
  </section>

  <script src="./index.js"></script>
  <script>
    const button = document.querySelector("button");

    const newMouseEvent = new MouseEvent("click", {
      bubbles: true,
      cancelable: true,
      clientX: 100,
      clientY: 100,
    });

    setTimeout(() => {
      button.dispatchEvent(newMouseEvent);
    }, 1000);

    button.addEventListener("click", (event) => {
      // when a user clicks, `true` is logged
      console.log(event.isTrusted);
    });
  </script>
</body>
```

---

---

## Document and resource loading

The lifecycle of an HTML page has three important events:

- `DOMContentLoaded` – the browser fully loaded HTML, and the DOM tree is built, but external resources like pictures `<img>` and stylesheets may not yet have loaded.
- `load` – not only HTML is loaded, but also all the external resources: images, styles etc.
- `beforeunload`/`unload` – the user is leaving the page

### `DOMContentLoaded`

`DOMContentLoaded` is a document level event and works only with `addEventListener`.

If there is a script tag in an html document, the `DOMContentLoaded` would fire after that script tag runs.

```js
<script>
  document.addEventListener("DOMContentLoaded", () => {
    console.log("DOM is ready!");
  });
</script>

<script>
  console.log("This comes before DOMContentLoaded");
</script>
```

There are two exceptions to this rule:

- Scripts with the `async` attribute, don’t block `DOMContentLoaded`.
- Scripts that are generated dynamically with `document.createElement('script')` and then added to the webpage also don’t block this event.

One more thing to remember is that `DOMContentLoaded` doesn't wait for an external stylesheet to load. However, if the link to an external stylesheet comes before a script tag, then as `DOMContentLoaded` has to wait for the script tags to load, it would fire after an external stylesheet loads.

### `load`

The `load` event on the `window` object triggers when the whole page is loaded including styles, images and other resources. This event is available via the `onload` property.

### `unload`

When a visitor leaves the page, the `unload` event triggers on `window`.

### `beforeunload`

If a visitor initiated navigation away from the page or tries to close the window, the `beforeunload` handler asks for additional confirmation.

The `event.preventDefault()` doesn’t work from a `beforeunload` handler.

### `async`, `defer`

When the browser loads HTML and comes across a `<script>...</script>` tag or a `<script src="..."></script>` tag, it has to execute the scripts and only after that, load the rest of the page. This means that scripts can block the DOM from being loaded. This also means that if a script tag is placed in a wrong spot, it won't be able to detect certain elements on a page, because DOM gets to be loaded after those scripts are executed.

There are two `<script>` attributes that solve the problem.

The `defer` attribute tells the browser not to wait for the script. Instead, the browser will continue to process the HTML, build DOM. The script loads “in the background”, and then runs when the DOM is fully built.

In other words:

- Scripts with `defer` never block the page.
- Scripts with `defer` always execute when the DOM is ready (but before `DOMContentLoaded` event).

If there is more than one script that has the `defer` attribute, they will be loaded in their relative order, just like regular scripts.

The `defer` attribute is only for external scripts. Hence, if the `<script>` tag has no `src`, `defer` won't work.

The `async` attribute means that a script is completely independent. Other scripts don’t wait for `async` scripts, and `async` scripts don’t wait for them. `DOMContentLoaded` and `async` scripts don’t wait for each other. `async` scripts load in the background and run when ready.

Just like `defer`, the `async` attribute is ignored if the `<script>` tag has no `src`.

Dynamic scripts behave as `async` by default. This is how to add a script dynamically:

```js
const script = document.createElement("script");
script.src = "/someScript.js";
document.body.append(script);
```

If we use `script.async=false`, then scripts will be executed in the document order, just like `defer`.

### Tracking the loading scripts and other external resources

We can track if the loading of some external resources were successful or not using two events:

- `onload` – successful load,
- `onerror` – an error occurred.

---

---

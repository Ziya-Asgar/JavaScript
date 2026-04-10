# Forms

- [Forms](#forms)
  - [`document.forms`](#documentforms)
  - [`form.elements`](#formelements)
  - [`<fieldset>`](#fieldset)
  - [`<element>.form`](#elementform)
  - [`<select>` element](#select-element)
    - [`<option>`](#option)
  - [submit a form to a server manually](#submit-a-form-to-a-server-manually)

---

---

## `document.forms`

`document.forms` is a named and ordered collection that lets us access the `<form>` element:

```html
<form name="formName">
  <input name="one" value="1" />
  <input name="two" value="2" />
</form>

<script src="./index.js"></script>
<script>
  // the form with name="formName"
  console.log(document.forms.formName);

  // the first form in the document
  console.log(document.forms[0]);
</script>
```

<hr>

## `form.elements`

There is `form.elements` which helps us access any form element:

```html
<form name="formName">
  <input name="one" value="1" />
  <input name="two" value="2" />
</form>

<script src="./index.js"></script>
<script>
  console.log(document.forms.formName.elements);
  console.log(document.forms.formName.elements["one"]);
</script>
```

<hr>

When there are multiple elements with the same name, then `<form>.elements["<nameOfTheFormElement>"]` is a collection as well. In that case, we can access elements like this: `<form>.elements.<nameOfTheFormElement>[0]`.

<hr>

## `<fieldset>`

`<fieldset>` elements inside a form have their own `.elements` collection as well.

```js
<form>.elements.<someFieldsetName>.elements.<someNameInTheFieldset>;
<form>.elements.<someFieldsetName>.elements[0];
```

<hr>

## `<element>.form`

If we access an element in the form, we can get the form through the element. For any element, the form is available as `<element>.form`.

Here are some ways to manipulate form elements:

```js
document.forms[0].elements.input.value = "New value";
document.forms[0].elements.textarea.value = "New text";
document.forms[0].elements.input.checked = true; // for a checkbox or radio button
```

<hr>

## `<select>` element

A `<select>` element has 3 important properties:

- `select.options` - the collection of `<option>` subelements,
- `select.value` - the value of the currently selected `<option>`,
- `select.selectedIndex` - the number of the currently selected `<option>`.

### `<option>`

Option elements have their own properties:

- `option.selected` - Is the option selected.
- `option.index` - The number of the option among the others in its `<select>`.
- `option.text` - Text content of the option (seen by the visitor).

Here is how to manipulate the `<option>` element within the `<select>`:

```js
select.options[0].selected = true;
select.value = "some value for first option that to be selected";
```

```js
select.selectedIndex = 0;
select.value = "some value for first option that to be selected";
```

Here is a syntax to create a new `<option>`: `new Option(textInsideTheOption, optionValue, defaultSelected, selected)`

- `defaultSelected` – if `true`, then selected HTML-attribute is created,
- `selected` – if `true`, then the option is selected.

```js
const option1 = new Option("Text", "value");
const option2 = new Option("Text", "value", true, true);
```

<hr>

## submit a form to a server manually

To submit a form to the server manually, we can call `<form>.submit()`

<hr>
<hr>

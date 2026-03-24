# JSON

- [JSON](#json)
  - [`JSON.stringify()`](#jsonstringify)
  - [`JSON.parse()`](#jsonparse)

---

## `JSON.stringify()`

`JSON.stringify(value[, replacer, space])` method converts a JavaScript value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

```js
const obj = {
  name: "John",
  age: 30,
  isAdmin: false,
  courses: ["html", "css", "js"],
  spouse: null,
};

const json = JSON.stringify(obj);

console.log(json); // {"name":"John","age":30,"isAdmin":false,"courses":["html","css","js"],"spouse":null}
```

Using the replacer function in the `JSON.stringify(value[, replacer, space])`:

```js
const obj = {
  key1: "value1",
  key2: "value2",
  key3: 3,
  key4: "value 4",
  key5: 5,
};

function replacer(key, value) {
  // Filtering out strings
  if (typeof value === "string") {
    return;
  }
  return value;
}

const json = JSON.stringify(obj, replacer);
console.log(json); // {"key3":3,"key5":5
```

<hr>

Be careful with circular references. Use the replacer in `JSON.stringify()`:

```js
const room = {
  number: 23,
};

const meetup = {
  title: "Conference",
  participants: [{ name: "John" }, { name: "Alice" }],
  place: room, // meetup references room
};

// room references meetup
room.occupiedBy = meetup;

// stringifies only the properties in the array
const json = JSON.stringify(meetup, ["title", "participants", "name"]);

console.log(json); // {"title":"Conference","participants":[{"name":"John"},{"name":"Alice"}]}
```

Here is the above example with the replacer function instead of an array:

```js
const room = {
  number: 23,
};

const meetup = {
  title: "Conference",
  participants: [{ name: "John" }, { name: "Alice" }],
  place: room, // meetup references room
};

room.occupiedBy = meetup; // room references meetup

const json = JSON.stringify(meetup, function replacer(key, value) {
  return key == "occupiedBy" ? undefined : value;
});

console.log(json);
// {"title":"Conference","participants":[{"name":"John"},{"name":"Alice"}],"place":{"number":23}}
```

<hr>

## `JSON.parse()`

`JSON.parse()` parses a JSON string, constructing the JavaScript value or object described by the string. An optional reviver function can be provided to perform a transformation on the resulting object before it is returned.

```js
const jsonNumbers = "[0, 1, 2, 3]";

const arr = JSON.parse(jsonNumbers);

console.log(arr); // [0, 1, 2, 3]
```

```js
const json = '{"title":"Conference","date":"2017-11-30T12:00:00.000Z"}';

const obj = JSON.parse(json, function (key, value) {
  if (key == "date") return new Date(value);
  return value;
});

console.log(obj);
// {title: 'Conference', date: Thu Nov 30 2017 04:00:00 GMT-0800 (Pacific Standard Time)}
```

<hr>
<hr>

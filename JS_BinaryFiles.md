# Binary files

- [Binary files](#binary-files)
  - [`ArrayBuffer`](#arraybuffer)
    - [Typed Arrays](#typed-arrays)
    - [Typed Array Methods](#typed-array-methods)
    - [`DataView`](#dataview)
  - [`TextDecoder` and `TextEncoder`](#textdecoder-and-textencoder)
    - [`TextDecoder`](#textdecoder)
    - [`TextEncoder`](#textencoder)
  - [Blob](#blob)
    - [Downloading Blobs](#downloading-blobs)
  - [File and FileReader](#file-and-filereader)
    - [`File`](#file)
    - [`FileReader`](#filereader)
  - [Summary of Binary Files](#summary-of-binary-files)

---

---

## `ArrayBuffer`

`ArrayBuffer` is a JavaScript constructor that can be used to allocate a specific number of
bytes in memory. It is an array of bytes. `ArrayBuffer` is the chunk of memory that is set aside to hold typed arrays (`Int8Array`, `UInt8Array` etc). The syntax to create an `ArrayBuffer` is `new ArrayBuffer(<bytes>)`:

```js
const buffer = new ArrayBuffer(16); // create a buffer of length of 16 bytes
console.log(buffer.byteLength); // 16
```

This allocates a contiguous memory area of 16 bytes and pre-fills it with zeroes.

Let’s eliminate a possible source of confusion. `ArrayBuffer` is not `Array`:

- It has a fixed length, we can’t increase or decrease it.
- It takes exactly that much space in the memory.
- To access individual bytes, another “view” object is needed, not `<buffer>[<index>]`.

<hr>

### Typed Arrays

We cannot interact with the `ArrayBuffer` directly. To manipulate an `ArrayBuffer`, we need to use a view object. A view object does not store anything on its own. It’s the “eyeglasses” that give an interpretation of the bytes stored in the `ArrayBuffer`.

```js
const buffer = new ArrayBuffer(16); // create a buffer of length of 16 bytes, 8-bit (1 byte) * 16 bytes = 128 bits

const view = new Uint32Array(buffer); // view the buffer as a sequence of 32-bit integers

console.log(Uint32Array.BYTES_PER_ELEMENT); // 16 bytes / 32 bits = 128 bits / 32 bits = 4 bytes per integer

console.log(view.length); // 4, it stores that many integers
console.log(view.byteLength); // 16, the size in bytes

// let's write a value
view[0] = 123456;

// iterate over values
for (let num of view) {
  console.log(num); // 123456, then 0, 0, 0 (4 values total)
}

// use the spread operator with a typed array
console.log(...view); // 123456 0 0 0
```

The common term for all these views (`Uint8Array`, `Uint32Array`, etc) is **typed array**. Please note, there’s no constructor called TypedArray, it’s just a common “umbrella” term to represent one of views over `ArrayBuffer`: `Int8Array`, `Uint8Array` and so on. Typed arrays behave like regular arrays: have indexes and are iterable.

There are various typed arrays:

- `Int8Array` - is an array of 8-bit integers. These integers can be in the range of -128 to 127.
- `UInt8Array` (unsigned array) - is an array of 8-bit integers. These integers can be in the range of 0 to 255.
- `UInt8ClampedArray` (unsigned and clamped array) - is an array of 8-bit integers. These integers can be in the range of 0 to 255. Clamped means that if you try to put a number less than 0, it will be converted to 0. If you try to put a number greater than 255, it will be converted to 255.
- `Int16Array` - is an array of 16-bit integers. These integers can be in the range of -32768 to 32767.
- `UInt16Array` (unsigned array) - is an array of 16-bit integers. These integers can be in the range of 0 to 65535.
- `Int32Array` - is an array of 32-bit integers. These integers can be in the range of -2147483648 to 2147483647.
- `UInt32Array` (unsigned array) - is an array of 32-bit integers. These integers can be in the range of 0 to 4294967295.
- `Float32Array` - for signed floating-point numbers of 32. It treats every 4 bytes as a floating point number.
- `Float64Array` - for signed floating-point numbers of 64 bits. It treats every 8 bytes as a floating point number with possible values from 5.0x10^-324 to 1.8x10^308.

A typed array constructor (be it `Int8Array` or `Float64Array`, doesn’t matter) behaves differently depending on argument types. There are 5 variants of arguments:

```js
new <TypedArray>(<buffer>, [<byteOffset>, <length>]);
new <TypedArray>(<object>);
new <TypedArray>(<typedArray>);
new <TypedArray>(<length>);
new <TypedArray>();
```

- If an `<ArrayBuffer>` argument is supplied, the view is created over it.
  - Optionally, we can provide `<byteOffset>` to start from (0 by default) and the `<length>` (till the end of the buffer by default), then the view will cover only a part of the buffer.
- If an Array, or any array-like object is given, it creates a typed array of the same length and copies the content. We can use it to pre-fill the array with the data:

```js
const arr = new Uint8Array([0, 1, 2, 3]);
console.log(arr.length); // 4, created binary array of the same length
console.log(arr[1]); // 1, filled with 4 bytes (unsigned 8-bit integers) with given values
```

- If another typed array is supplied, it does the same: creates a typed array of the same length and copies values. Values are converted to the new type in the process, if needed.

```js
const arr16 = new Uint16Array([1, 1000]);
const arr8 = new Uint8Array(arr16);
console.log(arr8[0]); // 1
console.log(arr8[1]); // 232, tried to copy 1000, but can't fit 1000 into 8 bits
```

- For a numeric argument length – creates the typed array to contain that many elements. Its byte length will be length multiplied by the number of bytes in a single item `<TypedArray>.BYTES_PER_ELEMENT`:

```js
const arr = new Uint16Array(4); // create typed array for 4 integers, 4 * 16-bit = 64-bit
console.log(Uint16Array.BYTES_PER_ELEMENT); // 2 bytes per integer, 2 bytes = 16-bit = 1 integer
console.log(arr.byteLength); // 8 (size in bytes), 4 integers - 64-bit, 64 / 8-bit(1 byte) = 8 bytes
```

- Without arguments, creates a zero-length typed array.

We can create a typed array directly, without mentioning `ArrayBuffer`. But a view cannot exist without an underlying `ArrayBuffer`, so it gets created automatically in all these cases except the first one (when provided).

- To access the underlying `ArrayBuffer`, there are following properties in TypedArray:
  - `buffer` – references the `ArrayBuffer`.
  - `byteLength` – the length of the `ArrayBuffer`.

This lets us to move from one view to another easily:

```js
const arr8 = new Uint8Array([0, 1, 2, 3]);

// another view on the same data
const arr16 = new Uint16Array(arr8.buffer);
```

<hr>

### Typed Array Methods

Typed arrays have regular `Array` methods, with notable exceptions. We can iterate with `map`, `slice`, `find`, `reduce` etc.

There are few things we can’t do though:

- No `splice` – we can’t “delete” a value, because typed arrays are views on a buffer, and these are fixed, contiguous areas of memory. All we can do is to assign a zero.
- No `concat` method.

There are two additional methods that typed arrays have:

- `<typedArray>.set(<fromArr>, [<offset>])` copies all elements from `<fromArr>` to the `<typedArray>`, starting at position `<offset>` (0 by default).
- `<typedArray>.subarray([<begin>, <end>])` creates a new view of the same type from `<begin>` to `<end>` (exclusive). That’s similar to `slice` method, but doesn’t copy anything – just creates a new view, to operate on the given piece of data.

<hr>

### `DataView`

`DataView` is a special super-flexible “untyped” view over `ArrayBuffer`. It allows to access the data on any offset in any format. `DataView` is great when we store mixed-format data in the same buffer.

- For typed arrays, the constructor dictates what the format is. The whole array is supposed to be uniform. The i-th number is `<arr>[<i>]`.
- With `DataView` we access the data with methods like `.getUint8(<i>)` or `.getUint16(<i>)`. We choose the format at method call time instead of the construction time. We also set the data with methods like `setUint8()`, `setUint16()`, etc.

The syntax is `new DataView(<buffer>, [<byteOffset>], [<byteLength>])`.

- `<buffer>` – the underlying `ArrayBuffer`. Unlike typed arrays, `DataView` doesn’t create a buffer on its own. We need to have it ready.
- `<byteOffset>` – the starting byte position of the view (by default 0).
- `<byteLength>` – the byte length of the view (by default till the end of buffer).

```js
// binary array of 4 bytes, all have the maximal value 255
const buffer = new Uint8Array([255, 255, 255, 255]).buffer;

const dataView = new DataView(buffer);

// get 8-bit number at offset 0
console.log(dataView.getUint8(0)); // 255

// now get 16-bit number at offset 0, it consists of 2 bytes, together interpreted as 65535
console.log(dataView.getUint16(0)); // 65535 (biggest 16-bit unsigned int)

// get 32-bit number at offset 0
console.log(dataView.getUint32(0)); // 4294967295 (biggest 32-bit unsigned int)

dataView.setUint32(0, 0); // set 4-byte number to zero, thus setting all bytes to 0
```

<hr>

## `TextDecoder` and `TextEncoder`

### `TextDecoder`

What if the binary data is actually a string? The built-in `TextDecoder` object allows one to read the value into an actual JavaScript string, given the buffer and the encoding.

- We first need to create it with `new TextDecoder([<encoding>], [<options>])`
  - `<encoding>` – `utf-8` by default, but `big5`, `windows-1251` and others are also supported.
  - `<options>` – optional object:
    - `fatal` – boolean, if `true` then throw an exception for invalid (non-decodable) characters, otherwise (default) replace them with character \uFFFD.
    - `ignoreBOM` – boolean, if `true` then ignore BOM (an optional byte-order Unicode mark), rarely needed.

- After creating the `TextDecoder`, we can decode with `.decode([<input>], [<options>])`
  - `<input>` – BufferSource to decode.
  - `<options>` – optional object:
    - `stream` – true for decoding streams, when decoder is called repeatedly with incoming chunks of data. In that case a multi-byte character may occasionally split between chunks. This option tells `TextDecoder` to memorize “unfinished” characters and decode them when the next chunk comes.

```js
const uint8Array = new Uint8Array([72, 101, 108, 108, 111]);
console.log(new TextDecoder().decode(uint8Array)); // Hello
```

We can decode a part of the buffer by creating a subarray view for it:

```js
const uint8Array = new Uint8Array([0, 72, 101, 108, 108, 111, 0]);

// the string is in the middle
// create a new view over it, without copying anything
const binaryString = uint8Array.subarray(1, -1);

console.log(new TextDecoder().decode(binaryString)); // Hello
```

<hr>

### `TextEncoder`

`TextEncoder` does the reverse thing – converts a string into bytes. The syntax is `new TextEncoder()`. The only encoding it supports is “utf-8”. It has two methods:

- `encode(<str>)` – returns `Uint8Array` from a string.
- `encodeInto(<str>, <destination>)` – encodes `<str>` into `<destination>` that must be `Uint8Array`.

```js
const encoder = new TextEncoder();

const uint8Array = encoder.encode("Hello");
console.log(uint8Array); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]

console.log(new TextDecoder().decode(uint8Array)); // Hello
```

<hr>

## Blob

`ArrayBuffer` and views are parts of ECMA standard, parts of JavaScript. In the browser, there are additional higher-level objects, described in the File API, in particular `Blob`. Blob stands for Binary Large Object. It's basically any binary file.

The constructor syntax is `new Blob(<blobParts>, <options>);`

- `<blobParts>` is an array of Blob/BufferSource/String values. The first argument to `Blob` must be an array.
- `<options>` optional object:
  - `type` – Blob type, usually MIME-type, e.g. image/png, text/plain, etc.
  - `endings` – whether to transform end-of-line to make the Blob correspond to current OS newlines (\r\n or \n). By default `"transparent"` (do nothing), but also can be `"native"` (transform).

```js
// create Blob from a typed array and strings
const helloArr = new Uint8Array([72, 101, 108, 108, 111]); // "Hello" in binary form

const blob = new Blob([helloArr, " ", "world"], { type: "text/plain" });

console.log(helloArr); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]
console.log(blob); // Blob { size: 11, type: "text/plain"
```

We can’t change data directly in a Blob, but we can slice parts of a Blob, create new Blob objects from them, mix them into a new Blob and so on. This behavior is similar to JavaScript strings: we can’t change a character in a string, but we can make a new corrected string.

We can extract Blob slices with `<blob>.slice([<byteStart>], [<byteEnd>], [<contentType>]);`

- `<byteStart>` – the starting byte, by default 0.
- `<byteEnd>` – the last byte (exclusive, by default till the end).
- `<contentType>` – the type of the new blob, by default the same as the source.

The arguments are similar to `<array>.slice`, negative numbers are allowed too.

The `Blob` constructor allows to create a blob from almost anything, including any BufferSource. If we need to perform low-level processing, we can get the lowest-level `ArrayBuffer` from `<blob>.arrayBuffer()`.

### Downloading Blobs

We can download/upload Blob objects, and the `type` naturally becomes `Content-Type` in network requests. A Blob can also be easily used as a URL for `<a>`, `<img>` or other tags, to show its contents.

```html
<!-- download attribute forces the browser to download instead of navigating -->
<a download="hello.txt" href="#" id="link">Download and Clear the Link</a>

<script>
  const blob = new Blob(["Hello, world!"], { type: "text/plain" });

  // URL.createObjectURL takes a Blob and creates a unique URL for it, in the form blob:<origin>/<uuid>.
  link.href = URL.createObjectURL(blob);

  link.addEventListener("click", function () {
    URL.revokeObjectURL(link.href); // will download and then revoke the URL, won't be able to download in the next click
  });
</script>
```

An alternative to `URL.createObjectURL` is to convert a Blob into a base64-encoded string. That encoding represents binary data as a string of ultra-safe “readable” characters with ASCII-codes from 0 to 64. And what’s more important – we can use this encoding in “data-urls”. A data url has the form `data:[<mediatype>][;base64],<data>`. We can use such urls everywhere, on par with “regular” urls.

To transform a Blob into base64, we’ll use the built-in `FileReader` object. It can read data from Blobs in multiple formats.

```js
const link = document.createElement("a");
link.download = "hello.txt";

const blob = new Blob(["Hello, world!"], { type: "text/plain" });

const reader = new FileReader();
reader.readAsDataURL(blob); // converts the blob to base64 and calls onload

reader.onload = function () {
  link.href = reader.result; // data url
  link.click();
};
```

By using a Blob with the `URL.createObjectURL(<blob>)` option we need to revoke the blob to free up the memory. Using a Blob with this "Blob to data url" option, we might have performance and memory losses on big `Blob` objects for encoding.

<hr>

## File and FileReader

### `File`

A `File` object inherits from `Blob` and is extended with filesystem-related capabilities. As `File` inherits from `Blob`, `File` objects have the same properties, plus:

- `name` – the file name,
- `lastModified` – the timestamp of last modification.

There are two ways to obtain it.

- First, there’s a constructor, similar to `Blob`: `new File(<fileParts>, <fileName>, [<options>])`
  - `<fileParts>` – is an array of Blob/BufferSource/String values.
  - `<fileName>` – file name string.
  - `<options>` – optional object:
    - `lastModified` – if `true`, the timestamp (integer date) of last modification.
- Second, more often we get a file from `<input type="file">` or "drag and drop" or other browser interfaces. In that case, the file gets this information from OS.
  - The input may select multiple files. The `<input>.files` is an array-like object with them.

```js
<input type="file" onchange="showFile(this)">

<script>
function showFile(input) {
  const file = input.files[0];

  console.log(`File name: ${file.name}`);
  console.log(`Last modified: ${file.lastModified}`);
  console.log(input.files); // FileList [ File ]
}
</script>
```

<hr>

### `FileReader`

`FileReader` is an object with the sole purpose of reading data from a `Blob` (and hence `File` too). The syntax is

```js
const reader = new FileReader(); // no arguments
```

The main methods:

- `readAsArrayBuffer(<blob>)` – read the data in binary format `ArrayBuffer`.
  - This is for binary files, to do low-level binary operations.
- `readAsText(<blob>, [<encoding>])` – read the data as a text string with the given encoding (`utf-8` by default).
  - This is for text files, when we’d like to get a string.
- `readAsDataURL(<blob>)` – read the binary data and encode it as base64 data url.
  - This can be used when we’d like to use this data in `src` for `img` or another tag. We can also use `URL.createObjectURL()`.
- `abort()` – cancel the operation.

As the reading proceeds, there are events:

- `loadstart` – loading started.
- `progress` – occurs during reading.
- `load` – no errors, reading complete.
- `abort` – `abort()` called.
- `error` – error has occurred.
- `loadend` – reading finished with either success or failure.

When the reading is finished, we can access the result as:

- `reader.result` is the result (if successful)
- `reader.error` is the error (if failed).

Here is an example of reading a text file with `readAsText()` method:

```html
<input type="file" onchange="readFile(this)" />

<script>
  function readFile(input) {
    const file = input.files[0];

    const reader = new FileReader();

    reader.readAsText(file);

    reader.onload = function () {
      console.log(reader.result);
    };

    reader.onerror = function () {
      console.log(reader.error);
    };
  }
</script>
```

Here is an example of reading an image file with `readAsDataURL()` method, attaching it a page, and sending it to a server as a `Blob`:

```html
<input type="file" />
<div id="preview"></div>

<script>
  const fileInput = document.querySelector("input");
  const preview = document.getElementById("preview");

  fileInput.addEventListener("change", () => {
    const fileReader = new FileReader();

    fileReader.readAsDataURL(fileInput.files[0]);

    fileReader.addEventListener("load", () => {
      const url = fileReader.result;
      // console.log(url)

      const img = new Image();
      img.src = url;
      // preview.appendChild(img)

      img.onload = () => {
        const canvas = document.createElement("canvas");
        const ctx = canvas.getContext("2d");
        canvas.width = img.width;
        canvas.height = img.height;

        ctx.drawImage(img, 0, 0);
        preview.appendChild(canvas);

        canvas.toBlob((blob) => {
          const formData = new FormData();
          formData.append("img", blob, "img.png");

          fetch("https://httpbin.org/post", {
            method: "POST",
            body: formData,
          })
            .then((res) => res.json())
            .then((res) => console.log(res));
        });
      };
    });
  });
</script>
```

The `error` event fires if the file cannot be read for some reason. When the `error` event fires, the `error` property of the `FileReader` is filled in. This object has a single property, `code`, which can have an error code of

- 1 - file not found
- 2 - security error
- 3 - read was aborted
- 4 - file isn’t readable
- 5 - encoding error

<hr>

## Summary of Binary Files

Here is the brief summary of above concepts about binary files:

```js
// create an array buffer
const buffer = new ArrayBuffer(4); // create an array buffer - binary data - of 4 bytes

console.log(buffer); // 4
console.log(buffer.byteLength); // 4

// create an 8-bit view over the buffer
const view8 = new Int8Array(buffer);

// the view of the buffer when all the bytes are viewed as separate 8-bit entities
console.log(view8); // Int8Array(4) [ 0, 0, 0, 0 ]
console.log(view8.byteLength); // 4
console.log(view8.byteOffset); // 0
console.log(view8.BYTES_PER_ELEMENT); // 1
console.log(view8.length); // 4, byteLength / BYTES_PER_ELEMENT

// create an 8-bit view over the buffer by offsetting 1 byte
console.log(new Int8Array(buffer, 1)); // Int8Array(3) [ 0, 0, 0 ], byteOffset is 1
console.log(new Int8Array(buffer, 1).byteOffset); // byteOffset is 1, so the view of the buffer starts after offsetting 1 byte

// create an 8-bit view over the buffer by offsetting 2 bytes and having 2 byte-length
console.log(new Int8Array(buffer, 2, 2)); // Int8Array [ 0, 0 ], byteOffset is 2 and the length is 2
console.log(new Int8Array(buffer, 2, 2).byteLength); // 2
console.log(new Int8Array(buffer, 2, 2).byteOffset); // 2
console.log(new Int8Array(buffer, 2, 2).length); // 2

// create a 16-bit view over the buffer
const view16 = new Uint16Array(buffer);

console.log(view16); // Uint16Array [ 0, 0 ]
console.log(view16.byteLength); // 4
console.log(view16.BYTES_PER_ELEMENT); // 2
console.log(view16.length); // 2, byteLength / BYTES_PER_ELEMENT

// set the 0th position to 45
view16[0] = 45;
console.log(view16); // Uint16Array [ 45, 0 ]
console.log(view8); // Int8Array(4) [ 45, 0, 0, 0 ]
console.log(new Int8Array(buffer, 1)); // Int8Array(3) [ 0, 0, 0 ], byteOffset is 1, so 1 byte (which now holds the value of 45) is skipped

// iterate over the 8-bit view of the buffer
for (let num of view8) {
  console.log(num); // 45, 0, 0, 0
}

// create a 32-bit view over the buffer
const view32 = new Uint32Array(buffer);
console.log(view32); // Uint32Array [ 45 ]

// create a view and an array buffer at the same time
const view16_2 = new Uint16Array([1, 2, 3, 4]); // Array buffer created automatically
console.log(view16_2); // Uint16Array(4) [ 1, 2, 3, 4 ]

// create a view using another view
const view16_3 = new Uint16Array([1, 2, 3, 4]);
const view8_2 = new Uint8Array(view16_3);

// create a view using the buffer of another view
const view32_2 = new Uint32Array(view16_3.buffer);

console.log(view16_3); // Uint16Array(4) [ 1, 2, 3, 4 ]
console.log(view8_2); // Uint8Array(4) [ 1, 2, 3, 4 ]
console.log(view32_2); // Uint32Array [ 131073, 262147 ]

// create a view specifying only the length - the number of elements
console.log(new Uint8Array(2)); // Uint8Array [ 0, 0 ]

// create a view without specifying only the length - the number of elements
console.log(new Float32Array()); // Float32Array []

// set the existing view `Uint8Array(4) [ 1, 2, 3, 4 ]` to have elements 5, 6
view8_2.set([5, 6]);
console.log(view8_2); // Uint8Array(4) [ 5, 6, 3, 4 ]

// set the existing view to have elements 7, 8 starting from position 1
view8_2.set([7, 8], 1);
console.log(view8_2); // Uint8Array(4) [ 5, 7, 8, 4 ]

// create the copy of view8_2 from position 1 till 3 (exclusive)
const view8_3 = view8_2.subarray(1, 3);
console.log(view8_3); // Uint8Array [ 7, 8 ]

// Create a DataView over the buffer
const dataView = new DataView(buffer);

// log the items in the dataView in the positions 0, 1, 2
console.log(dataView.getUint8(0)); // 45
console.log(dataView.getUint8(1)); // 0
console.log(dataView.getUint8(2)); // 0

// Create a DataView over the buffer with offsetting 1 byte, and having length 2
const dataView2 = new DataView(buffer, 1, 2);

// log the items in the dataView in the positions 0, 1
console.log(dataView2.getUint8(0)); // 0
console.log(dataView2.getUint8(1)); // 0

// set the item in the dataView2, position 0 to 10
dataView2.setUint8(0, 10);
console.log(dataView2.getUint8(0)); // 0
console.log(dataView.getUint8(1)); // 0 the item in the dataView in the position 1 is the same as dataView2 position 0

// decode binary data into a string
const view8_4 = new Uint8Array([72, 101, 108, 108, 111]);
console.log(new TextDecoder().decode(view8_4)); // Hello
console.log(new TextDecoder("utf-8").decode(view8_4)); // Hello

// encode a string into binary data
console.log(new TextEncoder().encode("Hello")); // Uint8Array(5) [ 72, 101, 108, 108, 111 ]

// declare a typed array and encode a string into it
const encodedArr = new Uint8Array(6);
new TextEncoder().encodeInto("Hello", encodedArr);
console.log(encodedArr); // Uint8Array(6) [ 72, 101, 108, 108, 111, 0 ]

const blob = new Blob(["Hello"], { type: "text/plain" });
console.log(blob); // Blob { size: 5, type: "text/plain"

blob
  .arrayBuffer()
  .then((b) => {
    console.log(b); // ArrayBuffer { byteLength: 5 }
  })
  .catch((error) => console.error(error));

const blob_2 = new Blob([view8_4], { type: "text/plain" });
console.log(blob_2); // Blob { size: 5, type: "text/plain" }

const url = URL.createObjectURL(blob);
console.log(url); // blob:http...

URL.revokeObjectURL(blob);

const reader = new FileReader();
reader.readAsDataURL(blob_2);

reader.onload = () => {
  console.log(reader.result); // data:text/plain;base64,SGVsbG8=
};

const file = new File(["Hello"], "filename", { type: "text/plain" });
console.log(file); // File { name: "filename", lastModified: 1717209982047, webkitRelativePath: "", size: 5, type: "text/plain" }

// If uploaded from by user using the `input` tag, then can be accessed via <input>.files

const reader2 = new FileReader();

reader2.readAsArrayBuffer(file);
reader2.onload = () => {
  console.log(reader2.result); // ArrayBuffer { byteLength: 5 }
};

const reader3 = new FileReader();

reader3.readAsText(file);
reader3.onload = () => {
  console.log(reader3.result); // Hello
};

const reader4 = new FileReader();

reader4.readAsDataURL(file);
reader4.onload = () => {
  console.log(reader4.result); // data:text/plain;base64,SGVsbG8=
};

const reader5 = new FileReader();

reader5.readAsText(file);

reader5.onloadstart = () => {
  console.log("starting to read as text");
};

reader5.onprogress = () => {
  console.log("progressing to read as text");
};

reader5.onabort = () => {
  console.log("aborted to read as text"); // aborted to read as text
};

reader5.onerror = () => {
  console.log("error while reading as text");
  reader5.error;
};

reader5.onload = () => {
  console.log("loaded the text");
  console.log(reader5.result);
};

reader5.onloadend = () => {
  console.log("ended reading as text"); // ended reading as text
};

reader5.abort();
```

<hr>
<hr>

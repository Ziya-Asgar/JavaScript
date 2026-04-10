# Regular Expressions

- [Regular Expressions](#regular-expressions)
  - [Intro](#intro)
  - [Creating Regular Expressions](#creating-regular-expressions)
  - [Flags](#flags)
  - [Regular Expression methods](#regular-expression-methods)
    - [`.match()`](#match)
    - [`.replace()`](#replace)
    - [`.replaceAll()`](#replaceall)
    - [`<regexp>.test()`](#regexptest)
  - [Character classes](#character-classes)
    - [Inverse classes](#inverse-classes)
  - [Using dot `.`](#using-dot-)
  - [Unicode encoding and `u` flag](#unicode-encoding-and-u-flag)
  - [Anchors: string start `^` and end `$`](#anchors-string-start--and-end-)
    - [Multiline mode of anchors `^`, `$` and the flag `m`](#multiline-mode-of-anchors---and-the-flag-m)
  - [Word boundary: `\b`](#word-boundary-b)
  - [Escaping Special characters](#escaping-special-characters)
  - [Sets and ranges](#sets-and-ranges)
  - [Quantifiers `+`, `\*`, `?` and `{<number>}`](#quantifiers----and-number)
  - [Greedy and lazy quantifiers](#greedy-and-lazy-quantifiers)
  - [Capturing groups](#capturing-groups)
  - [Backreferences in pattern: `\N` and `\k<name>`](#backreferences-in-pattern-n-and-kname)
  - [Alternation (OR) `|`](#alternation-or-)
  - [Lookahead and lookbehind](#lookahead-and-lookbehind)
  - [Catastrophic backtracking](#catastrophic-backtracking)
  - [Sticky flag `y`, searching at position](#sticky-flag-y-searching-at-position)
  - [Methods of RegExp and String](#methods-of-regexp-and-string)
  - [Summary of Regular Expressions](#summary-of-regular-expressions)

---

---

## Intro

Regular expressions are patterns that provide a powerful way to search in and replace a text. In JavaScript, they are available via the `RegExp` object, as well as being integrated in string methods. A Regular Expression consists of a pattern and optional flags.

---

---

## Creating Regular Expressions

There are two syntaxes that can be used to create a regular expression object.

- The “long” syntax:

```js
const regexp = new RegExp("<pattern>" [, "<flags>"]);
```

- And the “short” one, using a regular expression literal. This one is done by using forward slashes `/<regexp>/`:

```js
const regexp = /pattern/; // no flags
```

```js
const regexp = /pattern/gim; // with flags g,m and i
```

You should use a regex literal when you know the regular expression pattern at the time of writing the code. On the other hand, use the `RegExp` constructor if the regex pattern is to be created dynamically. Also, the regex constructor lets you write a pattern using a template literal, but this is not possible with the regex literal syntax.

<hr>

## Flags

There are 6 flags in JavaScript's Regular Expressions:

- `i` - With this flag the search is case-insensitive: no difference between "A" and "a".
- `g` - With this flag the search looks for all matches, without it – only the first match is returned.
- `s` - Enables “dotall” mode, that allows a dot `.` to match newline character `\n`
- `u` - Enables full Unicode support. The flag enables correct processing of surrogate pairs.
- `m` - Multiline mode
- `y` - “Sticky” mode: searching at the exact position in the text

<hr>

## Regular Expression methods

### `.match()`

The method `<string>.match(<regexp>)` finds all matches of `<regexp>` in the string `<string>`.

Here is an example without any flags. Without the flag `g`, it returns only the first match in the form of an array, with the full match at index 0 and some additional details in properties.

```js
const str = "We will, we will rock you";

const result = str.match(/we/);

console.log(result[0]); // we (1st match)
console.log(result.index); // 9 (position of the match)

console.log(result.input); // We will, we will rock you (source string)
console.log(result.length); // 1
```

We add the `i` flag to make the search case-insensitive.

```js
const str = "We will, we will rock you";

const result = str.match(/we/i);

console.log(result[0]); // We (1st match)
console.log(result.index); // 0 (position of the match)

console.log(result.input); // We will, we will rock you (source string)
console.log(result.length); // 1
```

Then, we add the flag `g` which returns an array of all matches.

```js
const str = "We will, we will rock you";

const result = str.match(/we/gi);

console.log(result); // Array [ "We", "we" ]
```

If there are no matches, `null` is returned.

```js
const str = "Hello";

const result = str.match(/bye/i);

console.log(result); // null
```

### `.replace()`

The `<string>.replace(<string>, <replacement)` method could be used on strings to replace parts of the string.

```js
const str = "JavaScript";
const newStr = str.replace("ava", "").replace("cript", "");
console.log(newStr); // JS
```

The method could also be used with regular expressions. `<string>.replace(<regexp>, <replacement>)` replaces matches found using `<regexp>` in string `<string>` with `<replacement>` (all matches if there’s flag `g`, otherwise, only the first one).

```js
// no flag g
console.log("We will, we will".replace(/we/i, "I")); // I will, we will

// with flag g
console.log("We will, we will".replace(/we/gi, "I")); // I will, I will
```

There are symbols that we can use to control the replacement process.

| Symbols          | Actions                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------- |
| `$&`             | inserts the whole match                                                                      |
| `` $` ``         | inserts a string before the match                                                            |
| `$'`             | inserts a string after the match                                                             |
| `$$`             | inserts character `$`                                                                        |
| `$group_number`  | Works with capturing groups. Inserts the contents of a capturing group in the `group_number` |
| `$<group_name> ` | Works with capturing groups. Inserts the contents of the parentheses with the given `<name>` |

```js
console.log("I love HTML and CSS".replace(/HTML/, "$&, JavaScript")); // I love HTML, JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$`, JavaScript")); // I love I love , JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$', JavaScript")); // I love  and CSS, JavaScript and CSS
console.log("I love HTML and CSS".replace(/HTML/, "$$, JavaScript")); // I love $, JavaScript and CSS

console.log("Name Surname".replace(/(Name)\s(Surname)/, "$2, $1")); // Surname, Name

console.log(
  "Name Surname".replace(
    /(?<firstName>Name)\s(?<lastName>Surname)/,
    "$<lastName>, $<firstName>",
  ),
); // Surname, Name
```

The `<replacement>` could also be a function. The `replace()` method will invoke the **replacer** function after the match has been performed and use the result of this function as the replacement string. The **replacer** function has the following syntax:

```js
function replacer(match, p1, p2, ..., offset, string);
```

The following are the meanings of each parameter:

- **match** is the matched substring.
- **p1, p2, …pn** are the nth string found by a parenthesized capture group provided by the regular expression.
- **offset** is the offset of the matched substring within the whole string being searched.
- **string** is the whole string being examined.

```js
const str = "I love HTML and CSS";

const result = str.replace(/(HTML)/, (match, p1, offset, string) => {
  console.log(match);
  console.log(p1);
  console.log(offset);
  console.log(string);

  return `HTML, JavaScript`;
});

console.log(result); // I love HTML, JavaScript and CSS
```

### `.replaceAll()`

The main use case for `replaceAll` is replacing all occurrences of a string. This method is essentially the same as `<str>.replace()`, with two major differences:

- If the first argument is a string, it replaces all occurrences of the string, while `replace` replaces only the first occurrence.
- If the first argument is a regular expression, the `g` flag must be provided. Otherwise, there’ll be an error.

```js
const str = "I love HTML and CSS, HTML, HTML";

const result1 = str.replace(/(HTML)/g, (match, p1, offset, string) => {
  return match.toLowerCase();
});

const result2 = str.replaceAll(/(HTML)/g, (match, p1, offset, string) => {
  return match.toLowerCase();
});

console.log(result1); // I love html and CSS, html, html
console.log(result2); // I love html and CSS, html, html
```

### `<regexp>.test()`

The method `<regexp>.test(<str>)` looks for at least one match, if found, returns `true`, otherwise `false`.

```js
const regexp = /hello/i;

console.log(regexp.test("Hello there")); // true
console.log(regexp.test("Hi there")); // false
```

<hr>

## Character classes

A character class is a special notation that matches any symbol from a certain set.

The **digit** class is written as `\d` and corresponds to “any single digit”.

```js
const phoneNumber = "+1(234)-567-89-01";

console.log(phoneNumber.match(/\d/)); // 1
console.log(phoneNumber.match(/\d/g)); // Array of 1, 2, 3 ... 9, 0, 1

console.log(phoneNumber.match(/\d/g).join("")); // 12345678901
```

The **space** class is denoted as `\s` and includes spaces, tabs `\t`, newlines `\n` and few other rare characters, such as `\v`, `\f` and `\r`.

```js
const str = "A sentence with some spaces.";

console.log(str.match(/\s/g)); // Array(4) [ " ", " ", " ", " " ]
```

The **word** class is denoted as `\w` and it is either a letter of Latin alphabet or a digit or an underscore \_. Non-Latin letters do not belong to `\w`.

```js
const str = "A word";

console.log(str.match(/\w/g)); // Array(5) [ "A", "w", "o", "r", "d" ]
```

A regexp may contain both regular symbols and character classes.

```js
const cssString = "CSS3 is the current version of CSS";

console.log(cssString.match(/CSS\d/)); // Array [ "CSS3" ]
```

A regexp can also contain one character class after another one.

```js
const str = "1 a";
const str2 = `1
a`;
const str3 = " abcde 12 ";

console.log(str.match(/\d\s\w/)); // matches - returns [ "1 a" ]
console.log(str2.match(/\d\s\w/)); // matches - returns [ "1\na" ]
console.log(str3.match(/\d\s\w/)); // doesnt't match - returns null
```

### Inverse classes

For every character class there exists an “inverse class”, denoted with the same letter, but uppercased. The “inverse” means that it matches all other characters, for instance:

- `\D` means non-digit: any character except `\d`, for instance a letter.
- `\S` means non-space: any character except `\s`, for instance a letter.
- `\W` means non-wordly character: anything but `\w`, e.g a non-latin letter or a space.

In the below example, we find all the non-digits using `/\D/g`, and replace them.

```js
const phoneNumber = "+1(234)-567-89-01";

console.log(phoneNumber.replace(/\D/g, "")); // 12345678901
```

<hr>

## Using dot `.`

A dot `.` is a special character class that matches “any character except a newline”.

```js
console.log("ABcd".match(/./)); // Array [ "A" ]
console.log("ABcd".match(/./g)); // Array(4) [ "A", "B", "c", "d" ]

console.log("him".match(/hi./)); // Array [ "him" ]
console.log("his".match(/hi./)); // Array [ "his" ]
```

By default, a dot `.` doesn’t match the newline character `\n`.

```js
console.log("A-B".match(/A.B/)); // Array [ "A-B" ]
console.log("A B".match(/A.B/)); // Array [ "A B" ]
console.log("A\nB".match(/A.B/)); // null
```

If we want the dot `.` to include the newline character `\n` as well, then we can use the `s` flag.

```js
console.log("A\nB".match(/A.B/s)); // Array [ "A\nB" ]
```

<hr>

## Unicode encoding and `u` flag

JavaScript uses Unicode encoding for strings. Most characters are encoded with 2 bytes, but there are some that are 4 bytes. When JavaScript language was created, Unicode encoding was simpler: there were no 4-byte characters. So, some JavaScript features still handle 4-byte characters incorrectly. For instance, `length` treats 4 bytes as two 2-byte characters. Therefore, `length` thinks that there are two characters here:

```js
console.log("😄".length); // 2
console.log("𝒳".length); // 2
```

This might be problematic when we are working with regular expressions. To avoid the problem, we use the `u` flag. With the `u` flag, a regexp handles 4-byte characters correctly.

Every character in Unicode has a lot of properties. They describe what “category” the character belongs to and contain miscellaneous information about it. For instance, if a character has the `Letter` property, it means that the character belongs to an alphabet (of any language). A `Number` property means that it’s a digit: maybe Arabic or Chinese, and so on.

We can search for characters with a property, by writing `/\p{<unicode_property>}/u`. To use `\p{…}`, a regular expression must have the `u` flag. For instance, `\p{Letter}` denotes a letter in any language. We can also use `\p{L}`, as `L` is an alias of `Letter`.

```js
const str = "A ბ ㄱ";

console.log(str.match(/\p{L}/gu)); // Array(3) [ "A", "ბ", "ㄱ" ]
console.log(str.match(/\p{L}/g)); // null - `\p` doesn't work without the flag `u`
```

Here are the main character categories and their subcategories:

- Letter `L`:
  - lowercase `Ll`,
  - modifier `Lm`,
  - titlecase `Lt`,
  - uppercase `Lu`,
  - other `Lo`.
- Number `N`:
  - decimal digit `Nd`,
  - letter number `Nl`,
  - other `No`.
- Punctuation `P`:
  - connector `Pc`,
  - dash `Pd`,
  - initial quote `Pi`,
  - final quote `Pf`,
  - open `Ps`,
  - close `Pe`,
  - other `Po`.
- Mark `M` (accents etc):
  - spacing combining `Mc`,
  - enclosing `Me`,
  - non-spacing `Mn`.
- Symbol `S`:
  - currency `Sc`,
  - modifier `Sk`,
  - math `Sm`,
  - other `So`.
- Separator `Z`:
  - line `Zl`,
  - paragraph `Zp`,
  - space `Zs`.
- Other `C`:
  - control `Cc`,
  - format `Cf`,
  - not assigned `Cn`,
  - private use `Co`,
  - surrogate `Cs`.

Here are links to learn more about Unicode

- List all properties by a character: https://unicode.org/cldr/utility/character.jsp.
- List all characters by a property: https://unicode.org/cldr/utility/list-unicodeset.jsp.
- Short aliases for properties: https://www.unicode.org/Public/UCD/latest/ucd/PropertyValueAliases.txt.
- A full base of Unicode characters in text format, with all properties, is here: https://www.unicode.org/Public/UCD/latest/ucd/.

<hr>

## Anchors: string start `^` and end `$`

The caret `^` and dollar `$` characters have special meaning in a regexp. They are called **anchors**. The caret `^` matches at the beginning of the text, and the dollar `$` – at the end.

```js
const str = "Beginning is here. Here is the ending";

console.log(str.match(/^Beginning/)); // Array [ "Beginning" ]
console.log(str.match(/ending$/)); // Array [ "ending" ]
```

Both anchors together `^...$` are often used to test whether or not a string fully matches the pattern. For instance, to check if the user input is in the right format

```js
const goodInput = "12:34";
const badInput = "12:345";

const regexp = /^\d\d:\d\d$/;

console.log(regexp.test(goodInput)); // true
console.log(regexp.test(badInput)); // false
```

### Multiline mode of anchors `^`, `$` and the flag `m`

The multiline mode with the flag `m` only affects the behavior of `^` and `$`. In the multiline mode anchors match not only at the beginning and the end of the string, but also at start/end of a line.

In the below example, the pattern `/^\d/gm` takes a digit from the beginning of each line:

```js
const str = `1st place
2nd place
3rd place`;

console.log(str.match(/^\d/gm)); // Array(3) [ "1", "2", "3" ]

// Without the flag `m` only the first digit is matched
console.log(str.match(/^\d/g)); // Array [ "1" ]
```

In the below example, the pattern `/\d$/gm` takes a digit from the end of each line:

```js
const str = `Winnie: 1
Piglet: 2
Eeyore: 3`;

console.log(str.match(/\d$/gm)); // Array(3) [ "1", "2", "3" ]

// Without the flag `m` only the digit at the end of the whole text is matched
console.log(str.match(/\d$/g)); // Array [ "3" ]
```

<hr>

## Word boundary: `\b`

A word boundary `\b` is similar to `^` and `$`. It tests if there is a word boundary. There are three different positions that qualify as word boundaries:

- At string start, if the first string character is a word character `\w`.
- Between two characters in the string, where one is a word character `\w` and the other is not.
- At string end, if the last string character is a word character `\w`.

```js
console.log("Hello, JavaScript!".match(/\bHello\b/)); // Array [ "Hello" ]
console.log("Hello, JavaScript!".match(/\bJavaScript\b/)); // Array [ "JavaScript" ]
console.log("Hello, JavaScript!".match(/\bHell\b/)); // null (no match)
console.log("Hello, JavaScript!".match(/\bJava!\b/)); // null (no match)
```

We can use `\b` with digits as well. For example, the pattern `\b\d\d\b` looks for standalone 2-digit numbers. In other words, it looks for 2-digit numbers that are surrounded by characters different from `\w`, such as spaces or punctuation.

```js
console.log("1 23 456 78".match(/\b\d\d\b/g)); // Array [ "23", "78" ]
console.log("12,34,56".match(/\b\d\d\b/g)); // Array(3) [ "12", "34", "56" ]
```

The word boundary test `\b` checks that there should be `\w `on the one side from the position and "not `\w`" – on the other side. But `\w `means a latin letter a-z (or a digit or an underscore), so the test doesn’t work for other characters, e.g. cyrillic letters or hieroglyphs.

<hr>

## Escaping Special characters

There are special characters in a regexp, such as `[ ] { } ( ) \ ^ $ . | ? * +`.

So far, we have used a backslash `\` as a special character in regex. It is used to denote character classes like `\d` for digits, `\s` for spaces, etc. But it's also used for escaping. If there is a special character, let's say a dot `.`, and we don't want to use the dot as a special character, then we can use `\` to indicate that we are looking for a regular dot. This is called escaping a character. By using the `\` we are escaping the special use case of a character.

```js
console.log("Chapter 5.1".match(/\d\.\d/)); // 5.1 (match!)
console.log("Chapter 511".match(/\d\.\d/)); // null (looking for a real dot \.)

// we don't escape the dot in the below example
console.log("Chapter 511".match(/\d.\d/)); // Array [ "511" ]
```

Here is one more example. Parenteses are special characters, so we are escaping them in the below example:

```js
console.log("function g()".match(/g\(\)/)); // Array [ "g()" ]
```

A slash symbol '/' is not a special character, but in JavaScript it is used to open and close the regexp: `/...pattern.../`, so we should escape it too:

```js
console.log("path/to/folder".match(/\//)); // Array [ "/" ]
```

If we’re not using `/.../`, but create a regexp using `new RegExp`, then we don’t need to escape it:

```js
console.log("path/to/folder".match(new RegExp("/"))); // Array [ "/" ]
```

From the above example, it's visible that `new Regexp()` accepts a string as an argument to create a regular expression. That might cause a problem with using a backslash, because backslash has its own meaning while used as part of a string. For example:

- `\n` – becomes a newline character,
- `\u0024` – becomes the Unicode character with such code,
- …And when there’s no special meaning: like `\d` or `\z`, then the backslash is simply removed.

```js
console.log("d\nd"); // d [new line] d
console.log("\u0024 "); // $ - unicode character
console.log("d.d"); // d.d
```

So, if we need to use `new Regexp()`, and we want to use the backslash in it, the way backslash is used in `/.../` pattern, then we need to use double backslash `\\`.

```js
const regStr = "\\d\\.\\d";
console.log(regStr); // \d\.\d

const regexp = new RegExp(regStr);
console.log("Chapter 5.1".match(regexp)); // 5.1
```

<hr>

## Sets and ranges

Several characters or character classes inside square brackets `[…]` mean to “search for any character among given”. That’s called a **set** and they can be used in a regexp along with regular characters:

```js
// find "t" or "m", and then "op"
console.log("Mop top".match(/[tm]op/gi)); // Array [ "Mop", "top" ]
```

Note that although there are multiple characters in the set, they correspond to exactly one character in the match.

```js
// find "V", then "o" or "i", then "la"
console.log("Voila".match(/V[oi]la/)); // null, no matches

console.log("Vila".match(/V[oi]la/)); // Array [ "Vila" ]

console.log("Vola".match(/V[oi]la/)); // Array [ "Vola" ]
```

Square brackets may also contain character ranges:

- `[a-z]` is a character in range from a to z
- `[0-5]` is a digit range from 0 to 5

```js
console.log("Exception 0xAF".match(/[0-9]x[A-F][A-F]/g)); // Array [ "0xAF" ]

// We can have more than one range in the same [ ... ]
console.log("Exception 0xAF".match(/[0-9]x[0-9A-F][0-9A-F]/g)); // Array [ "0xAF" ]
console.log("Exception 0xA5".match(/[0-9]x[0-9A-F][0-9A-F]/g)); // Array [ "0xA5" ]
```

We can also use special characters in sets:

- `\d` – is the same as `[0-9]`,
- `\w` – is the same as `[a-zA-Z0-9_]`,
- `\s` – is the same as `[\t\n\v\f\r ]`, plus few other rare Unicode space characters.

Besides normal ranges, there are “excluding” ranges that look like `[^…]`. They are denoted by a caret character `^` at the start and match any character except the given ones.

The example below looks for any characters except letters, digits and spaces:

```js
console.log("test15@example.com".match(/[^\d\sA-Z]/gi)); // Array [ "@", "." ]
```

In square brackets, we can use the vast majority of special characters without escaping:

- Symbols `. + ( )` never need escaping.
- A hyphen `-` is not escaped in the beginning or the end (where it does not define a range).
- A caret `^` is only escaped in the beginning (where it means exclusion).
- The closing square bracket `]` is always escaped (if we need to look for that symbol).

But if you decide to escape them just in case, then it won't be a problem.

<hr>

## Quantifiers `+`, `\*`, `?` and `{<number>}`

A quantifier is appended to a character (or a character class, or a set etc) and specifies how many we need.

The simplest quantifier is a number in curly braces: `{<number>}`. For example, `\d{4}` is the same as `\d\d\d\d`.

```js
console.log("1 12 123 1234 12345".match(/\d{4}/)); //  Array [ "123" ]
```

The range: `{3,5}` means match 3 to 5 times.

```js
console.log("1 12 123 1234 12345".match(/\d{3,5}/)); //  Array [ "123" ]
console.log("1 12 123 1234 12345".match(/\d{3,5}/g)); //  Array(3) [ "123", "1234", "12345" ]
```

We can omit the upper limit and write `{3,}`.

```js
console.log("1 12 123 1234 12345".match(/\d{3,}/)); //  Array [ "123" ]
console.log("1 12 123 1234 12345".match(/\d{3,}/g)); //  Array(3) [ "123", "1234", "12345" ]
```

Instead of writing something as `{1,}`, we can use the shorthand `+`. `+` means match something one or more times:

```js
console.log("1 12 123 1234 12345".match(/\d{1,}/)); //  Array [ "1" ]
console.log("1 12 123 1234 12345".match(/\d{1,}/g)); //  Array(5) [ "1", "12", "123", "1234", "12345" ]

console.log("1 12 123 1234 12345".match(/\d+/)); //  Array [ "1" ]
console.log("1 12 123 1234 12345".match(/\d+/g)); //  Array(5) [ "1", "12", "123", "1234", "12345" ]
```

Instead of writing something as `{0,1}`, we can use the shorthand `?`. `?` means match something zero times or once:

```js
const str = "Should I write color or colour?";

console.log(str.match(/colou{0,1}r/g)); // Array [ "color", "colour" ]
console.log(str.match(/colou?r/g)); // Array [ "color", "colour" ]
```

Instead of writing something as `{0,}`, we can use the shorthand `*`. `*` means match something zero times or more:

```js
console.log("100 10 1".match(/\d0*/g)); // Array(3) [ "100", "10", "1" ]
```

<hr>

## Greedy and lazy quantifiers

There is something called greedy search in regular expressions. In the greedy mode (by default), a quantified character is repeated as many times as possible.

To understand let's see an example. Let's say, we want to retrieve all the words that are in quotes from a sentence. Let's try using `/".+"/g`:

```js
const regexp = /".+"/g;

const str = 'a "witch" and her "broom" is one';

console.log(str.match(regexp)); // Array [ '"witch" and her "broom"' ]
```

It doesn't work. Instead of finding two matches "witch" and "broom", it finds one: "witch" and her "broom".

- First, JavaScript tries to find the quote. JavaScript finds the quote at the 3rd position.
- Then it tries to see if the rest of the subject string conforms to `.+"`.
- It tries to match the dot. Dot means any character, except the newline. So, the next character matches the dot. But we have provided `+` and therefore JavaScript tries to check if more characters match the dot. All characters match the dot, so it only stops when it reaches the end of the string.
- Now the engine finished repeating `.+` and tries to find the next character of the pattern. It’s the quote `"`. But the string has finished. The regular expression engine understands that it took too many `.+` and starts to backtrack.
- Now it assumes that `.+` ends one character before the string end and tries to match the rest of the pattern from that position. It keeps backtracking until it finds the quote.
- Finally, the result ends up being `"witch" and her "broom"`.

The **lazy** mode of quantifiers is an opposite to the greedy mode. It means: “repeat minimal number of times”. We can enable it by putting a question mark `?` after the quantifier. Usually a question mark `?` is a quantifier by itself (zero or one), but if added after another quantifier (or even itself) it gets another meaning – it switches the matching mode from greedy to lazy. So,

- `*` becomes `*?`,
- `+` becomes `+?`,
- `?` becomes `??`.

The regexp `/".+?"/g` works as intended: it finds "witch" and "broom":

```js
const regexp = /".+?"/g;

const str = 'a "witch" and her "broom" is one';

console.log(str.match(regexp)); // Array [ '"witch"', '"broom"' ]
```

<hr>

## Capturing groups

A part of a pattern can be enclosed in parentheses `(...)`. This is called a “capturing group”. It has two effects:

- It allows to get the part of a match as a separate item in the result array.
- If we put a quantifier after the parentheses, it applies to the parentheses as a whole.

```js
console.log("Gogogo now!".match(/go+/gi)); // Array(3) [ "Go", "go", "go" ]

console.log("Gogogo now!".match(/(go)+/gi)); // Array [ "Gogogo" ]
```

Parentheses are numbered from left to right. The search engine memorizes the content matched by each of them and allows to get it in the result. The method `<str>.match(<regexp>)`, if regexp has no flag `g`, looks for the first match and returns it as an array:

- At index 0: the full match.
- At index 1: the contents of the first parentheses.
- At index 2: the contents of the second parentheses.
- …and so on…

```js
const str = "<h1>Hello, world!</h1>";

const tag = str.match(/<(.*?)>/);

console.log(tag[0]); // <h1>
console.log(tag[1]); // h1
```

Parentheses can be nested.

```js
const str = '<span class="my">';

const regexp = /<(([a-z]+)\s*([^>]*))>/;

const result = str.match(regexp);
console.log(result[0]); // <span class="my">
console.log(result[1]); // span class="my"
console.log(result[2]); // span
console.log(result[3]); // class="my"
```

When we search for all matches (flag `g`), the `match` method does not return contents for capturing groups. For example, let’s find all tags in a string:

```js
const str = "<h1> <h2>";

const tags = str.match(/<(.*?)>/g);

console.log(tags); // Array [ "<h1>", "<h2>" ]
```

To get `groups` in the result, we should search using the method `<str>.matchAll(<regexp>)`. Just like `match`, it looks for matches, but there are 3 differences:

- It returns not an array, but an iterable object.
- When the flag `g` is present, it returns every match as an array with groups.
- If there are no matches, it returns not `null`, but an empty iterable object.

```js
let results = "<h1> <h2>".matchAll(/<(.*?)>/gi);

// results - is not an array, but an iterable object
console.log(results); // RegExp String Iterator {  }

console.log(results[0]); // undefined (*)

results = Array.from(results); // let's turn it into array

console.log(results[0]); // Array [ "<h1>", "h1" ]
console.log(results[1]); // Array [ "<h2>", "h2" ]
```

Remembering groups by their numbers is hard. For simple patterns it’s doable, but for more complex ones counting parentheses is inconvenient. We can give a name to a capturing group. That’s done by putting `?<group_name>` **immediately after the opening parenthesis**.

```js
const str = "2019-04-30";

const dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/;

const groups = str.match(dateRegexp).groups;

console.log(groups); // Object { year: "2019", month: "04", day: "30" }
console.log(groups.year); // 2019
console.log(groups.month); // 04
console.log(groups.day); // 30
```

As you can see, the groups reside in the `.groups` property of the `match`. To look for all dates, we can add flag `g`. We’ll also need `matchAll` to obtain full matches, together with groups:

```js
const str = "2019-10-30 2020-01-01";

const dateRegexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;

const results = str.matchAll(dateRegexp);

for (let result of results) {
  const { year, month, day } = result.groups;

  console.log(`${day}.${month}.${year}`);
  // first log: 30.10.2019
  // second log: 01.01.2020
}
```

Method `<str>.replace(<regexp>, <replacemen>t)` that replaces all matches with regexp in `<str>` allows to use parentheses contents in the `<replacement>` string. That’s done using `$group_number` syntax.

```js
const str = "John Bull";
const regexp = /(\w+) (\w+)/;

console.log(str.replace(regexp, "$2, $1")); // Bull, John
```

For named parentheses, the reference will be `$<name>`.

```js
const regexp = /(?<year>[0-9]{4})-(?<month>[0-9]{2})-(?<day>[0-9]{2})/g;

const str = "2019-10-30, 2020-01-01";

console.log(str.replace(regexp, "$<day>.$<month>.$<year>"));
// 30.10.2019, 01.01.2020
```

Sometimes we need parentheses to correctly apply a quantifier, but we don’t want their contents in results. A group may be excluded by adding `?:` in the beginning:

```js
const str = "Gogogo John!";

// ?: excludes 'go' from capturing
const regexp = /(?:go)+ (\w+)/i;

const result = str.match(regexp);

console.log(result[0]); // Gogogo John (full match)
console.log(result[1]); // John
console.log(result.length); // 2 (no more items in the array)
```

<hr>

## Backreferences in pattern: `\N` and `\k<name>`

We can use the contents of capturing groups `(...)` not only in the result or in the replacement string, but also in the pattern itself. A group can be referenced in the pattern using `\N`, where `N` is the group number.

```js
const str = `He said: "She's the one!".`;

// `\1` means “find the same text as in the first group”
const regexp = /(['"])(.*?)\1/g;

console.log(str.match(regexp)); // Array [ `"She's the one!"` ]
```

If we use `?:` in the group, then we can’t reference it. Groups that are excluded from capturing `(?:...)` are not memorized by the engine.

To reference a named group, we can use `\k<name>`.

```js
const str = `He said: "She's the one!".`;

const regexp = /(?<quote>['"])(.*?)\k<quote>/g;

console.log(str.match(regexp)); // Array [ `"She's the one!"` ]
```

<hr>

## Alternation (OR) `|`

Alternation is the term in regular expression that is actually a simple “OR”. In a regular expression, it is denoted with a vertical line character `|`.

```js
const regexp = /html|php|css|java(script)?/gi;

const str = "First HTML appeared, then CSS, then JavaScript";

console.log(str.match(regexp)); // Array(3) [ "HTML", "CSS", "JavaScript" ]
```

To apply alternation to a chosen part of the pattern, we can enclose it in parentheses:

- I love `HTML|CSS` matches I love HTML or CSS.
- I love `(HTML|CSS)` matches I love HTML or I love CSS.

```js
const str = "I love HTML and CSS";
const str2 = "I love CSS";

// This tries to find either "I love HTML" or "CSS"
console.log(str.match(/I love HTML|CSS/g)); // Array [ "I love HTML", "CSS" ]
console.log(str2.match(/I love HTML|CSS/g)); // Array [ "CSS" ]

// This tries to find either "I love HTML" or "I love CSS"
console.log(str.match(/I love (HTML|CSS)/g)); // Array [ "I love HTML" ]
console.log(str2.match(/I love (HTML|CSS)/g)); // Array [ "I love CSS" ]
```

One more example:

```js
// better time regexp
const regexp = /([01]\d|2[0-3]):[0-5]\d/g;

console.log("00:00 10:10 23:59 25:99 1:2".match(regexp)); // Array(3) [ "00:00", "10:10", "23:59" ]
```

<hr>

## Lookahead and lookbehind

Sometimes we need to find only those matches for a pattern that are followed or preceded by another pattern. There’s a special syntax for that, called “lookahead” and “lookbehind”, together referred to as “lookaround”. The syntax is: `X(?=Y)`, it means "look for X, but match only if followed by Y". There may be any pattern instead of X and Y. Please note: the lookahead is merely a test, the contents of the parentheses `(?=...)` is not included in the result.

```js
const str = "1 turkey costs 30€";

console.log(str.match(/\d+(?=€)/)); // Array [ "30" ], the number 1 is ignored, as it's not followed by €
```

More complex tests are possible, e.g. `X(?=Y)(?=Z)` means:

- Find X.
- Check if Y is immediately after X (skip if isn’t).
- Check if Z is also immediately after X (skip if isn’t).
- If both tests passed, then the X is a match, otherwise continue searching.

```js
const str = "1 turkey costs 30€";

// looks for \d+ that is followed by a space (?=\s), and there’s 30 somewhere after it (?=.*30)
console.log(str.match(/\d+(?=\s)(?=.*30)/)); // Array [ "1" ]
```

There is also a negative lookahead. The syntax is: `X(?!Y)`, it means "search X, but only if not followed by Y".

```js
const str = "2 turkeys cost 60€";

console.log(str.match(/\d+\b(?!€)/g)); // Array [ "2" ] (the price is not matched)
```

Lookahead allows to add a condition for “what follows”. Lookbehind is similar, but it looks behind. The syntax is:

- Positive lookbehind: `(?<=Y)X`, matches X, but only if there’s Y before it.
- Negative lookbehind: `(?<!Y)X`, matches X, but only if there’s no Y before it.

Please Note: Lookbehind is not supported in non-V8 browsers, such as Safari, Internet Explorer.

```js
const str = "1 turkey costs $30";

// the dollar sign is escaped \$
// Positive lookbehind
console.log(str.match(/(?<=\$)\d+/)); // Array [ "30" ] (skipped the sole number)

// Negative lookbehind
console.log(str.match(/(?<!\$)\b\d+/g)); // Array [ "1" ] (the price is not matched)
```

Generally, the contents inside lookaround parentheses does not become the part of a result. E.g. in the pattern `\d+(?=€)`, the € sign doesn’t get captured as a part of the match. That’s natural: we look for a number `\d+`, while `(?=€)` is just a test that it should be followed by €. But in some situations we might want to capture the lookaround expression as well, or a part of it. If we want that, just wrap that part into additional parentheses.

```js
const str = "1 turkey costs 30€";
const regexp1 = /\d+(?=€)/;
const regexp2 = /\d+(?=(€))/; // extra parentheses around €

console.log(str.match(regexp1)); // Array [ "30" ]
console.log(str.match(regexp2)); // Array [ "30", "€" ]
```

And here’s the same for lookbehind:

```js
const str = "1 turkey costs $30";
const regexp1 = /(?<=\$|£)\d+/;
const regexp2 = /(?<=(\$|£))\d+/;

console.log(str.match(regexp1)); // Array [ "30" ]
console.log(str.match(regexp2)); // Array [ "30", "$" ]
```

<hr>

## Catastrophic backtracking

We mentioned that to turn from the greedy search mode to the lazy mode, we need to `?` after a quantifier. But in some situations, we might want to keep the greedy search mode, but get rid of the backtracking. To stop the backtracking, we add `+` after a quantifier. That is, we use `\d++` instead of `\d+` to stop `+` from backtracking. With one more `+`, the quantifier, in this example `\d++`, becomes a **possessive quantifier**. Possessive quantifiers are in fact simpler than “regular” ones. They just match as many as they can, without any backtracking. The search process without backtracking is simpler.

<hr>

## Sticky flag `y`, searching at position

The flag `y` allows to perform the search at the given position in the source string. We can use this flag with `<regexp>.exec(<str>)` method. For a regexp without flags `g` and `y`, this method looks only for the first match, it works exactly like `<str>.match(<regexp>)`. But if there’s flag `g`, then it performs the search in `<str>`, starting from the position stored in the `<regexp>.lastIndex` property. And, if it finds a match, then sets `<regexp>.lastIndex` to the index immediately after the match. If we can `exec` again, the next `exec` will run starting from the `<regexp>.lastIndex`.

```js
const str = "let varName"; // Let's find all words in this string
const regexp = /\w+/g;

console.log(regexp.lastIndex); // 0 (initially lastIndex=0)

const word1 = regexp.exec(str);
console.log(word1[0]); // let (1st word)
console.log(regexp.lastIndex); // 3 (position after the match)

const word2 = regexp.exec(str);
console.log(word2[0]); // varName (2nd word)
console.log(regexp.lastIndex); // 11 (position after the match)

const word3 = regexp.exec(str);
console.log(word3); // null (no more matches)
console.log(regexp.lastIndex); // 0 (resets at search end)
```

Here is the implementation with the `for` loop:

```js
const str = "let varName";
const regexp = /\w+/g;

let result;

while ((result = regexp.exec(str))) {
  console.log(`Found ${result[0]} at position ${result.index}`);
  // Found let at position 0, then
  // Found varName at position 4
}
```

If we want the `exec` to start searching from a specific position in a string, we can manually set `lastIndex` to a number.

```js
const str = 'let varName = "value"';

const regexp = /\w+/g; // without flag "g", property lastIndex is ignored

regexp.lastIndex = 4;

const word = regexp.exec(str);
console.log(word); // Array [ "varName" ]
```

The `regexp.exec` call starts searching at position `lastIndex` and then goes further. If there’s no word at position `lastIndex`, but it’s somewhere after it, then it will be found. If we need to find a match exactly at the given position at the text, not somewhere after it, we can use flag `y`. The flag `y` makes `<regexp>.exec` to search exactly at the position `lastIndex`, not “starting from” it.

```js
const str = 'let varName = "value"';

const regexp = /\w+/y;

regexp.lastIndex = 3;
console.log(regexp.exec(str)); // null (there's a space at position 3, not a word)

regexp.lastIndex = 4;
console.log(regexp.exec(str)); // Array [ "varName" ] (word at position 4)
```

<hr>

## Methods of RegExp and String

The `.split(<delimiter>)` could be used on a string without regular expressions. It splits a string by a provided delimiter. However, we can also use it with a regular expression.

```js
console.log("12, 34, 56".split(/,\s*/)); // Array(3) [ "12", "34", "56" ]
```

The method `<str>.search(<regexp>)` returns the position of the first match or `-1` if none found. `search` only finds the first match:

```js
const str = "A drop of ink may make a million think";

console.log(str.search(/ink/i)); // 10 (first match position
```

<hr>

## Summary of Regular Expressions

Here is a brief summary of some concepts in the regular expressions:

```js
const shortStr = "This is a short text.";
const longStr = `Here is a long text.
This is a multiline one.
It has numbers "like" 123 or 45678, also numbers with "symbols" +1-234-4567-89-01.
It has a lot more "symbols such as" [ ] ( ) * & $ ! @.`;

// Simple match with all the details that could be access through the result
console.log(longStr.match(/is/)); // Array [ "is" ]

console.log(Array.isArray(longStr.match(/is/))); // true, the result of `match` comes as an array, if there's a match
console.log(longStr.match(/no match/)); // returns null, if there's no match

console.log(longStr.match(/is/)[0]); // is
console.log(longStr.match(/is/).length); // 1, the number of matches
console.log(longStr.match(/is/).index); // 5, the position of the matched string in the source string
console.log(longStr.match(/is/).input); // the source string, where the search happens

console.log(longStr.match(/is/g)); // Array(3) [ "is", "is", "is" ], flag `g` returns all matches
console.log(longStr.match(/is/g).length); // 3
console.log(longStr.match(/is/g).index); // undefined, with the `g` flag, `match` doesn't return additional details about the match
console.log(longStr.match(/is/g).input); // undefined, with the `g` flag, `match` doesn't return additional details about the match

console.log(longStr.matchAll(/is/g)); // `matchAll` mustbe called with the flag `g`
const matchAllArr = Array.from(longStr.matchAll(/is/g)); // `matchAll` returns an iterable object, we can convert it to an array, if we are going to iterate through it more than once
console.log(matchAllArr); // Array(3) [ (1) […], (1) […], (1) […] ]
console.log(matchAllArr.length); // 3

// `matchAll` has access to additional details for all the matches
console.log(matchAllArr[0].length); // 1, the number of matches in the array for the first match, same as `longStr.match(/is/).length`
console.log(matchAllArr[0].index); // 5, the position of the first matched string in the source string, same as `longStr.match(/is/).index`
console.log(matchAllArr[0].input); // the source string, where the search happens, same as `longStr.match(/is/).input`

console.log(longStr.matchAll(/no match/g)); // returns an empty iterable object, if there's no match

console.log(longStr.match(/it/g)); // Array [ "it" ], the "it" is from "...with..." in the source
console.log(longStr.match(/it/gi)); // Array(3) [ "It", "it", "It" ], flag `i` makes the search case-insensitive

console.log(/it/i.test(longStr)); // true, returns true on the first match
console.log(/no match/i.test(longStr)); // false, returns false if no match

console.log(/it/gi.test(longStr)); // true, flag `g` doesn't matter with `test`, as it returns true on the first match

console.log(shortStr.replace("short", "very short")); // This is a very short text. `replace` could be used with a simple string
console.log(shortStr.replace(/short/, "very short")); // This is a very short text. `replace` could be used with regexp

console.log(shortStr.replace(/short/, "very $&")); // This is a very short text. `$&` is the matched string
console.log(shortStr.replace(/short/, "...hapchi... I said, $`short")); // This is a ...hapchi... I said, This is a short text. `$`` is the string before the matched string.
console.log(shortStr.replace(/short/, "$'")); // This is a  text. text. `$'` is the string after the matched string.
console.log(shortStr.replace(/short/, "$$")); // This is a $ text. `$$` is $.

console.log(shortStr.replace(/(This) (is)/, "$2 $1")); // is This a short text. `$1` is (This) and `$2` is (is).
console.log(
  shortStr.replace(
    /(?<firstWord>This) (?<secondWord>is)/,
    "$<secondWord> $<firstWord>",
  ),
); // is This a short text. `$<firstWord>` is (This) and `$<secondWord>` is (is).

// `replace` accepts a function whose return value will be used as a replacement
console.log(
  "A\nB\nC".replace(/A/, function (match, offset, string) {
    return `Return from func: match: ${match}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A, offset: 0, input string: A
B
C. The End.
B
C */

// matching string, capturing groups, the offset of the position of the match from the beginning of the source string, and the source string itself could be accessed
console.log(
  "A\nB\nC".replace(/(A)/, function (match, p1, offset, string) {
    return `Return from func: match: ${match}, capturing group: ${p1}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A, capturing group: A, offset: 0, input string: A
B
C. The End.
B
C */

// the more capturing groups are accessed between match and offset parameters
console.log(
  "A\nB\nC".replace(/(A)\n(B)/, function (match, p1, p2, offset, string) {
    return `Return from func: match: ${match}, capturing group 1: ${p1}, capturing group 2: ${p2}, offset: ${offset}, input string: ${string}. The End.`;
  }),
);
/* Return from func: match: A
B, capturing group 1: A, capturing group 2: B, offset: 0, input string: A
B
C. The End.
C */

console.log(shortStr.replaceAll(/is/g, "IS")); // ThIS IS a short text. `replaceAll` must be used with the flag `g`
console.log(shortStr.replace(/is/g, "IS")); // ThIS IS a short text, `replace` with the flag `g` is the same as `replaceAll`

console.log(longStr.match(/\d/)); // Array [ "1" ], `\d` returns digits
console.log(longStr.match(/\D/)); // Array [ "H" ], `\d` returns non-digits

console.log(longStr.match(/\s/)); // Array [ " " ], `\d` returns spaces
console.log(longStr.match(/\S/)); // Array [ "H" ], `\d` returns non-spaces

console.log(longStr.match(/\w/)); // Array [ "H" ], `\d` returns wordly characters
console.log(longStr.match(/\W/)); // Array [ " " ], `\d` returns non-wordly characters

console.log(longStr.match(/./g)); // matches any character except the newline
console.log(longStr.match(/./gs)); // with flag `s`, `.` matches the newline character as well

console.log(longStr.match(/^Here/gi)); // Array [ "Here" ], `^` anchor searches the beginning of a string
console.log(longStr.match(/\.$/gi)); // Array [ "." ], `$` anchor searches the end of a string

console.log(longStr.match(/^It/gim)); // Array [ "It", "It" ], `^` with the flag `m` searches the beggining of every line
console.log(longStr.match(/\.$/gim)); // Array(4) [ ".", ".", ".", "." ], `$` with the flag `m` searches the end of every line

console.log(longStr.match(/it/gi)); // Array(3) [ "It", "it", "It" ], the second "it" is from "...with..." in the source
console.log(longStr.match(/\bit\b/gi)); // Array [ "It", "It" ], `\b` means a word boundary, a non-`\w` character

console.log(longStr.match(/\b[Ii]t\b/g)); // Array [ "It", "It" ], `[Ii ]` means one of I or i
console.log(longStr.match(/\bit\b/g)); // null

console.log(longStr.match(/\b[^Ii]t\b/g)); // null, `[^Ii ]` means any character other than I or i

console.log(longStr.match(/\d{3}/g)); // Array(3) [ "123", "234", "456" ], `\d{3}` is the same as \d\d\d
console.log(longStr.match(/\d{3,}/g)); // Array(3) [ "123", "234", "4567" ], `\d{3,}` means 3 or more digits
console.log(longStr.match(/\d{4,5}/g)); // Array [ "45678", "4567" ], `\d{4,5}` means 4 or 5 digits

console.log(longStr.match(/\d+/g)); // Array(7) [ "123", "45678", "1", "234", "4567", "89", "01" ], `+` means {1,}
console.log(longStr.match(/4\d?/g)); // Array(3) [ "45", "4", "45" ], `?` means {0,1}
console.log(longStr.match(/4\d*/g)); // Array(3) [ "45678", "4", "4567" ], `*` means {0,}

console.log(longStr.match(/".+?"/gi)); // Array(3) [ '"like"', '"symbols"', '"symbols such as"' ], +? turns on the lazy mode for +
console.log(longStr.match(/".??"/gi)); // null, ?? turns on the lazy mode for ?
console.log(longStr.match(/".*?"/gi)); // Array(3) [ '"like"', '"symbols"', '"symbols such as"' ], +? turns on the lazy mode for *

// match
// matchAll
// test
// replace
// replaceAll

// g
// i
// s
// u
// m
// y

// $&
// $`
// $'
// $$
// $group_number
// $<group_name>

// \d
// \s
// \w

// \D
// \S
// \W

// .

// ^
// $
// \b

// [ ]
// [^ ]

// {<number>}
// {<number>,}
// {<lower_limit_number>,<upper_limit_number>}
// + same as {1,}
// ? same as {0,1}
// * same as {0,}

// +?
// *?
// ??

// ( )
// ( ( ) ( ) )
// (?: )

// (?<group_name>)
// (\group_number)
// (\k<group_name)

// |
// ( | )

// (?=)
// (?!)
// (?<=)
// (?<!)

// (?=( ))

// \d++
// \w++

// exec with lastIndex and flag y
```

<hr>
<hr>

# Date Object

- [Date Object](#date-object)
  - [create a new `Date()`](#create-a-new-date)
  - [`Date.now()`](#datenow)
  - [`.getTime()`](#gettime)
  - [Setting a date using the `Date` object](#setting-a-date-using-the-date-object)
  - [Retrieve different parts of a date](#retrieve-different-parts-of-a-date)
  - [`.getTimezoneOffset()`](#gettimezoneoffset)
  - [Setting different parts of a date](#setting-different-parts-of-a-date)
  - [`Date.parse()`](#dateparse)

---

## create a new `Date()`

We can create a new `Date()` variable using the `new` keyword:

```js
// new Date(year, month[, date, hours, minutes, seconds, ms)]
const date = new Date();
console.log(date); // For example, Fri Oct 06 2023 20:40:15 GMT-0700 (Pacific Daylight Time)

// year and month specified (months start from 0)
const date2 = new Date(1991, 2);
console.log(date2); // Mon Mar 25 1991 00:00:00
```

<hr>

## `Date.now()`

The `Date.now()` static method returns the number of milliseconds elapsed since the epoch, which is defined as the midnight at the beginning of January 1, 1970, UTC. If we provide these milliseconds to the `new Date()` syntax, we will get current date and time:

```js
const nowInMS = Date.now();

console.log(nowInMS); // For example, 1519211809934
console.log(new Date(nowInMS)); // logs current date and time
```

## `.getTime()`

`.getTime()` method returns the same as above:

```js
const nowInMS = new Date().getTime();

console.log(nowInMS);
```

<hr>

## Setting a date using the `Date` object

There are different ways of setting a date using the `Date` object. The exact time might vary depending on your time zone:

- Providing `0` to the `Date()` as an argument, will give the date of January 1, 1970, UTC (this might vary depending on the time zone).

  ```js
  const jan_01_1970 = new Date(0);
  ```

- We can provide a date with milliseconds from January 1, 1970, UTC. Below code multiplies number of seconds in an hour with 1000 to get the number of milliseconds in an hour. Then multiplies it with negative 24 hours, to go one day back from January 1, 1970, UTC.

  ```js
  const dec_31_1969 = new Date(-24 * 3600 * 1000);

  console.log(dec_31_1969);
  ```

- We can set a date as a string:

  ```js
  const date2017 = new Date("2017-01-26");
  ```

- A month in the `Date` object starts from `0` (January is `0`). If we provide number of days in a month more than the month can have, the `Date` object automatically calculates a proper date. Below code, for example, returns February 1st, not January 32nd.

  ```js
  // new Date(year, month[, date, hours, minutes, seconds, ms)]
  const date2013 = new Date(2013, 0, 32);

  console.log(date2013); // Fri Feb 01 2013 00:00:00 GMT-0800 (Pacific Standard Time)
  ```

- Here is another example of setting a date with the `Date` object. This time even the optional values are set:

  ```js
  // new Date(year, month[, date, hours, minutes, seconds, ms)]
  new Date(2011, 0, 1, 0, 0, 0, 0); // 1 Jan 2011, 00:00:00
  ```

- The below code returns the same as above. Hours, minutes, seconds, and milliseconds are `0` by default:

  ```js
  // new Date(year, month[, date, hours, minutes, seconds, ms)]
  new Date(2011, 0, 1);
  ```

<hr>

## Retrieve different parts of a date

After creating a date, we can use various methods of the `Date` object to retrieve different parts of a date:

```js
const now = new Date();

now.getFullYear();
now.getMonth(); // number of a month, starting from 0
now.getDate(); // day of a month
now.getDay(); // day of a week
now.getHours();
now.getMinutes();
now.getSeconds();
now.getMilliseconds();
```

The above methods return different values depending on your time zone. There is UTC version of these methods. UTC stands for Coordinated Universal Time. Greenwich Mean Time and UTC display the same time:

```js
const nowUTC = new Date();

nowUTC.getUTCFullYear();
nowUTC.getUTCMonth();
nowUTC.getUTCDate();
nowUTC.getUTCDay();
nowUTC.getUTCHours();
nowUTC.getUTCMinutes();
nowUTC.getUTCSeconds();
nowUTC.getUTCMilliseconds();
```

<hr>

## `.getTimezoneOffset()`

The `.getTimezoneOffset()` method of `Date` instances returns the difference, in minutes, between this date as evaluated in the UTC time zone, and the same date as evaluated in the local time zone:

```js
new Date().getTimezoneOffset();
```

<hr>

## Setting different parts of a date

Here are various ways of setting different parts of a date:

```js
const now = new Date();

now.setFullYear(2011, 1, 1); // setFullYear(year, [month], [date])

now.setMonth(1, 1); // setMonth(month, [date])

now.setDate(1);

now.setHours(1, 0, 0, 0); // setHours(hour, [min], [sec], [ms])

now.setMinutes(20, 0, 0); // setMinutes(min, [sec], [ms])

now.setSeconds(20, 0); // setSeconds(sec, [ms])

now.setMilliseconds(100); // setMilliseconds(ms)
```

<hr>

## `Date.parse()`

`Date.parse(<str>)` can read a date from a string. The JavaScript specification only specifies one format to be universally supported: `YYYY-MM-DDTHH:mm:ss.sssZ`

Various components can be omitted, so the following are all valid:

- Date-only form: YYYY, YYYY-MM, YYYY-MM-DD
- Date-time form: one of the above date-only forms, followed by T, followed by HH:mm, HH:mm:ss, or HH:mm:ss.sss. Each combination can be followed by a time zone offset.

For example, "2011-10-10" (date-only form), "2011-10-10T14:48:00" (date-time form), or "2011-10-10T14:48:00.000+09:00" (date-time form with milliseconds and time zone) are all valid date time strings.

```js
// parses the date into milliseconds
Date.parse("2012-01-26T13:51:50.417-07:00"); // 1327611110417
```

<hr>
<hr>

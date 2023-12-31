# Left substring generator

Generates all left substrings of a given string.

* Use `String.prototype.length` to terminate early if the string is empty.
* Use a `for...in` loop and `String.prototype.slice()` to `yield` each substring of the given string, starting at the beginning.

```js
const leftSubstrGenerator = function* (str) {
  if (!str.length) return;
  for (let i in str) yield str.slice(0, i + 1);
};
```

```js
[...leftSubstrGenerator('hello')];
// [ 'h', 'he', 'hel', 'hell', 'hello' ]
```

# Sort characters in string

Alphabetically sorts the characters in a string.

* Use the spread operator (`...`), `Array.prototype.sort()` and `String.prototype.localeCompare()` to sort the characters in `str`.
* Recombine using `Array.prototype.join()`.

```js
const sortCharactersInString = str =>
  [...str].sort((a, b) => a.localeCompare(b)).join('');
```

```js
sortCharactersInString('cabbage'); // 'aabbceg'
```

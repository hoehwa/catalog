# Last n elements

Gets the last `n` elements of an array.

* Use `Array.prototype.slice()` with a start value of `-n` to get the last `n` elements of `arr`.

```js
const lastN = (arr, n) => arr.slice(-n);
```

```js
lastN(['a', 'b', 'c', 'd'], 2); // ['c', 'd']
```

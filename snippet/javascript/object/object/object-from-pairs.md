# Object from pairs

Creates an object from the given key-value pairs.

* Use `Array.prototype.reduce()` to create and combine key-value pairs.
* [`Object.fromEntries()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Object/fromEntries) provides similar functionality.

```js
const objectFromPairs = arr =>
  arr.reduce((a, [key, val]) => ((a[key] = val), a), {});
```

```js
objectFromPairs([['a', 1], ['b', 2]]); // {a: 1, b: 2}
```

# Ungroup array elements based on function

Creates an array of elements, ungrouping the elements in an array produced by [zip](https://github.com/mindulle/Documents/blob/main/js/s/zip/README.md) and applying the provided function.

* Use `Math.max()` and the spread operator (`...`) to get the longest subarray in the array, `Array.prototype.map()` to make each element an array.
* Use `Array.prototype.reduce()` and `Array.prototype.forEach()` to map grouped values to individual arrays.
* Use `Array.prototype.map()` and the spread operator (`...`) to apply `fn` to each individual group of elements.

```js
const unzipWith = (arr, fn) =>
  arr
    .reduce(
      (acc, val) => (val.forEach((v, i) => acc[i].push(v)), acc),
      Array.from({
        length: Math.max(...arr.map(x => x.length))
      }).map(x => [])
    )
    .map(val => fn(...val));
```

```js
unzipWith(
  [
    [1, 10, 100],
    [2, 20, 200],
  ],
  (...args) => args.reduce((acc, v) => acc + v, 0)
);
// [3, 30, 300]
```

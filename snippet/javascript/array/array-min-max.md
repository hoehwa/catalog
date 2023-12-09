# Tip: Min and max value in a JavaScript array

When working with numeric arrays in JavaScript, you might find yourself in need of finding the minimum or maximum value. Luckily, JavaScript's `Math` built-in object has got you covered. You can simply use `Math.min()` or `Math.max()` combined with the spread operator (`...`), as both functions accept any number of arguments.

```js
const nums = [2, 4, 6, 8, 1, 3, 5, 7];

Math.max(...nums); // 8
Math.min(...nums); // 1
```

For more complex cases, such as finding the min/max value in an array of objects, you might have to resort to `Array.prototype.map()` or `Array.prototype.reduce()`. On the other hand, our [minBy](https://github.com/mindulle/Documents/blob/main/js/s/min-by/README.md) or [maxBy](https://github.com/mindulle/Documents/blob/main/js/s/max-by/README.md) snippets might be all you need.

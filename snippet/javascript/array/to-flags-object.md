# Array to flags object

Converts an array of strings into an object mapping to true.

* Use `Array.prototype.reduce()` to convert the array into an object, where each array value is used as a key whose value is set to `true`.

```js
const flags = arr => arr.reduce((acc, str) => ({...acc, [str]: true }), {});
```

```js
flags(['red', 'green']); // { red: true, green: true }
```

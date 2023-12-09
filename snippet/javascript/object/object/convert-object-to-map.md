# Convert object to Map

Converts an object to a `Map`.

* Use `Object.entries()` to convert the object to an array of key-value pairs.
* Use the `Map` constructor to convert the array to a `Map`.

```js
const objectToMap = obj => new Map(Object.entries(obj));
```

```js
objectToMap({a: 1, b: 2}); // Map {'a' => 1, 'b' => 2}
```

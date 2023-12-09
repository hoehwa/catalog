# How do I convert an iterable to an array in JavaScript?

JavaScript ES6 introduced, among many other things, the [spread operator (`...`)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread\_syntax), which allows an iterable to be expanded in places where zero or more arguments or elements are expected.

We can use the spread operator to convert iterables or, as they are sometimes referred to, array-likes. Let's take a look at some examples:

#### String

When the spread operator is applied to a string, the result is an array of strings each one representing a character of the original string:

```js
const name = 'Zelda';
const letters = [...name]; // 'Z', 'e', 'l', 'd', 'a'
```

#### Set

A [`Set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/Set) is a collection of unique values. When the spread operator is applied to it, the result is an array of the stored values:

```js
const data = [1, 2, 3, 1, 2, 4]
const values = new Set(data);
const uniqueValues = [...values]; // [1, 2, 3, 4]
```

Note that the above example is the basis for the [uniqueElements snippet](https://github.com/mindulle/Documents/blob/main/js/s/unique-elements/README.md).

#### NodeList

A [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) is a collection of nodes, returned by methods such as `Document.childNodes()` or `Document.querySelectorAll()`. While it implements some methods that help manipulate it as an array (e.g. `NodeList.prototype.forEach()`), it's oftentimes desirable to convert it to an array. When the spread operator is applied to it, the result is an array of the contained nodes:

```js
const nodes = document.childNodes;
const nodeArray = [...nodes]; // [ <!DOCTYPE html>, html ]
```

Note that the above example is the basis for the [nodeListToArray snippet](https://github.com/mindulle/Documents/blob/main/js/s/node-list-to-array/README.md).

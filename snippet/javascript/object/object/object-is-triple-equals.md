# What's the difference between Object.is() and the triple equals operator in JavaScript?

If you want to check equality in JavaScript, there are two comparison operators, which are explained in depth in a previous [article](https://github.com/mindulle/Documents/blob/main/blog/s/javascript-equality/README.md).

Very briefly, the double equals operator (`==`) only compares value whereas the triple equals operator (`===`) compares both value and type. But there is also a third option, `Object.is()`, which behaves the same as the triple equals operator with the exception of `NaN` and `+0` and `-0`.

Here are some examples for additional clarity:

```js
{} === {}; // false
Object.is({}, {}); // false

1 === 1; // true
Object.is(1, 1); // true

+0 === -0; // true
Object.is(+0, -0); // false

NaN === NaN; // false
Object.is(NaN, NaN); // true
```

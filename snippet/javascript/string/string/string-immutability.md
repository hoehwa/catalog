# Are JavaScript strings immutable?

String specifications among programming languages vary, however most languages treat them as reference types. But strings in JavaScript are different. They are **immutable primitives**. This means that the characters within them may not be changed and that any operations on strings actually create new strings.

```js
const x = 'type';
x[1] = 'a';       // Nothing happens, doesn't throw an error
console.log(x);   // LOGS: 'type'
```

It helps to think of strings in the way that we think of numbers, if we are to better understand how they work. Numeric values are also immutable primitives. If, for example, you could mutate numbers, you could change the meaning of the value `42` to be another number, say `13`. In the same sense, you cannot mutate a string with a value of `gem` to make it `gym`.

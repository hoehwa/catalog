# Luhn check

Implements the [Luhn Algorithm](https://en.wikipedia.org/wiki/Luhn\_algorithm) used to validate a variety of identification numbers, such as credit card numbers, IMEI numbers, National Provider Identifier numbers etc.

* Use `String.prototype.split()`, `Array.prototype.reverse()` and `Array.prototype.map()` in combination with `parseInt()` to obtain an array of digits.
* Use `Array.prototype.shift()` to obtain the last digit.
* Use `Array.prototype.reduce()` to implement the Luhn Algorithm.
* Return `true` if `sum` is divisible by `10`, `false` otherwise.

```js
const luhnCheck = num => {
  const arr = (num + '')
    .split('')
    .reverse()
    .map(x => parseInt(x));
  const lastDigit = arr.shift();
  let sum = arr.reduce(
    (acc, val, i) => (i % 2 !== 0 ? acc + val : acc + ((val *= 2) > 9 ? val - 9 : val)),
    0
  );
  sum += lastDigit;
  return sum % 10 === 0;
};
```

```js
luhnCheck('4485275742308327'); // true
luhnCheck(6011329933655299); //  true
luhnCheck(123456789); // false
```

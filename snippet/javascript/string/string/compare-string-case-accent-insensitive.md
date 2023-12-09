# Tip: Compare strings regardless of case and accent

Comparing and sorting JavaScript strings is rather common. Usually, the use of `String.prototype.localeCompare()` is sufficient for sorting arrays of strings in most scenarios. Dealing with accents and cases can get tricky, however, and lead to unexpected results. This is where `Intl.Collator` comes into play, an object used for language-sensitive string comparison. Using `Intl.Collator.prototype.compare()`, you can sort strings regardless of their case or accent and it can even accept a locale argument.

```js
const arr = ['ä', 'a', 'b', 'A', 'B', 'Å'];

const localeCompare = (a, b) => a.localeCompare(b);
const collator = new Intl.Collator();
const deCollator = new Intl.Collator('de');
const svCollator = new Intl.Collator('sv');

arr.sort(localeCompare);      // ['a', 'A', 'Å', 'ä', 'b', 'B']
arr.sort(collator.compare);   // ['a', 'A', 'Å', 'ä', 'b', 'B']
arr.sort(deCollator.compare); // ['a', 'A', 'Å', 'ä', 'b', 'B']
arr.sort(svCollator.compare); // ['a', 'A', 'b', 'B', 'Å', 'ä']
```

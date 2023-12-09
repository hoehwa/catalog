# Device supports touch events

Checks if touch events are supported.

* Check if `'ontouchstart'` exists in the `Window`.

```js
const supportsTouchEvents = () =>
  window && 'ontouchstart' in window;
```

```js
supportsTouchEvents(); // true
```

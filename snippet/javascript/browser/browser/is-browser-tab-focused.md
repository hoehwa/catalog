# Check if browser tab is focused

Checks if the browser tab of the page is focused.

* Use the `Document.hidden` property, introduced by the [Page Visibility API](https://developer.mozilla.org/en-US/docs/Web/API/Page\_Visibility\_API) to check if the browser tab of the page is visible or hidden.

```js
const isBrowserTabFocused = () => !document.hidden;
```

```js
isBrowserTabFocused(); // true
```

# Tip: Style links without a class

When styling injected or generated HTML content, you might not have access to the classes or IDs of the elements you want to style. This can become especially annoying when dealing with link elements. Luckily, you can use the `:not()` selector with an appropriate attribute selector to check for the absence of a class and style links accordingly.

```css
a[href]:not([class]) {
  color: #0077ff;
  text-decoration: underline;
}
```

As a bonus tip, you can use [the previous tip about selecting any link](https://github.com/mindulle/Documents/blob/main/css/s/select-any-link/README.md) to further enhance this solution.

# 4 ways to center content with CSS

#### Flexbox

Using flexbox to vertically and horizontally center content is usually the **preferred method**. All it takes is three lines of code in the container element to set `display: flex` and then center the child element vertically and horizontally using `align-items: center` and `justify-content: center` respectively. You can view the [Flexbox centering snippet](https://github.com/mindulle/Documents/blob/main/css/s/flexbox-centering/README.md) for the code and examples.

#### Grid

Using the grid module is very similar to flexbox and also a common technique, especially if you are **already using grid in your layout**. The only difference from the previous technique is the `display` which is set to `grid` instead. You can view the [Grid centering snippet](https://github.com/mindulle/Documents/blob/main/css/s/grid-centering/README.md) for the code and examples.

#### Transform

Transform centering uses, as the name implies, CSS transforms to center an element. It depends on the container element having a `position: relative`, allowing the child element to utilize `position: absolute` to position itself. Then `left: 50%` and `top: 50%` are used to offset the child element and `transform: translate(-50%, -50%)` to negate its position. You can view the [Transform centering snippet](https://github.com/mindulle/Documents/blob/main/css/s/transform-centering/README.md) for the code and examples.

#### Table

Last but not least, table centering is an older technique which you might favor when working with **older browsers**. It depends on the use of `display: table` in the container element. This allows the child element to use `display: table-cell` in combination with `text-align: center` and `vertical-align: middle` to center itself horizontally and vertically. You can view the [Display table centering snippet](https://github.com/mindulle/Documents/blob/main/css/s/display-table-centering/README.md) for the code and examples.

# List includes all values

Checks if all the elements in `values` are included in `lst`.

* Check if every value in `values` is contained in `lst` using a `for` loop.
* Return `False` if any one value is not found, `True` otherwise.

```py
def includes_all(lst, values):
  for v in values:
    if v not in lst:
      return False
  return True
```

```py
includes_all([1, 2, 3, 4], [1, 4]) # True
includes_all([1, 2, 3, 4], [1, 5]) # False
```

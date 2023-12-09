# How do I trim whitespace from a string in Python?

When working with Python strings, a pretty common question is how to trim whitespace from a string. Whitespace characters are the space ( ), tab (), newline (), and carriage return characters (). Here are 3 different methods to trim whitespace from a string in Python.

#### Remove leading and trailing whitespace characters

Use the `str.strip()` method to remove whitespace characters from both the beginning and end of a string.

```py
'  Hello  '.strip()    # 'Hello'
```

#### Remove leading whitespace characters

Leading whitespace characters are the whitespace characters at the start of a string. To remove them, use the `str.lstrip()` method.

```py
'  Hello  '.lstrip()   # 'Hello  '
```

#### Remove trailing whitespace characters

Trailing whitespace characters are the whitespace characters at the end of a string. To remove them, use the `str.rstrip()` method.

```py
'  Hello  '.rstrip()   # '  Hello'
```

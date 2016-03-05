# `trim`
The `trim` filter is used to trim whitespace off the beginning and end of a string.
```
{{ "    This text has too much whitespace.    " | trim }}
```
The above example will output the following:
```
This text has too much whitespace.
```
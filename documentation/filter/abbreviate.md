# `abbreviate`
The `abbrevate` filter will abbreviate a string using an ellipsis. It takes one argument which is the max
width of the desired output including the length of the ellipsis.
```
{{ "this is a long sentence." | abbreviate(7) }}
```
The above example will output the following:
```
this...
```

## Arguments
- length
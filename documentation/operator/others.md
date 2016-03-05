# Other Operators
The `|` operator is used to apply a filter to a variable.
```
{{ user.name | capitalize }}
```
Pebble supports the use of the conditional operator (often named the ternary operator).
```
{{ foo == null ? bar : baz }}
```
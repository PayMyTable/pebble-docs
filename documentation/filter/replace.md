# `replace`
The 'replace' filter formats a given string by replacing the placeholders (placeholders are free-form):
```
{{ "I like %this% and %that%." | replace({'%this%': foo, '%that%': "bar"}) }}
```

## Arguments
- placeholders to replace
# `urlencode`

The `urlencod` translates a string into `application/x-www-form-urlencoded` format using the "UTF-8" encoding scheme.

```
{{ "The string ü@foo-bar" | urlencode }}
```

The above example will output the following:
```
The+string+%C3%BC%40foo-bar
```
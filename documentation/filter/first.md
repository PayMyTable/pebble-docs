# `first`
The `first` filter will return the first item of a collection, or the first letter of a string.
```
{{ users | first }}
{# will output the first item in the collection named 'user' #}

{{ 'Mitch' | first }}
{# will output 'M' #}
```
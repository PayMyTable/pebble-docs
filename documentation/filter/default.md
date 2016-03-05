## `default`
The `default` filter will render a default value if and only if the object being filtered is empty.
A variable is empty if it is null, an empty string, an empty collection, or an empty map.
```
{{ user.phoneNumber | default("No phone number") }}
```
If the `strictVariables` setting of the `PebbleEngine` is set to false (which is the default), then
attribute expressions are null safe. In the following example, if `foo`, `bar`, or `baz` are null the output
will become an empty string which is a perfect use case for the default filter:
```
{{ foo.bar.baz | default("No baz") }}
```
If `strictVariables` is set to `true`, the above example will throw a null pointer exception if either
`foo` or `bar` are null.

## Arguments
- default
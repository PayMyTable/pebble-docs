# `escape`
The `escape` filter will turn special characters into safe character references in order to avoid XSS
vulnerabilities. This filter will typically only need to be used if you've turned off autoescaping.
```
{{ "<div>" | escape }}
{# output: &lt;div&gt; #}
```
Please read the [escaping guide](../guide/escaping) for more information about escaping.

## Arguments
- strategy
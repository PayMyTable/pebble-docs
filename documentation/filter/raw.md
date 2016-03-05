# `raw`
The `raw` filter prevents the output of an expression from being escaped by the autoescaper.
The `raw` filter must be the very last operation performed within the expression otherwise the
autoescaper will deem the expression as potentially unsafe and escape it regardless.

```
{% set danger = "<div>" %}
{{ danger | upper | raw }}
{# ouptut: <DIV> #}
```

If the `raw` filter is not the last operation performed then the expression will be escaped:
```
{% set danger = "<div>" %}
{{ danger | raw | upper }}
{# output: &lt;DIV&gt; #}
```
See the [escaping guide](../guide/escaping) for more details on how escaping works.
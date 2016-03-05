# Autoescape

The `autoescape` tag can be used to temporarily disable/re-enable the autoescaper as well as change the
escaping strategy for a portion of the template.
```
{{ danger }} {# will be escaped by default #}
{% autoescape false %}
	{{ danger }} {# will not be escaped #}
{% endautoescape %}
```
```
{{ danger }} {# will use the "html" escaping strategy #}
{% autoescape "js" %}
	{{ danger }} {# will use the "js" escaping strategy #}
{% endautoescape %}
```
See the [escaping](../guide/escaping) guide for more details on how escaping works.
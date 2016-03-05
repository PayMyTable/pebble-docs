# `filter`

The `filter` tag allows you to apply a filter to a large chunk of template.
```
{% filter upper %}
	hello
{% endfilter %}}

{# output: 'HELLO' #}
```
Multiple filters can be chained together.
```
{% filter upper | escape %}
	hello<br>
{% endfilter %}}

{# output: 'HELLO&lt;br&gt;' #}
```
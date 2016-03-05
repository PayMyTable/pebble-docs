# `rsort`
The `rsort` filter will sort a list in reversed order. The items of the list must implement `Comparable`.
```
{% for user in users | sort %}
	{{ user.name }}
{% endfor %}
```
# `sort`
The `sort`` filter will sort a list. The items of the list must implement `Comparable`.
```
{% for user in users | sort %}
	{{ user.name }}
{% endfor %}
```
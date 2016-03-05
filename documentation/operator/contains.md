# `contains`
The `contains` operator can be used to determine if a collection, map, or array contains a particular item.
```
{% if ["apple", "pear", "banana"] contains "apple" %}
	...
{% endif %}
```
When using maps, the contains operator checks for an existing key.
```
{% if {"apple":"red", "banana":"yellow"} contains "banana" %}
	...
{% endif %}
```
The operator can be used to look for multiple items at once:
```
{% if ["apple", "pear", "banana", "peach"] contains ["apple", "peach"] %}
	...
{% endif %}
```
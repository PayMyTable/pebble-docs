# `macro`
The `macro` tag allows you to create a chunk of reusable and dynamic content. The macro can be called
multiple times in the current template or even from another template with the help of the [import](import) tag.

It doesn't matter where in the current template you define a macro, i.e. whether it's before or after you call it.
Here is an example of how to define a macro:
```
{% macro input(type="text", name, value) %}
	<input type="{{ type }}" name="{{ name }}" value="{{ value }}" />
{% endmacro %}
```
And now the macro can be called numerous times throughout the template, like so:
```
{{ input(name="country") }}
{# will output: <input type="text" name="country" value="" /> #}
```
If the macro resides in another template, use the [import](import) tag first.
```
{% import "form_util" %}
{{ input("text", "country", "Canada") }}
```
A macro does not have access to the same variables that the rest of the template has access to.
A macro can only work with the variables provided as arguments.
# What is it?
Pebble is a full featured template engine for Java; it separates itself from other Java
template engines with it's inheritance feature and it's easy-to-read syntax.it ships with built-in autoescaping for
security, and it includes integrated support for internationalization.
```twig
{% block content %}
	<ul>
	{% for user in users %}
		<li>{{ user.name }}</li>
	{% endfor %}
	</ul>
{% endblock %}
```

# About
Pebble is a java template template engine inspired by [Twig](http://twig.sensiolabs.org/).
It separates itself from the crowd
with it's inheritance feature and it's easy-to-read syntax. It ships with built-in autoescaping for
security, and it includes integrated support for internationalization.

## Basic Usage
For more information on installation and configuration, see [the installation guide](documentation/guide/installation).
For more information on basic usage, see [the basic usage guide](documentation/guide/basic-usage).

First, add the following dependency to your pom.xml:
```
<dependency>
	<groupId>com.mitchellbosecke</groupId>
	<artifactId>pebble</artifactId>
	<version>2.3.0</version>
</dependency>
```

Then create a template in your WEB-INF folder. Let's start with a base template that all
other templates will inherit from, name it "base.html":
```
<html>
<head>
	<title>{% block title %}My Website{% endblock %}</title>
</head>
<body>
	<div id="content">
		{% block content %}{% endblock %}
	</div>
	<div id="footer">
		{% block footer %}
			Copyright 2014
		{% endblock %}
	</div>
</body>
</html>
```
Then create a template that extends base.html, call it "home.html":
```
{% extends "base.html" %}

{% block title %} Home {% endblock %}

{% block content %}
	<h1> Home </h1>
	<p> Welcome to my home page. My name is {{ name }}.</p>
{% endblock %}
```
Now we want to compile the template, and render it:
```
PebbleEngine engine = new PebbleEngine.Builder().build();
PebbleTemplate compiledTemplate = engine.getTemplate("home.html");

Map<String, Object> context = new HashMap<>();
context.put("name", "Mitchell");

Writer writer = new StringWriter();
compiledTemplate.evaluate(writer, context);

String output = writer.toString();
```
The output should result in the following:
```
<html>
<head>
	<title> Home </title>
</head>
<body>
	<div id="content">
		<h1> Home </h1>
	    <p> Welcome to my home page. My name is Mitchell.</p>
	</div>
	<div id="footer">
		Copyright 2014
	</div>
</body>
</html>
```

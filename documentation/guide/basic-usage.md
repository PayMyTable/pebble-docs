# Basic Usage

## Introduction
Pebble templates can be used to generate any sort of textual output. It is typically used to generate HTML but it can
also be used to create CSS, XML, JS, etc. A template itself will contain whatever language you are attempting to output
alongside Pebble-specific features and syntax. Here is a simple example that will generate a trivial HTML page:

```
<html>
	<head>
		<title>{{ websiteTitle }}</title>
	</head>
	<body>
		{{ content }}
	</body>
</html>
```
When you evaluate the template you will provide it with a "context" which is just a map of variables.
This context should include the two variables above, `websiteTitle` and `content`.

## Set Up
You will want to begin by creating a PebbleEngine object which is responsible for compiling your templates:
```
PebbleEngine engine = new PebbleEngine.Builder().build();
```
And now, with your new PebbleEngine instance you can start compiling templates:
```
PebbleTemplate compiledTemplate = engine.getTemplate("templates/home.html");
```
Finally, simply provide your compiled template with a java.io.Writer object and a Map of variables (the context)
to get your output!
```
Writer writer = new StringWriter();

Map<String, Object> context = new HashMap<>();
context.put("websiteTitle", "My First Website");
context.put("content", "My Interesting Content");

compiledTemplate.evaluate(writer, context);

String output = writer.toString();
```

## Syntax Reference
There are two primary delimiters used within a Pebble template: `{{ ... }}` and `{% ... %}`. The first set of delimiters
will output the result of an expression. Expressions can be very simple (ex. a variable name) or much more complex.
The second set of delimiters is used to change the control flow of the template; it can contain an if-statement,
define a parent template, define a new block, etc.

## Variables
You can print variables directly to the output; for example, if the context contains a variable called `foo` which is a
String with the value "bar" you can do the following which will output "bar".
```
{{ foo }}
```
You can use the dot (.) notation to access attributes of variables. If the attribute contains any atypical
characters, you can use the subscript notation ([]) instead.
```
{{ foo.bar }}
{{ foo["bar"] }}
```
Behind the scenes `foo.bar` will attempt the following techniques to to access the `bar` attribute of the `foo`
variable:
- If `foo` is a map, `foo.get("bar")`
- `foo.getBar()`
- `foo.isBar()`
- `foo.hasBar()`
- `foo.bar()`
- `foo.bar`

If the value of variable (or attribute) is null it will output an empty string.

## Type Safety
Pebble templates are dynamically typed and any possible type safety issues won't occur until the actual runtime
evaluation of your templates. Pebble does however allow you to choose how to handle type safety issues with the use
of it's `strictVariables` setting. By default, `strictVariables` is set to `false` which means that the following:
```
{{ foo.bar }}
```
will print an empty string even if the object `foo` does not actually have an attribute called `bar`.
If `strictVariables` is set to true, the above expression would throw an exception.

When `strictVariables` is set to false your expressions are also null safe. The following expression will print an
empty string even if foo and/or bar are null:
```
{{ foo.bar.baz }}
```
The default [filter](../filter/default) might come in handy for the above situations.

## Filters

Output can be further modified with the use of filters. Filters are separated from the variable using a
pipe symbol (`|`) and may have optional arguments in parentheses. Multiple filters can be chained and the output
of one filter is applied to the next.
```
{{ "If life gives you lemons, eat lemons." | upper | abbreviate(13) }}
```
The above example will output the following:
```
IF LIFE GI...
```

## Functions
Whereas filters are intended to modify existing content/variables, functions are intended to generate new content.
Similar to other programming languages, functions are invoked via their name followed by parentheses (`()`).
```
{{ max(user.score, highscore) }}
```

## Control Structure
Pebble provides several tags to control the flow of your template, two of the main ones being the [for](../tag/for) loop,
and [if](../tag/if) statements.
```
{% for article in articles %}
    <h3>{{ article.title }}</h3>
    <p>{{ article.content }}</p>
{% else %}
    <p> There are no articles. </p>
{% endfor %}
```
```
{% if category == "news" %}
    {{ news }}
{% elseif category == "sports" %}
    {{ sports }}
{% else %}
    <p>Please select a category</p>
{% endif %}
```

## Including other Templates
The [include](../tag/include) tag is used to include the rendered output of one template into another.
```
<div class="sidebar">
	{% include "advertisement.html" %}
</div>
```

## Template Inheritance
Template inheritance is the most powerful feature of Pebble. It allows templates to override sections of their parent
template. In your parent template you define "blocks" which are the sections that are allowed to be overriden.

First let us look at an example of a parent template:
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
			Copyright 2013
		{% endblock %}
	</div>
</body>
</html>
```
In the above example, we have used the [block](../tag/block) tag to define several sections that child templates are
allowed to override.

A child template might look like this:

```
{% extends "parent.html" %}

{% block title %} Home {% endblock %}

{% block content %}
	<h1> Home </h1>
	<p> Welcome to my home page.</p>
{% endblock %}
```

The first line uses the [extends](../tag/extends) tag to declare the parent template. The extends tag should be the
first tag in the template and there can only be one.

Evaluating the child template will produce the following output:

```
<html>
<head>
	<title>Home</title>
</head>
<body>
	<div id="content">
		<h1> Home </h1>
		<p> Welcome to my home page.</p>
	</div>
	<div id="footer">
		Copyright 2013
	</div>
</body>
</html>
```

You may have noticed that in the above example, because the child template doesn't override the `footer` block,
the value from the parent is used instead.

Dynamic inheritance is possible by using an expression with the `extends` tag:
```
{% extends ajax ? 'ajax.html' : 'base.html' %}
```

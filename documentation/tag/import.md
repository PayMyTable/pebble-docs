# `import`
The `import` tag allows you to use [macros](macro) defined in another template.

Assuming that a macro named `input` exists in a template called `form_util` you can import it like so:

```
{% import "form_util" %}

{{ input("text", "name", "Mitchell") }}
```

## Dynamic Import
The `import` tag will accept an expression to determine the template to import at runtime. For example:
```
{% import modern ? 'ajax_form_util' : 'simple_form_util' %}

{{ input("text", "name", "Mitchell") }}
```

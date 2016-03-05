# `import`
The `import` tag allows you to use [macros](macro) defined in another template.

Assuming that a macro named `input` exists in a template called `form_util` you can import it like so:

```
{% import "form_util" %}

{{ input("text", "name", "Mitchell") }}
```
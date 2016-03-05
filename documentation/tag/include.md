# `include`

The `include` tag allows you to insert the rendered output of another template directly into the
current template. The included template will have access to the same variables that the current template does.

```
Top Content
{% include "advertisement" %}
Bottom Content
{% include "footer" %}
```
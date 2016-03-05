# `block`
The `block` function is used to render the contents of a block more than once. It is not to be confused
with the block *tag* which is used to declare blocks.

The following example will render the contents of the "post" block twice; once where it was declared
and again using the `block` function:
```
{% block "post" %} content {% endblock %}

{{ block("post") }}
```
The above example will output the following:
```
content

content
```

## Performance Warning
The `block` function will impair the use of the [flush](../tag/flush) tag used within the block being rendered.
It is typically okay for a block to use the `flush` tag which will flush the already-rendered
content to the user-provided `Writer` but the block function will internally use it's own `StringWriter` and
therefore flushing inside the block will no longer do any good (nor will it do harm).
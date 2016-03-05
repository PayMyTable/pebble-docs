# `parallel`
The `parallel` tag allows you to designate a chunk of content to be rendered using a new thread.
This tag is only available if you provide an `ExecutorService` to the main `PebbleEngine`.

```
{{ upperContent }}

{% parallel %}
    {{ calculation.slowCalculation }}
{% endparallel %}

{{ lowerContent }}
```
In the above example, the slow calculation will not block the `lowerContent` from being evaluated concurrently.

See the [high performance guide](../guide/high-performance) for more tips on how to improve performance.
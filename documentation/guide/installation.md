# Installation & Configuration
## Installation
Pebble is hosted in the Maven Central Repository. Simply add the following dependency into your `pom.xml` file:
```
<dependency>
	<groupId>com.mitchellbosecke</groupId>
	<artifactId>pebble</artifactId>
	<version> 2.1.0 </version>
</dependency>
```
## Set Up
If you are integrating Pebble with Spring MVC, read [this guide](spring-integration).

You will want to begin by creating a `PebbleEngine` which is responsible for coordinating the retrieval and
compilation of your templates:
```
PebbleEngine engine = new PebbleEngine.Builder().build();
```
And now, with your new `PebbleEngine` instance you can start compiling templates:
```
PebbleTemplate compiledTemplate = engine.getTemplate("templateName");
```
Finally, simply provide your compiled template with a `Writer` object and a Map of variables to get your output!
```
Writer writer = new StringWriter();

Map<String, Object> context = new HashMap<>();
context.put("name", "Mitchell");

compiledTemplate.evaluate(writer, context);

String output = writer.toString();
```

## Template Loader
The `PebbleEngineBuilder` will also accept a `Loader` implementation as an argument. A loader is responsible for
finding your templates.

Pebble ships with the following loader implementations:

- `ClasspathLoader`: Uses a classloader to search the current classpath.
- `FileLoader`:  Finds templates using a filesystem path.
- `ServletLoader`:  Uses a servlet context to find the template. This is the recommended loader for use within an
application server but is not enabled by default.
- `StringLoader`: Considers the name of the template to be the contents of the template.
- `DelegatingLoader`: Delegates responsibility to a collection of children loaders.

If you do not provide a custom Loader, Pebble will use an instance of the `DelegatingLoader` by default.
This delegating loader will use a `ClasspathLoader` and a `FileLoader` behind the scenes to find your templates.

## Pebble Engine Settings

All the settings are set during the construction of the `PebbleEngine` object.

| Setting  | Description | Default |
| --- | --- | --- |
| `cache` | An implementation of a guava cache that the Pebble engine will use to cache compiled templates. If you set the cache to null this will disable all caching and templates will be recompiled with every invocation of engine.getTemplate(...). | An implementation that will hold a maximum of 200 templates.|
| `defaultLocale` | The default locale which will be passed to each compiled template. The templates then use this locale for functions such as i18n, etc. A template can also be given a unique locale during evaluation.  | `Locale.getDefault()` |
| `executorService` | An `ExecutorService` that allows the usage of some advanced multithreading features, such as the `parallel` tag. | `null` |
| `loader` | An implementation of the `Loader` interface which is used to find templates. | An implementation of the `DelegatingLoader` which uses a `ClasspathLoader` and a `FileLoader` behind the scenes. |
| `strictVariables` | If set to true, Pebble will throw an exception if you try to access a variable or attribute that does not exist (or an attribute of a null variable). If set to false, your template will treat non-existing variables/attributes as null without ever skipping a beat. | `false` |



# Integration with Spring 3

## Example
There is a fully working example project located on [github](http://github.com/mbosecke/pebble-example-spring)
which can be used as a reference. It is a very simple and bare-bones project designed to only portray the basics.
To build the project, simply run `mvn install` and then deploy the resulting war file to a an application container.
For your convenience, a built version of the example project is currently being hosted
[here](http://www.mitchellbosecke.com/pebble-example-spring).

## Setup
First of all, make sure your project includes the `pebble-spring3` dependency.
This will provide the necessary `ViewResolver` and `View` classes.
```
<dependency>
	<groupId>com.mitchellbosecke</groupId>
	<artifactId>pebble-spring3</artifact>
	<version>${pebble.version}</version>
</dependency>
```
Secondly, make sure your templates are on the classpath (ex. `/WEB-INF/templates/`). Now you want to define a
`PebbleEngine` bean and a `PebbleViewResolver` in your configuration.
```
@Configuration
@ComponentScan(basePackages = { "com.example.controller", "com.example.service" })
@EnableWebMvc
public class MvcConfig extends WebMvcConfigurerAdapter {

    @Autowired
    private ServletContext servletContext;

    @Bean
    public Loader templateLoader(){
        return new ServletLoader(servletContext);
    }

    @Bean
    public PebbleEngine pebbleEngine() {
        return new PebbleEngine(templateLoader());
    }

    @Bean
    public ViewResolver viewResolver() {
        PebbleViewResolver viewResolver = new PebbleViewResolver();
        viewResolver.setPrefix("/WEB-INF/templates/");
        viewResolver.setSuffix(".html");
        viewResolver.setPebbleEngine(pebbleEngine());
        return viewResolver;
    }

}
```
Now the methods in your `@Controller` annotated classes can simply return the name of the template as you
normally would if using JSPs:
```
@Controller
@RequestMapping(value = "/profile")
public class ProfileController {

	@Autowired
	private UserService userService;

	@RequestMapping
	public ModelAndView getUserProfile(@RequestParam("id") long id) {
		ModelAndView mav = new ModelAndView();
		mav.addObject("user", userService.getUser(id));
		mav.setViewName("profile");
		return mav;
	}

}
```
The above example will render `\WEB-INF\templates\profile.html` and the "user" object will be available
in the evaluation context.

## Features

### Access to Spring beans
Spring beans are now available to the template:
```
{{ beans.beanName }}
```

### Access to http request
HttpRequest is available like this. Really useful to get the context path when outputting href.
```
{{ request.contextPath }}
```

### Access to http session
HttpSession is available like this:
```
{{ session.maxInactiveInterval }}
```
# Spring Tutorial Notes

## [Serving Web Content](https://spring.io/guides/gs/serving-web-content/)

A class is defined as a controller using the `@Controller` annotation:

```Java
@Controller
public class HelloController {
    ...
}
```

Create URL mappings with the `@RequestMapping` annotation on a method:

```Java
@RequestMapping("/greeting")
public String greeting(@RequestParam(value="name", required = false, defaultValue = "World") String name, Model model) {
    model.addAttribute("name", name);
    return "greeting";
}
```

* The annotation maps all requests to `/greeting` to this method
  * RequestMapping can be scoped to just GET, PUT, POST, etc, but defaults to handling all HTTP operations by default
  * To narrow mappings down to just GET, use `@RequestMapping(method=GET)`
* The `@RequestParam(value="name", required = false, defaultValue = "World") String name` parameter of the method binds the value of the query String parameter `name` to the `name` parameter of the `greeting()` method.
  * The parameter is not required, and if unsupplied will default to "World"
  * The value of the `name` parameter is added to a `Model` object, making it accessible to the view template (huh?)
  * The method body here relies on a [view technology](https://spring.io/understanding/view-templates), in this case [Thymeleaf](http://www.thymeleaf.org/doc/tutorials/2.1/thymeleafspring.html), to perform server-side rendering of the HTML. Similar to JSF?

View:

```HTML
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Serving Web Content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Hello, ' + ${name} + '!'" />
</body>
</html>
```

## Devtools

Spring provides the optional `spring-boot-devtools` dependency which can help speed up development by providing features such as 'hot swapping' which allow changes to be made without restarting an app to apply code changes. Also:

* Switches template engines to disable caching
* Enables LiveReload to refresh browser automatically (nice!)
* Other reasonable defaults based on development instead of production

## Building the Application

Although it is possible to package this service as a traditional WAR file, this tutorial packages everything into a single executable JAR file, with a classic `main()` method and an embedded Tomcat servlet container to provide the HTTP runtime.

The `main()` class `src/main/java/com/joshdoug/web/Application.java`:

```Java
package com.joshdoug.web;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

* `@SpringBootApplication` is a convenience annotation that adds:
  * `@Configuration` tags the class as a source of bean definitions for the application context
  * `@EnableAutoConfiguration` tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings
  * Normally `@EnableWebMvc` needs to be added for a Spring MVC app, but Spring Boot adds it automatically when it sees `spring-webmvc` on the classpath. This flags the application as a web application and activates key behaviours such as setting up a `DispatcherServlet`
  * `@ComponentScan` tells Spring to look for other components, configurations, and services in the `com.joshdoug.web` package, allowing it to find the controllers
# Apache Tomcat

* [Tomcat 9.0 Documentation Index](https://tomcat.apache.org/tomcat-9.0-doc/index.html)

## Configuration

The main configuration file for a Tomcat application is the web.xml, this is similar to the Main class of a Java application and is where Tomcat will look to figure out which pages to display.

### Servlet Creation and Configuration

When using IntelliJ, the Web panel (accessible alongside Project, Structure, Favourites, etc on the left, or via View > Tool Windows > Web) can be used to manage and add to the project, e.g. select the Web module node and create a new Servlet. Alternatively manually creating the Servlet in the `src` folder and typing/copy-pasting the boiler plate code also works.

Making the Servlet accessible can be done using xml configuration in the web.xml file, or more conveniently by using annotations, e.g. `@WebServlet(name = "TestServlet", urlPatterns = {"/testServlet"})`, much nicer.

* [WebServlet Annotation Docoumentation](https://javaee.github.io/javaee-spec/javadocs/javax/servlet/annotation/WebServlet.html)
* [IntelliJ IDEA Serlvet Documentation](https://www.jetbrains.com/help/idea/servlets.html)

## Issues & Workarounds

IntelliJ doesn't support the latest Java EE descriptor/XML namespaces, so these have to be changed manually for Tomcat 9:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee/"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee/
          http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
           version="4.0">

</web-app>
```

Hopefully once Tomcat 9 hits stable IntelliJ sorts this out.

IntelliJ will also complain that the URI is not registerd and it cannot resolve the symbol, but that doesn't seem to matter as only Tomcat needs to care about that.
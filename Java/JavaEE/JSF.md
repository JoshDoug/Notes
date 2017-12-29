# JavaServer Faces (JSF)

Java spec for building component-based UIs for web applications.

* [Java Server Faces Spec Page](https://javaee.github.io/javaserverfaces-spec/)
* Current spec version for Java EE 8 in 2017 is JSF 2.3

## Implementations

* Oracle Mojarra - Reference Implementation, coordinates:
  * `org.apache.myfaces.core:myfaces-api:2.2.12`
  * `org.apache.myfaces.core:myfaces-impl:2.2.12`
  * Both are necessary (I think?)
* [Apache MyFaces](http://myfaces.apache.org/)
* PrimeFaces - not an implementation, but builds on top of JSF implementations

## Introduction

JSF is part of the presentation* layer and is used for web frontend user interfaces, using an MVC design pattern. Also includes:

* Facelets view language
* Data binding
* AJAX support
* Alternative template frameworks (pluggable ecosystem), such as PrimeFaces

* Presentation layer typically includes JSP, JSF, JAX-RS, WebSockets, and Servlet.

## Faces Life Cycle

* Restore view
* Apply request values
* Process validations
* Update model values
* Invoke application
* Render response

## Mojarra JavaServer Faces

*Oracle's open source implementation of the JSF standard.*

* [Oracle Mojarra Site](https://javaserverfaces.github.io/)
* [Repo with useful ReadMe](https://github.com/javaserverfaces/mojarra)

## Apache Myfaces

* [Apache MyFaces Site](https://myfaces.apache.org/index.html)
* [MyFaces Documentation](https://myfaces.apache.org/wiki/)

### [Introduction to JSF](https://myfaces.apache.org/jsfintro.html)

Note: *Might be outdated*

JSF is the standard for web-development frameworks in Java, based on the MVC paradigm and is addtionally (like most web-frameworks) component-based and event-orientated.

JSF applications are typically built using Facelets, xml/xhtml components. Prior to this other templating languages such as JSP and Shale Clay were also used.

The rest of the Quick Start guide is laughably outdated or non-functional.

### [MyFaces Core User Guide](https://myfaces.apache.org/wiki/core/user-guide.html)

## IntelliJ

To add JSF support to a basic web project (Tomcat with a Web Module template) is not at all obvious, go to Project Settings (`⌘;`) > Modules, right click the Web dropdown under the Project Module name, choose `+ add` and JSF should be listed there, then the option to download/setup the JSF jars will be available and IntelliJ will work.

Alternatively, use Maven and import the dependencies.
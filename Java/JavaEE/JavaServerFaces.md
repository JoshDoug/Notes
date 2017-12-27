# JavaServer Faces (JSF)

Java spec for building component-based UIs for web applications.

* [Java Server Faces Spec Page](https://javaee.github.io/javaserverfaces-spec/)
* Current spec version for Java EE 8 in 2017 is JSF 2.3

## Implementations

* Oracle Mojarra - Reference Implementation
* [Apache MyFaces](http://myfaces.apache.org/)
* PrimeFaces - not an implementation, but builds on top of JSF implementations

## Introduction

JSF is part of the presentation* layer and is used for web frontend user interfaces, using an MVC design pattern. Also includes:

* Facelets view language
* Data binding
* AJAX support
* Alternative template frameworks (pluggable ecosystem), such as PrimeFaces

* Presentation layer typically includes JSP, JSF, JAX-RS, WebSockets, and Servlet.

## IntelliJ

To add JSF support to a basic web project (Tomcat with a Web Module template) is not at all obvious, go to Project Settings (`⌘;`) > Modules, right click the Web dropdown under the Project Module name, choose `+ add` and JSF should be listed there, then the option to download/setup the JSF jars will be available and IntelliJ will work.
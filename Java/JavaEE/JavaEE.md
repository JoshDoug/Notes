# Notes on Java Enterprise Edition

Notes on JavaEE or whatever it ends up being called

## Links to Documentation and Tutorials

* [Oracle Java EE 7 Documentation](https://docs.oracle.com/javaee/7/index.html)
* [Oracle Java EE 7 Tutorial](https://docs.oracle.com/javaee/7/tutorial/)
* [Java EE Spec Repo](https://github.com/javaee/javaee-spec) & [Java EE GitHub Spec Site](https://javaee.github.io/javaee-spec/)
* [Java EE 8 Spec Docs ?](https://javaee.github.io/javaee-spec/javadocs/)
* [List of Java EE Specs and Reference Implementations](https://javaee.github.io/javaee-spec/Specifications)
* [ReadLearnCode Java EE blog posts](https://readlearncode.com/category/java-ee/)
* [Java EE Tutorial](https://javaee.github.io/tutorial/) & [ToC](https://javaee.github.io/tutorial/toc.html)
* [Java EE Tutorial Repo](https://github.com/javaee/tutorial)
* [First Cup Tutorial](https://javaee.github.io/firstcup/), [First CUP ToC](https://javaee.github.io/firstcup/toc.html), and [First Cup Repo](https://github.com/javaee/firstcup-examples)
* [JCP - Java Community Process](jcp.org) - spec development process
* [Java EE 7 Example Application - Cargo Tracker](https://github.com/javaee/cargotracker)
* [List of Web containers](https://en.wikipedia.org/wiki/Web_container)

## History, Present, Future (Present being Java EE7)

History:

* JPE Project - 1998
* J2EE 1.2 - 1999, Enterprise Java Platform with 10 specs such as Servlet, JSP, EJB, JMS, RMI/IOP
* J2EE 1.3 - 2001, 13 specs, Focus on Robustness, with CMP, Connector Architecture added
* J2EE 1.4 - 2003, 20 specs, Focus on Web Services, with Web Services, Managed, Deploymnet, Asynchronous Connector added
* Java EE 5 - 2006, 23 specs Focus on ease of development, Annotations, EJB 3.0, Persistence API, New and Updated Web Services (shift from XML & configuration to Annotations and convention)
* Java EE 6 - 2009, 28 specs, Focus on flexibility, extensibility, profiles, CDI, RESTful web services, EJB Lite, Managed Beans 1.0, and more.
* Java EE 7 - 2013, 28+ specs (33 APIs/Specs?), growth slows, fine tuning and improved programmer friendliness.
* Java EE 8 - focus on Cloud and Microservices, improvements to Servlets, CDI, JSON-P, JSF, JAX-RS, Bean Validation, and addition of JSON-B, Security, Configuration, and Health Check - 37 APIs?
  * [What's new in Java EE 8](http://www.oracle.com/technetwork/java/javaee/overview/index.html)
* Java EE 9 or whatever comes next will continue this focus on cloud and microservices.

Java EE is:

* A set of APIs and runtime
* Consists of 28+ specifications
* All Java SE APIs can be used in combination with any Java EE component
* Annotation-based configuration, XML is (mostly?) optional, and convention over configuration
* Contexts and Dependency Injection (CDI)

## [Java EE 8 Specifications](http://www.oracle.com/technetwork/java/javaee/tech/index.html)

Spec and version, JSR, Yes (if included in Web Profile), _*bold and italic*_ if new/updated

* _Java EE Platform_
  * _*Java Platform, Enterprise Edition 8 (Java EE 8), JSR 366*_
* _Web Application Technologies_
  * _*Java API for WebSocket 1.1, JSR 356, Yes*_
  * _*Java API for JSON Binding 1.0, JSR 367, Yes*_
  * _*Java API for JSON Processing 1.1, JSR 374, Yes*_
  * _*Java Servlet 4.0, JSR 369, Yes*_
  * _*JavaServer Faces 2.3, JSR 372, Yes*_
  * Expression Language 3.0, JSR 341, Yes
  * JavaServer Pages 2.3, JSR 245, Yes
  * Standard Tag Library for JavaServer Pages (JSTL) 1.2, JSR 52, Yes
* _Enterprise Application Technologies_
  * Batch Applications for the Java Platform 1.0, JSR 352
  * Concurrency Utilities for Java EE 1.0, JSR 236
  * _*Contexts and Dependency Injection for Java 2.0, JSR 365, Yes*_
  * Dependency Injection for Java 1.0, JSR 330, Yes
  * _*Bean Validation 2.0, JSR 380, Yes*_
  * Enterprise JavaBeans 3.2, JSR 345, Yes
  * Interceptors 1.2, JSR 318, Yes
  * Java EE Connector Architecture 1.7, JSR 322
  * _*Java Persistence 2.2, JSR 338, Yes*_
  * _*Common Annotations for the Java Platform 1.3, JSR 250, Yes*_
  * Java Message Service API 2.0, JSR 343
  * Java Transaction API (JTA) 1.2, JSR 907, Yes
  * _*JavaMail 1.6, JSR 919*_
* _Web Services Technologies_
  * _*Java API for RESTful Web Services (JAX-RS) 2.1, JSR 370, Yes*_
  * Implementing Enterprise Web Services 1.3, JSR 109
  * Web Services Metadata for the Java Platform 2.1, JSR 181
  * Java API for XML-Based RPC (JAX-RPC) 1.1 (Optional), JSR 101
  * Java API for XML Registries (JAXR) 1.0 (Optional), JSR 93
* _Management and Security Technologies_
  * _*Java EE Security API 1.0, JSR 375, Yes*_
  * Java Authentication Service Provider Interface for Containers 1.1, JSR 196, Yes
  * Java Authorization Contract for Containers 1.5, JSR 115
  * Java EE Application Deployment 1.2  (Optional), JSR 88
  * J2EE Management 1.1, JSR 77
  * Debugging Support for Other Languages 1.0 JSR 45, Yes
* _Java EE-related Specs in Java SE_
  * Java Management Extensions (JMX) 2.0, JSR 3
  * SOAP with Attachments API for Java (SAAJ) Specification 1.3, JSR 67
  * Streaming API for XML (StAX) 1.0, JSR 173
  * Java API for XML Processing (JAXP) 1.6, JSR 206
  * Java Database Connectivity 4.0, JSR 221
  * Java Architecture for XML Binding (JAXB) 2.2, JSR 222
  * Java API for XML-Based Web Services (JAX-WS) 2.2, JSR 224
  * JavaBeans Activation Framework (JAF) 1.1, JSR 925

## Java EE Server Implementations

There are over 20 compliant Java EE implementations, here's a shortlist of some of the more popular options:

* GlassFish (Reference Implementation from Oracle, but moving to Eclipse?)
* Oracel WebLogic (Oracle's commercial implementation)
* Apache TomEE (Supports the Web Profile subset of Java EE APIs)
* Apache Tomcat (Doesn't fully implement Java EE either)
* RedHat JBoss Enterprise Platform
* WildFly
* WebSphere Liberty by IBM, built atop OpenLiberty
* Payara (Commercially supported and built on top of GlassFish)

Full Platform offers a complete Java EE solution for complete enterprise solutions, whereas the web profile offers only those technologies that are necessary for a fully functioning web application.

## Application Layers

Examples of the typical APIs that make up each layer of a typical Java EE application:

* Presentation Layer: JSP, JSF, JAX-RS, WebSockets, Servlet
* Business Layer: Facade, EJB, Entities
* Data Access Layer: JPA, JCA, JMS, Batch Processing
* Crosscutting Layer: Bean Validation, CDI, Interceptor, Transaction, Security, JSON-P

## [Java EE Tutorial](https://javaee.github.io/tutorial/toc.html)

### Preface

Related links:

* [GlassFish Server documentation](https://javaee.github.io/glassfish/documentation)
* [Java EE Spec](https://javaee.github.io/javaee-spec/)
* [Apache Derby Docs](https://db.apache.org/derby/docs/10.13/adminguide/)
* [GlassFish Samples](https://javaee.github.io/glassfish-samples/)

Default Paths and File Names:

* `as-install` - base install directory for GlassFish Server or the SDK of which GlassFish is a part of, e.g. `/Applications/Servers/glassfish5/glassfish`.
* `as-install-parent` - parent of the base install directory for GlassFish Server, e.g. `/Applications/Servers/glassfish5`
* `tut-install` - represents the base install directory for the Java EE Tutorial after installing GlassFish Server or the SDK and run the Update Tool, e.g. `as-install-parent/docs/javaee-tutorial`
* `domain-dir` - represents the directory in which a domain's configuration is stored, e.g. `as-install/domains/domain1`

### Part 1: Introduction

### Chapter 1: Overview

Chapter introduces Java EE application development, covers development basics, Java EE architecture & APIs, important terms & concepts, and how to approach Java EE application programming, assembly, & depolyment.

#### Introduction to Java EE

The Java EE platform developed through the Java Community Process (JCP), expert groups create Java Specification Requests (JSRs) to define the various Java EE Technologies to help provide tools, software and APIs that can be used to build distributed, transactional, portable applications that are fast, secure, performant, and reliable.

The Java EE platform used a simplified programming model (compared to what?), XML descriptors are optional and instead a developer can use annotations directly in a Java source file. There's also dependency injection, helping to hide the creation and lookup of resources from application code, but I don't really understand that yet.

#### Java EE 8 Platform Highlights

* HTML5 and HTTP/2 Support
* [Java API for JSON Binding](https://javaee.github.io/tutorial/overview008.html#java-api-for-json-binding)
* [Java EE Security API](https://javaee.github.io/tutorial/overview008.html#java-ee-security-api)
* [Java API for JSON Processing](https://javaee.github.io/tutorial/overview008.html#java-api-for-json-processing) improvements, such as JSON Pointer, Patch, and Merge Patch.
* New features for:
  * RESTful web services ([Java API for RESTful Web Services](https://javaee.github.io/tutorial/overview008.html#java-api-for-restful-web-services))
  * Servlets ([Java Servlet Technology](https://javaee.github.io/tutorial/overview008.html#java-servlet-technology))
  * JavaServer Faces ([JavaServer Faces Technology](https://javaee.github.io/tutorial/overview008.html#javaserver-faces-technology))
  * Contexts and Dependency Injections features ([CDI for Java EE](https://javaee.github.io/tutorial/overview008.html#contexts-and-dependency-injection-for-java-ee))
  * JavaBean validation ([Been Validation](https://javaee.github.io/tutorial/overview008.html#bean-validation))

#### Java EE Application Model

Lots of corporate jargon and marketing speak, but basically Java EE provides a basis for creating complex enterprise level applications.

#### Distributed Multitiered Applications

The Java EE platform uses a distributed multitiered application model for enterprise applications, kinda like MVC on steroids. Application logic is divided into components according to function, and the applications components that make up a Java EE application are installed on various machines depending on the tier in the multitiered Java EE environment to which the application belongs (or it could all be on one machine, of course).

A typical multitiered application would have a client application/webpage, a Java EE Server, and a Database:

* Client-tier components run on the client machine (Application Client &/or Web Pages).
* Web-tier components run on the Java EE server (JavaServer Faces Pages).
* Business-tier components run on the Java EE server (Enterprise Beans).
* Enterprise information system (EIS)-tier software runs on the EIS server (Databases).

Security: it does some stuff for you? Unclear from the description.

Java EE Components: Java EE applications are made up of components which are a self-contained functional software unit that is assembled into a Java EE application with its related classes and files and that communicates with other components. The Java EE spec defines the following components:

* Application clients and applets are components that run on the client.
* Java Servlet, JavaServer Faces, and JavaServer Pages (JSP) technology components are web components that run on the server.
* EJB components (enterprise beans) are business components that run on the server.

> "Java EE components are written in the Java programming language and are compiled in the same way as any program in the language. The differences between Java EE components and "standard" Java classes are that Java EE components are assembled into a Java EE application, they are verified to be well formed and in compliance with the Java EE specification, and they are deployed to production, where they are run and managed by the Java EE server."

*So...they're normal Java but they run on a Java EE Server?*

[More info on the tutorial site](https://javaee.github.io/tutorial/overview004.html).

#### [Java EE Containers](https://javaee.github.io/tutorial/overview005.html)

_Write this section up at a later date once I can make sense of the marketing speel_.

#### [Web Services Support](https://javaee.github.io/tutorial/overview006.html)

Java EE platform provides XML APIs and tools for designing, developing, testing, and deploying web services that use open XML-based standards and transport protocols.

SOAP (Simple Object Access Protocol) Transport Protocol - An XML-based protocol that is transmitted over HTTP. following the HTTP request-and-response model.

WSDL (Web Services Description Language) Standard Formt - A standardised XML format for describing network services, description includes the name, location and ways to communicate with the service. GlassFish Server provides a tool for generating the WSDL spec of a web service that uses remote procedure calls to communicate with clients.

#### Java EE Application Assembly and Deployment

A Java EE application is packaged into one or more standard units for deployment to any Java EE platform-compliant system. Each unit contains:

* A functional component or components, such as an enterprise bean, web page, servlet, or applet
* An optional deployment descriptor that describes its content

Once a Java EE unit has been produced, it is ready to be deployed. Deployment typically involves using a platform’s deployment tool to specify location-specific information, such as a list of local users who can access it and the name of the local database. Once deployed on a local platform, the application is ready to run.

#### Java EE 8 APIs

Summaries of the technologies required by the Java EE platform and the APIs used in Java EE applications.

##### Enterprise JavaBeans Technology

An Enterprise JavaBeans (EJB) component, or enterprise bean, is a body of code that has fields and methods to implement modules of business logic and is used as a building block, standalone or with other EJBs to execute business logic on the Java EE server.

Enterprise beans are either session beans or message-driven beans:

* A session bean
* A message-driven bean

##### Java Servlet Technology

##### JavaServer Faces Technology

##### JavaServer Pages Technology

##### JavaServer Pages Standard Tag Library

##### Java Persistence API

##### Java Transaction API

##### Java API for RESTful Web Services

##### Managed Beans

##### Contexts and Dependency Injection for Java EE

##### Dependency Injection for Java

##### Bean Validation

##### Java Message Service API

##### Java EE Connector Architecture

##### JavaMail API

##### Java Authorization Contract for Containers

##### Java Authentication Service Provider Interface for Containers

##### Java EE Security API

##### Java API for WebSocket

##### Java API for JSON Processing

##### Java API for JSON Binding

##### Concurrency Utilities for Java EE

##### Batch Applications for the Java Platform

#### Java EE 8 APIs in the Java Platform, Standard Edition 8

#### GlassFish Server Tools

## [First Cup Tutorial](https://javaee.github.io/firstcup/toc.html)
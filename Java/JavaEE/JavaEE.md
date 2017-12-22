# Notes on Java Enterprise Edition

Notes on JavaEE or whatever it ends up being called

## Links to Documentation and Tutorials

* [Oracle Java EE 7 Documentation](https://docs.oracle.com/javaee/7/index.html)
* [Java EE Spec Repo](https://github.com/javaee/javaee-spec) & [Java EE GitHub Spec Site](https://javaee.github.io/javaee-spec/)
* [Java EE 8 Spec Docs ?](https://javaee.github.io/javaee-spec/javadocs/)
* [List of Java EE Specs and Reference Implementations](https://javaee.github.io/javaee-spec/Specifications)
* [ReadLearnCode Java EE blog posts](https://readlearncode.com/category/java-ee/)
* [Java EE Tutorial](https://javaee.github.io/tutorial/) & [ToC](https://javaee.github.io/tutorial/toc.html)
* [Java EE Tutorial Repo](https://github.com/javaee/tutorial)
* [First Cup Tutorial](https://javaee.github.io/firstcup/), [First CUP ToC](https://javaee.github.io/firstcup/toc.html), and [First Cup Repo](https://github.com/javaee/firstcup-examples)

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

#### Distributed Multitiered Applications

#### Java EE Containers

#### Web Services Support

#### Java EE Application Assembly and Deployment

#### Java EE 8 APIs

#### Java EE 8 APIs in the Java Platform, Standard Edition 8

#### GlassFish Server Tools

## [First Cup Tutorial](https://javaee.github.io/firstcup/toc.html)
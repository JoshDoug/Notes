# [Javadoc Technology](https://docs.oracle.com/javase/8/docs/technotes/guides/javadoc/index.html)

## Basic Overview

JavaDoc is a Java tool included with the JDK that can extract and build HTML documentation for a Java application or library from the source code. It does this with information from class and method comments as well as the source directly.

A JavaDoc comment differs from a typical multiline comment by starting with two asterisks:

```Java
/**
 *
 */
```

This signals to the JavaDoc tool that this is a JavaDoc comment. It can also included inline HTML markup.

## IntelliJ

You can generate a JavaDoc in IntelliJ by selecting the option under the tools menu. This prompts a popup which gives you several options such as where to put the docs, and options for including private and package-private code, or scoping it to protected & public, for example.
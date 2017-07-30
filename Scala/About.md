# Scala - Scalable Language

Used in the Akka and Spark tools because of its scalability and easy integration with Java.
Scala runs on the JVM and naturally combiens OO design with functional programming, Scala classes can call Java methods and inherit from Java classes.

Scala was started in 2003 as a research project in Switzerland and was released in 2004. It is currently version 2.12.3 as of writing this.

Scala has a REPL, has access to all Java libraries and tools, and is statically typed. It is a pure OO language with no primitive data types, and even functions are considered objects. So Scala is both functional and object orientated. Functions can be passed to other functions and returned from functions, functions can even be assigned to variables. Scala supports higher-order functions, nested functions, and currying (what is that?). Scala has lightweight syntax for anonymous functions, aka Lambda functions, and also includes Generic classes, Variance annotations, Uuper and lower type bounds, Inner classes and abstract types as object members, compound types, explicitly typed self-references, implicit parameters and conversions, polymorphic methods. Crikey.

Scala is easily integrated with Java, all java.lang classes are automatically imported, other classes can be explicitly imported. Scala can call any Java code, subclass and existing Java class, and implement any Java interface. The reverse is also true, Java code can call into Scala code if the Scala code subclasses a Java class or implements a Java interface.

## Installing Scala

Scala's [website](https://www.scala-lang.org/), and GitHub [repo](https://github.com/scala/scala).

IntelliJ IDEA also has a Scala plugin which deals with the setup.

## SBT - Scala Build Tool

A build tool for Scala, version 0.13.16 as of writing this, with 1.0 in devel.

## [Dotty](http://dotty.epfl.ch/)

Dotty is a 'next generation compiler for Scala', and is offered as an alternate compiler when using IDEA. It can easily be installed with Homebrew.
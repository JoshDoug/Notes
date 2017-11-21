# Up and Running with Java 9

* [Documentation](https://docs.oracle.com/javase/9/)
* [What's new in Java 9 Video](https://youtu.be/9PFcTwRlASY?t=1497)
* [Blog Post](https://blogs.oracle.com/java/features-in-java-8-and-9)
* [Keynote that demos JShell, modules, linking modules](https://www.youtube.com/watch?v=e9eSPtpiGkA)
* [Java 9 Features - List of JEPS](http://openjdk.java.net/projects/jdk9/)
* [Beyond Java 9](http://openjdk.java.net/projects/jdk/)
* [Java 10](http://openjdk.java.net/projects/jdk/10)

## Behind the scenes improvements

Lots of benefits of moving to JDK9 without even making any changes, don't even need to recompile.

* Strings are more effeciently managed by the JVM
* JavaDoc gets a search box, niceeeeeee

## New Release Cycle

There will be a new release every 6 months which are only supported for 6 months, with an LTS every 3 years.

Types of support:

* Public updates: Free public support, possibly with new features.
* Premier Support: Support, if you pay for it.
* Extended Support: Support, if you pay even more for it.
* Sustaining Support: Support on a case by case basis that would be very expensive.

[Oracle Java Support page](http://www.oracle.com/technetwork/java/eol-135779.html).

## New features & functionality

### Project Jigsaw (JSR 376) - modularise the Java Platform

A JSR can contain one or more JEPs, here are the JEPs associated with JSR 376:

* JEP 200: The Modular JDK
* JEP 201: Modular Source Code
* JEP 220: Modualr Run-Time Images
* JEP 260: Encapsulate Most Internal APIs
* JEP 261: Module System
* JEP 282: jlink: The Java Linker

The main goals are to ensure reliable configuration (with a better alternative to the classpath), and strong encapsulation.

* JDK divided into set of modules
* JDK modules can be convined into a variety of configurations instead of just using a monolithic runtime
  * Configurations can be used to create equivalents to compact profiles, but are more flexible and useful
  * Custom configurations can be made with a reduced set of modules
* Restructures the JDK and JRE runtime images
  * Improves performance, security, and maintainability
* Defines a new URI (Uniform Resource Identifier)
  * The new URI scheme is used for naming modules, classes, and resources that are stored in a runtime image.
* Makes most of the JDK's internal APIs inaccessible by default

Use the `jdeps` tool, e.g. `jdeps -jdkinternals Example.class` to test for the use of internal APIs.

#### jlink

Now that it's more common for a Java application to contain its own runtime, it makes sense for that runtime to be tailored to the application.
Only ship as much of the runtime as necessary, instead of shipping a monolithic JRE. Probably best for IOT devices. So you can create a runtime image that only contains the Java plaftform modules your application needs, as well as packaging your application within the image. Also useful for use with containers!

#### Enhanced Deprecation

Addition to deprecations, condemned: `@Deprecated(since=9, condemned=true)` this means the usage isn't just discouraged or has a better new replacement, but it means that it is actually up for removal in a future release, most likely the next version.

Tool jdeprscan searches for depreactated code: [jdeprscan tool documentation](https://docs.oracle.com/javase/9/tools/jdeprscan.htm)

#### Convenience Factory Methods for Collections

Covered in JEP 269

#### JShell REPL (JEP 222)

Try out new APIs without having to write a bunch of boilerplate.

Covered in this section by JShell.md.

#### Mutli-Release JAR Files

tools/jar

Extend the JAR file format to allow multiple, Java-release-specific versions of class files to coexist in a single archive. Sounds interesting, but might not be something I ever use...useful for Uni where computers are on an older JRE?

Write JDK-version-specific variants of the same code into a single jar file. Sounds like a lot of work, but if you're already doing it and distributing multiple JARs..then seems like a no brainer.

But how does this work on different operating systems - release a jar per OS? Kinda messes up the point of Java surely, or have a runtime environment that can detect the OS and contains a bunch of redundant code for other OSs?

## Process API Updates

* Controls and manages OS processes
* Update extends Java's ability to interact with the OS
* The ProcessHandle class provides access to critical data
  * Examples: native process ID, arguments, command, start time, accumulated CPU time, user, parent process, and descendants
  * Get PID of the current JVM process
  * Enumerate processes running in the system
  * Manage process trees
  * Manage subprocesses

## New adopted standards

* Unicode 8.0
* OCSP Stapling for TLS - what.
  * Allows app to circumvent additional ping to CA to check Cert is still valid
* SHA-3 Hash Algo
* HTML5 Javadoc
* HTTP/2 Client - on an incubator module (JEP 11) will be added to the standard in a later release

## Housekeeping

Encapsulate Most Internal APIs

* Basically sun.misc.Base64, Unsafe, etc
* Not using these internal APIs so doesn't matter to me anyway.
* Can check with `jdeps` tool, included in JDK

Modular Java Application Packaging - jlink again

* Integrate features from Jigsaw into the Java Packager, including module awareness and customer runtime creation

Cont:

* New version string: 9.x.x using semver, Semantic Versioning, instead of 1.9_X.xblah weirdness
* JEP 295: AOT Compilation (Ahead of time compilation), tool `jaotc`
* Unified GC Logging
* Make G1 the Default Garbage Collector
# Up and Running with Java 9

* [Documentation](https://docs.oracle.com/javase/9/)
* [What's new in Java 9 Video](https://youtu.be/9PFcTwRlASY?t=1497)
* [Blog Post](https://blogs.oracle.com/java/features-in-java-8-and-9)
* [Keynote that demos JShell, modules, linking modules](https://www.youtube.com/watch?v=e9eSPtpiGkA)

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

### Project Jigsaw - modularised the Java Platform

* JEP 261: Module System
* JEP 200: The Modular JDK
* JEP 201: Modular Source Code
* JEP 220: Modualr Run-Time Images
* Plus
  * JEP 260: Encapsulate Most Internal APIs
  * JEP 282: jlink: The Java Linker

#### jlink

Now that it's more common for a Java application to contain its own runtime, it makes sense for that runtime to be tailored to the application.
Only ship as much of the runtime as necessary, instead of shipping a monolithic JRE. Probably best for IOT devices. So you can create a runtime image that only contains the Java plaftform modules your application needs, as well as packaging your application within the image. Also useful for use with containers!

#### Enhanced Deprecation

Addition to deprecations, condemned: `@Deprecated(since=9, condemned=true)` this means the usage isn't just discouraged or has a better new replacement, but it means that it is actually up for removal in a future release, most likely the next version.

Tool jdeprscan searches for depreactated code: [jdeprscan tool documentation](https://docs.oracle.com/javase/9/tools/jdeprscan.htm)

#### Convenience Factory Methods for Collections

Covered in JEP 269

#### JShell REPL

Try out new APIs without having to write a bunch of boilerplate.

#### Mutli-Release JAR Files

tools/jar

Extend the JAR file format to allow multiple, Java-release-specific versions of class files to coexist in a single archive. Sounds interesting, but might not be something I ever use...useful for Uni where computers are on an older JRE?

Write JDK-version-specific variants of the same code into a single jar file. Sounds like a lot of work, but if you're already doing it and distributing multiple JARs..then seems like a no brainer.

But how does this work on different operating systems - release a jar per OS? Kinda messes up the point of Java surely, or have a runtime environment that can detect the OS and contains a bunch of redundant code for other OSs?

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
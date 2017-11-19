# Java Modules

*A module is a set of packages designed for reuse.*

* Java 9 Modularity book
* [Java 9 Modularitt book code examples](https://github.com/java9-modularity/examples)

## Java 9 Modularity Notes

Notes are on concepts and defintions that may be useful to revisit, not general introductory or contextual content. Most headings will be shown for the sake of structure, but may be shortly summarised or not at all, in which case just revisit the book.

### Chapter 1: Modularity Matters

#### What Is Modularity

Modularity aims to manage and reduce complexity through decomposition of a system through abstractions into components with consistent interfaces. Modules are identifiable artifacts containing code, with metadata describing the module and its relation to other modules. An application then consists of multiple modules working together.

Modules group related code, but beyond that they must adhere to 3 core tenets:

* *Strong Encapsulation:* A module must be able to conceal part of its code from other modules. By doing so, a clear line is drawn between code that is publicly usable and code that is deemed an internal implementation detail. This prevents accidental or unwanted coupling between modules: you simply cannot use what has been encapsulated. As a result, encapsulated code may change freely without affecting user of the module.
* *Well-defined Interfaces:* Encapsulation is good, but for modules to work together, not everything can be encapsulated. Code that is not encapsulated is, by definition, part of the public API of the module. Since other modules can use this public code, it must be managed with great care. A breaking change in non-encapsulated code can break other moduels that depend on it. Therefore, modules should expose well-defined and stable interfaces to other modules.
* *Explicit Dependences:* Modules often need other modules to fulfill their obligations. Such dependencies must be part of the module definition, in order for modules to be self-contained. Explicit dependencies give rise to a *module graph*: nodes represent modules, and edges represent dependencies between modules. Having a module graph is important for both understanding an application and running it with all necessary modules. It provides the basis for a reliable configuration of modules.

#### Before Java 9

Java has method encapsulation, basic package encapsulation (protected classes), but it's limited. Interfaces and factories can also be used with dependency injection to provide a level of encapsulation. Maven has helped with compile time dependency management, including managing transient dependencies, and the OSGi framework does run-time managemnt, but more can be done.

#### Jars As Modules

Kind of, but not really - has no strong encapsulation, limited to convention which is easily and often ignored.

#### Classpath Hell

Classpath Hell and Jar Hell are common terms in the Java community for a reason, they're bad. Modules can help with this.

#### Java 9 Modules

Java 9 brings a module system for application use, which has also been used within Java itself to modularise the JRE and JDK.

The Java 9 Module System adheres to the 3 core tenets of modualarity, modules can either export or strongly encapsulate packages, and they can express dependencies on other modules explicitly.
The module system and included metadata provide much more detail about the structure of an application and its dependencies than the flat list of classpath JARs.

The module system brings many beneifts, here are some of the most important ones:

* *Reliable Configuration*: The module system checks whether a given combination of modules satisfies all dependencies before compiling or running code. This leads to fewer run-time errors.
* *Strong Encapsulation*: Modules explicitly choose what to expose to other modules. Accidental (or intentional) dependencies on internal implementation details are prevented.
* *Scalable Development*: Explicity boundaries enable teams to work in parallel while still creating maintainable codebases. ONly explicitly exported public types are shared, creating boundaries that are automatically enforced by the module system.
* *Security*: Strong encapsulation is enforced at the deepest layers inside the JVM. This limits the attack surface of the Java runtime. Gaining reflective access to sensitive internal classes is not possible anymore. But what does this mean for libraries that make extensive use of reflection?
* *Optimisation*: Because the module system knows which modules belong together, including platform modules, no other code needs to be considered during JVM startup. It also opens up the possibility to create a minimal configuration of modules for distribution. Furthermore, whole-program optimisations can be applied to such a set of modules. Before modules, this was much harder, because explicit dependency information was not available and a class could reference any other class from the classpath.

### Chapter 2: Modules and the Modular JDK

The main contents of Java are shipped in `rt.jar`, rt short for runtime, which weighs in at over 60MBs and contains legacy code and bloat such as CORBA. With Java 9's modularity, developers don't need to include that extra cruft in their deployments. Encapsulating classes and having the option of unused modules also dramatically reduces the attack surface of Java.

#### The Modular JDK

A basic step towards a more modular JDK was taken in Java 8 with the introduction of *compact profiles*, which were subsets of packages from the standard library. There were three profiles, `compact1`, `compact2`, and `compact3`, each profile is a superset of the previous, building more packages on top that can be used. This is still very limited compared to the modular system in Java 9.

* `compact1`: Smalled profile with Java core classes and logging and scripting APIs.
* `compact2`: Extends compact1 with XML, JDBC, and RMI APIs
* `compact3`: Extends compact2 with security and management APIs

This worked as an intermediate solution, but ultimately a more flexible appraoch was necessary. Java 9 splits the JDK into about 90 platform modules, instead of a monolithic library.

The Java module system does not allow compile-time circular dependencies between modules, which is good as they're generally an indicator of bad design.

* `java --list-modules` - lists all modules in the currently installed JDK

Incubator Modules: A simple way to add unstable implementations for testing purposes while still making clear that the API may change or be removed. This is covered by Java Enhancement Proposal (JEP) 11. An example of this in Java 9 is a new http client, `jdk.incubator.httpclient@9`.

#### Modular Descriptors

A module descriptor is used to store the metadata of a module, such as its name, and what is exposed, the module descriptor lives in a file called `module-info.java`.

Example `module-info.java` for the `java.prefs` platform module:

```Java
module java.prefs {
    requires java.xml;

    exports java.util.prefs;
}
```

* `requires` - this keyword indicates a dependency, in this case on `java.xml`
* A single package from the `java.prefs` module is exported to other modules.

Modules live in a global namespace and as such the module names must be unique. As with packages, conventions such as reverse DNS notation can be used to ensure uniqueness for modules. A module descriptor always starts with the `module` keyword, followed by the name of the module. Then, the body of `module-info.java` describes other characteristics of the module (if any).

The body of the module descriptor specifies a dependency on `java.xml` with the `requries` keyword, dependencies are enforced by the module system and this dependency needs to be declared otherwise it will not compile. The implicit dependency of `java.base` doesn't need to be added, much like it's unneccessary to import `java.lang.String` to a class using strings. A module descriptor can also contain `exports` statements. Strong encapsulation is the default for modules, only when a package is explicitly exported, such as `java.util.prefs` in the example, can it be accessed from other modules.

#### Readability

By having dependencies explicitly stated in the module descriptor the readability of the structure of an application nad the relationships between the modules is improved.

#### Accessibility

Normal access modifiers still work the same within a module, but importantly even a public class is innaccessible to other modules unless the package it is in is explicity exported. If a package is exported then the code inside behaves in much the same way as pre-Java 9, with protected, -(default, package private), and private all behaving as they used to. This is important when considering the design of an application, it's important to design a package structure where types meant for external consumption are clearly seperated from internal implementation concerns. Essentially exported packages within a module form the API of the module. Even if the exported packages are not intended to signify an official API, third parties might treat them that way.

Reflection is no longer all powerful when confronted with the module system and has to respect the strong encapsulation of a package, but packages that are exported should work the same way with reflection.

#### Implied Readability

Implied readability covers the use of transitive dependencies. For example, `java.sql` makes use of `java.xml`, but use of the `java.sql` API will likley also return xml objects and as such use of `java.sql` will likely result in a dependency on `java.xml` in the module using `java.sql` (still following?). As such it makes sense for `java.sql` to pass on it's xml dependency to classes that are dependent on it, this can be done with the `transitive` keyword used in conjunction with `requries`. The transitive dependency declaration for `java.sql` would be: `requrires transitive java.xml`, so now any module using `java.sql` will also have a dependency on `java.xml` automatically. This is used in aggregator modules such as `java.se` and `java.se.ee` which contain no code and instead aggregate several modules so that the list of modules to `require` is shortened, this is done by `java.se`'s module descriptor listing all the relevant modules as `require transitive`.
# Java Modules

*A module is a set of packages designed for reuse.*

* Java 9 Modularity book
* [Java 9 Modularity book code examples](https://github.com/java9-modularity/examples)

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

Implied readability covers the use of transitive dependencies. For example, `java.sql` makes use of `java.xml`, but use of the `java.sql` API will likley also return xml objects and as such use of `java.sql` will likely result in a dependency on `java.xml` in the module using `java.sql` (still following?). As such it makes sense for `java.sql` to pass on its xml dependency to classes that are dependent on it, this can be done with the `transitive` keyword used in conjunction with `requries`. The transitive dependency declaration for `java.sql` would be: `requrires transitive java.xml`, so now any module using `java.sql` will also have a dependency on `java.xml` automatically. This is used in aggregator modules such as `java.se` and `java.se.ee` which contain no code and instead aggregate several modules so that the list of modules to `require` is shortened, this is done by `java.se`'s module descriptor listing all the relevant modules as `require transitive`.

#### Qualified Exports

It will sometimes be useful to expose a package only to certain other modules, and this can be done with *qualified exports*. An example of a qualified export can be found in the `java.xml` module descriptor:

```Java
mdoule java.xml {
    ...
    exports com.sun.xml.internal.stream.writers to java.xml.ws;
    ...
}
```

This resricts the `com.sun.xml.internal.stream.writers` to just `java.xml.ws`. Multiple module names, seperated by a comma, can be provided as targets for a qualified export.

It's probably best to avoid using qualified exports if possible, although in cases such as the JDK with a large legacy code base it may be useful as a means to migrate to modules.

#### Module Resolution and the Module Path

Modules are resolved from the *module path*, as opposed to the classpath. Whereas the classpath is a flat list of types, the module path contains only modules, and these modules carry explicit information on what packages they export, making the module path efficiently indexable. The Java runtime and compiler know exactly which module to resolve from the module path when looking for types from a given package. Previously a scan through the whole classpath was the only way to locate an arbritary type.

When an application packaged as a module is run, it needs all of its dependencies as well. Module resolution is the process of computing a minimal required set of modules fiven a dependency graph and a *root module* chosen from tha graph. Every module reachable from the root module ends up in the set of *resolved modules*. Mathematically speaking, this amounts to computing the *transitive closure* of the dependency graph.

When modules are resolved some checks are performed, e.g. two modules with the same name will lead to an error at startup (rather than a run-time classloading failure). Another check is for uniqueness of exported packages, only one module on the module path may expose a given package. "Split Packages" is discussed on page 94 of the book.

Versions - these are deliberately outside the scope of the module system. Versioned modules are discussed on page 106 of the book.

#### Using the Modular JDK Without Modules

With Java 9 modules are opt-in, prior applications should continue to work as before without any modifications. When the module system is not explicitly used then the classpath continues to be used as it would in prior versions. But when the module system is not being explicitly used, it is still being used because the JDK now uses the module system, as a result all code compiled outside a module is added to an *unnamed module*. This unnamed module reads all other modules, but you've still got to deal with the classpath. This implicit use of the module system voids almost all the benefits. Also running code compiled on a prior version of Java behaves a little differently, with a more lenient form of strong encapsulation being used to avoid breakage. There are some other differences, see the book, page 31.

### Chapter 3: Working with Modules

Practical work - building a hello world module and then a running example project called EasyText.

#### Your First Module

This will examine a Modular 'Hello World' and everything involved in creating and using it.

##### Anatomy of a Module

Starting out with a single class, in a package, leading to a single module. Modules may only contain types that are inside packages, so a package definition is required.

Hello World:

```Java
package com.javamodularity.helloworld;

public class HelloWorld {
    public static void main(String... args) {
        System.out.println("Hello Modular World");
    }
}
```

Interesting that the book example uses varargs instead of the typical main String array.

The folder structure of the project:

```tree
src
└── helloworld
    ├── com
    │   └── javamodularity
    │       └── helloworld
    │           └── HelloWorld.java
    └── module-info.java

5 directories, 2 files
```

There are two differences to the project structure from a normal Java project. First there is the module folder, helloworld, which encompasses the module and is named after the name of the module. Secondly there is the module descriptor, in the file `module-info.java`. The module descriptor signals to Java that we're working with modules. The module descriptor must always be within the root of the module folder, and is compiled along with other source files into a binary class-file called `module-info.class`.

The module descriptor:

```Java
module helloworld {

}
```

This is a minimal module descriptor, just for the purpose of a Hello World example. The module is declared with the `module` keyword, followed by the module name. The module name must match the name of the module directory otherwise it wont compile (although in a single module scenario this isn't the case, but it's still good practice). Although the descriptor is empty it does still implicitly depend on `java.base`. The `module` keyword is only treated as a keyword inside `module-info.java` so this wont affect conflict with the use of `module` as a keyword in other source files, this makes it a restricted keyword.

##### Naming Modules

Modules convey the high-level structure of an application, so naming is important. Module names live in a gloabl namespace separate from other namespaces in Java. Technically this means a module name can the same as a class, interface, or package, but in practice this should be avoided. Modules names must be unique, the reverse DNS notation for packages can be used, but it's cluncky. It's preferable to choose shorter, more readable module names, although if the module will be part of widely used library then uniqueness is important.

##### Compilation

Compiling the Hello World example from above as would be done in Java 8:

```bash
javac -d out src/helloworld/com/javamodularity/helloworld/HelloWorld.java
```

To run:

```bash
cd out
# Tab complete will work for the package name
java com.javamodularity.helloworld.HelloWorld
```

Compiling the Hello World example from above using Java 9 modules:

```bash
javac -d out/helloworld \
         src/helloworld/com/javamodularity/helloworld/HelloWorld.java \
         src/helloworld/module-info.java
```

To run:

```bash
java --module-path out \
     --module helloworld/com.javamodularity.helloworld.HelloWorld
```

The flags have shorter alternatives, `-p` can be used insted of `--module-path`, and `-m` instead of `--module`.

Resulting directory structure, aka the *exploded module* format:

```tree
out/
└── helloworld
    ├── com
    │   └── javamodularity
    │       └── helloworld
    │           └── HelloWorld.class
    └── module-info.class
```

There are two notable differences here:

* `helloworld` is specified as an output directory, reflecting the module name (the directory doesn't have to be the same name, but it's good practice)
* `module-info.java` is added as a source file to compile, this also triggers the module-aware mode of javac.

###### Compiling multiple modules

So far the 'single-module mode' of the Java compiler has been used, but typically projects will consist of multiple modules either as 3rd party dependencies or different modules within an application. For these cases additional compiler flags have been added: `--module-source-path` and `--module-path`, these are the module-aware counterparts of `-sourcepath` and `-classpath`.

###### Build tools

Most of the time the Java compiler isn't interacted with directly, and is instead used via Maven, Gradle, or other build tools. But for comprehensive coverage of the compiler flags and general use of the tool there is [official documentation](https://docs.oracle.com/javase/9/tools/tools-and-command-reference.htm#JSWOR596).

##### Packaging

Modules can be packaged into JARs in much the same way as before, resulting in *modular* JAR files, which are like a normal JAR file but also containing a *module-info.class*.

To package up the modular Hello World example:

```bash
mkdir mods
jar -cfe mods/helloworld.jar com.javamodularity.helloworld.HelloWorld -C out/helloworld .
```

Here the `-c` stands for create, `-f` for the archive filename (helloworld.jar), `-e` for the 'entry point' or main method (the package declaration and main Class `com.javamodularity.helloworld.HelloWorld`), and `-C` changes to the specified directory and includes the following file or directory. The arguments can be bunched at the start of specified before each argument, both work.

The filename of the jar isn't technically important as the module is identified by the `module-info.class` packaged within the jar.

##### Running Modules

Modules can be run using the previously shown example using an exploded module:

```bash
java --module-path out \
     --module helloworld/com.javamodularity.helloworld.HelloWorld
```

This can be simplified when running the modular JAR:

```bash
java --module-path mods --module helloworld
```

This is because when the module is packaged into a JAR a manifest is automatically created with the entry point. In both these cases the helloworld module is the root module for execution, the JVM starts from this root module and then resolves any other modules necessary to run the root module from the module path (none in this case). If a module necessary to helloworld wasn't on the module path this would cause an error at startup rather than when the JVM tries to load a non-existant class at runtime.

##### Module Path

The module path is a list of paths to individual modules and directories containing modules. Each directory can contain zero or more module definitions, and the module definition can be an exploded module or a modular JAR. Example module path containing all three options: `out/:explodedmodule/:packagedmodule.jar`, here any modules (exploded or JARs) within the `out` dir are included, the exploded module is included, and the modular JAR is included.

Note: on Linux & macOS the module path uses a colon, `:`, as a seperator, while on Windows a semicolon, `;`, is used.

Module selection: if two modules within the same directory on the module path have the same name then the resolver will show an error, however if the two modules are in different directories then the first module is selected and the subsequent modules with the same name are ignored. _*Confusing*_

##### Linking Modules

Java 9 has an optional linking phase (inbetween the compile and run-time phases) that can be used to create custom runtime images that only contain the necessary modules to run an application. These are often much smaller than the usual runtime image, which has benefits on storage, overhead, and security.

```bash
jlink --module-path mods/:$JAVA_HOME/jmods \
      --add-modules helloworld \
      --launcher hello=helloworld \
      --output helloworld-image
```

* The `--module-path` option constructs the module path, containing mods where the modular JAR is, and the JDK directory where the platform modules are contained. Unlike javac and java, jlink requires that platform modules be explicitly added to the module path.
* The `--add-modules` options indicates that helloworld is the root module that needs to be runnable in the runtime image.
* The `--launcher` option defines the entry point to directly run the module in the image.
* The `--output` option indicates that directory name for the runtime image.

The result is a directory containing essentially a Java runtime completely tailored to running helloworld:

```tree
.
├── bin
│   ├── hello
│   ├── java
│   └── keytool
├── conf
│   └── ...
├── include
│   └── ...
├── legal
│   └── ...
├── lib
│   └── ...
└── release
```

The important parts are `bin/hello`, an executable script that directly launches the helloworld module, and `bin/java` which is the Java runtime capable of resolving only helloworld and its dependencies.

Note: jlink is not added to the system path by default, so it needs to be added manually like so:

```bash
# Ensure jlink is added to PATH
export PATH="/Library/Java/JavaVirtualMachines/jdk-9.jdk/Contents/Home/bin:$PATH"
```

#### No Module Is an Island

Of course the main advantages of modules come into play when composing more than one of them.

##### Introducing the EasyText Example

EasyText will be the example project, starting off as a single monolithic module before being split and added to. It's use will be to analyse text complexity. Here are the requirements of the application:

* Must have the ability to add new analysis algorithms without modifying or recompiling existing modules
* Different frontends (e.g. GUI & CLI) must be able to reuse the same analysis logic
* Must support different configurations, without recompilation and without deploying all code for each configuration

Technical requirements:

* Read the input text, either from the GUI or an input file
* Split the text into sentences and words (as many readability formulas work with sentence and/or word level metrics)
* Run one or more analyses on the text
* Show the result to the user

These requirements can all be met without modules, but modules certainly help and improve the result.

The starting example (chapter3/easytext-singlemodule), easytext, is just a single package within a single module, similar to HelloWorld.

##### A Tale of Two Modules

In the example the text-analysis algorithm and the main program are seperated into two modules, `easytext.analysis` and `easytext.cli`. This allows the analysis module to be reused with different frontends (a GUI) later on. The cli handles the cli and file parsing logic. The `Main` class in `easytext.analysis` delegates the analysis to the `FleshKincaid` class. As there are now two interdependent modules they need to be compiled with the multimodule mode of javac: `javac -d out --module-source-path src -m easytext.cli`, this specifies the output directory, that the modules are in the src directory, and that the root module is `easytext.cli`. Note `easytext.analysis` doesn't need to be specified in the command because it's listed in the module descriptor for `easytext.cli` and can be found in the specified src directory.

Descriptor for the cli module:

```Java
module easytext.cli {
    // Requires analysis module
    requires easytext.analysis;
}
```

Descriptor for the analysis module:

```Java
module easytext.analysis {
    // Exports analysis package
    exports javamodularity.easytext.analysis
}
```

The module system will check for cyclic dependencies between modules, although it's still possible between classes of a module (but not really recommended). Cyclic dependencies between classes of different modules are also blocked. So the `analysis` module cannot require the `cli` module without introducing a cyclic dependency. Indirect cyclic dependencies are also blocked, for example if module A depended on module B which depends on module C which depends on module A (there's a nice simple picture in the book). TKTK - create a diagram in StarUML?

#### Working with Platform Modules

Platform modules come with the Java runtime and provide functionality such as XML parsers, GUI toolkits, and other typical standard library features. They behave the same as application modules but are included with the JDK. EasyText will be extended and as a result will result on some platform modules explicitly, so far it's only relied on java.base which is an implicit dependency.

##### Finding the Right Platform Module

It's necessary to know which platform modules an application depends on as they need to be specified in the module-descriptor. To list all the platform modules run `java --list-modules`, pipe it through `column` to make it easier to read. There are different types of platform modules such as `java.*`, `javafx.*` and `jdk.*`, the `jdk.*` modules contain JDK-specific code and can vary across JDK implementations.

##### Creating a GUI Module

The GUI module implements a basic javafx GUI which requires & reuses the FleschKincaid analyis module, currently the only available algorithm but this will be added to later. The GUI class imports 7 javafx packages, JavaDoc can be used to see which modules these are in. To see what packages a module exports and what modules a module requires from the CLI use the `--describe-module` option, e.g. `java --describe-module javafx.controls`. Most modern IDEs will also automatically import modules into the module descriptor. The easytext GUI requires two javafx modules: `javafx.graphics` and `javafx.controls`.

The GUI also needs to export it's own package so that the javafx.graphics module can access it via reflection to instantiate it as the GUI extends the Application class. Yeah that's confusing and I don't really understand it and yes it seems to be a cyclic dependency, although not an explicit one as that's avoided via reflection. Technically because it's using reflection the dependency only happens at runtime, whereas the cyclic dependency blocking is only enforced at compile time. The resulting module descriptor is:

```Java
module easytext.gui {
    exports javamodularity.easytext.gui to javafx.graphics;

    requires javafx.graphics;
    requires javafx.controls;
    requires easytext.analysis;
}
```

Using the qualified export ensures that only javafx.graphics is capable of accessing the main GUI class.

#### The Limits of Encapsulation

So far the easytext application has both GUI and CLI frontends which can be swapped and use the analysis code which is also modularised. The nexts steps are to:

* Uncouple the frontends from the FleshKincaid class/concrete analysis implementations
* Frontends should be able to discover new analysis implementations in new modules without any code changes.

##### Interfaces and Instantiation

An interface can be used to provide a stable abstraction for analysis algorithms, but how do you instantiate an instance of an algorithm? Indirection!
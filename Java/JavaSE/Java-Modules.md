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

Kind of, but not really.
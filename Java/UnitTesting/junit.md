# JUnit info

* Example provided by Junit for setting up junit with ant [here](https://github.com/junit-team/junit4/wiki/Getting-started-%E2%80%93-Ant)
* Overview/Introduction to JUnit 5 and the changes from JUnit 4, video: [JUnit 5 by Marc Philipp](https://www.youtube.com/watch?v=0qI6_NKFQsY)

## [JUnit 5](http://junit.org/)

* Documentation: [JUnit 5 Docs](http://junit.org/junit5/docs/current/api/)
* JUnit 5 [User Guide](http://junit.org/junit5/docs/current/user-guide/)
* [Junit 5 Samples](https://github.com/junit-team/junit5-samples)

Note: Junit 5 has some issues with the maven-surefire-plugin version 2.20.1, so use 2.19.1 for the time being.

## 1 Overview

JUnit supports Java 8 or higher.

### What JUnit 5 is

JUnit 5 differs from prior versions in that it is composed of several different modules from three different sub-projects: JUnit Platfrom, JUnit Jupiter, and JUnit Vintage.

* JUnit Platform - a foundation for launching testing frameworks on the JVM and provides a TestEngine API. The basic idea is that other testing frameworks can be built on top of it, including future versions of JUnit.
* JUnit Jupiter - Basically JUnit 5 as far as users are concerned, provides a new programming model and extension model for writing tests and extensions in JUnit 5.
* JUnit Vintage - compatibility with older versions of JUnit 3 and 4.

## 2 Installation

Milestone releases are deployed to Maven Central.

### [2.1 Dependency Metadata](http://junit.org/junit5/docs/current/user-guide/#dependency-metadata)

#### 2.1.1 JUnit Platform

* Group ID: `org.junit.platform`
* Version: `1.0.2` (worth noting?)
* Artficats IDs:
  * `junit-platform-commons` - Internal common library/utils of JUnit. Not intended to be used outside of JUnit itself.
  * `junit-platform-console` - Support for discovering and executing tests on the JUnit Platform from the console, see [Console Launcher](http://junit.org/junit5/docs/current/user-guide/#running-tests-console-launcher) for details.
  * `junit-platform-console-standalone` - An executable JAR with all dependencies included.
  * `junit-platform-engine` - Public API for test engines, see [Plugging in Your Own Test Engine](http://junit.org/junit5/docs/current/user-guide/#launcher-api-engines-custom) for details.
  * `junit-platform-gradle-plugin` - Gradle support.
  * `junit-platform-launcher` - Public API for configuring and launching test plans - typically used by IDEs and build tools, see [JUnit Platform Launcher API](http://junit.org/junit5/docs/current/user-guide/#launcher-api) for details.
  * `junit-platform-runner` - Runner for executing tests and test suites on the JUnit Platform in a JUnit 4 environment, see [Using JUnit 4 to Run the JUnit Platform](http://junit.org/junit5/docs/current/user-guide/#running-tests-junit-platform-runner) for details.
  * `junit-platform-suite-api` - Annotations for configuring test suites on the JUnit Platform, support by the [JUnit Platform runner](JUnitPlatform runner) and possibly by third-party `TestEngine` implementations.
  * `junit-platform-surefire-provider` - Support for discovering and executing tests on the JUnit Platform using [Maven Surefire](http://junit.org/junit5/docs/current/user-guide/#running-tests-build-maven).

#### 2.1.2 JUnit Jupiter

* Group ID: `org.junit.jupiter`
* Version: `5.0.2`
* Artifact IDs:
  * `junit-jupiter-api` - JUnit Jupiter API for [writing tests](http://junit.org/junit5/docs/current/user-guide/#writing-tests) and [extensions](http://junit.org/junit5/docs/current/user-guide/#extensions)
  * `junit-jupiter-engine` - JUnit Jupiter test engine implementation, only required at runtime - but it is required and does seem to be the only dependency that needs to be specified within Maven's POM (other than the plugin dependencies which are declared seperately)!
  * `junit-jupiter-params` - Support for [parameterised tests](http://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests) in JUnit Jupiter.
  * `junit-jupiter-migrationsupport` - Migration support from JUnit 4 to JUnit Jupiter, only required for running selected JUnit 4 rules.

#### 2.1.3 JUnit Vintage

* Group ID: `org.junit.vintage`
* Version: `4.12.2`
* ArtifactID: `junit-vintage-engine` - JUnit Vintage test engine implementation that allows running JUnit tests written in JUnit 3 or JUnit 4 style, on the new JUnit Platform

#### 2.1.4 Optional Dependencies

All the prior listed artifacts have an `optional` dependency in their published Maven POMs on the `@API Guardian JAR`.

* Group ID: `org.apiguardian`
* Version: `1.0.0`
* Artifact ID: `apiguardian-api`

### 2.2 Dependency Diagram

![Dependency Diagram](http://junit.org/junit5/docs/current/user-guide/images/component-diagram.svg)

## 3 Writing Tests

A first test case example from JUnit 5's documentation:

```Java
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

class FirstJUnit5Tests {

    @Test
    void myFirstTest() {
        assertEquals(2, 1 + 1);
    }

}
```

Why is the Assertion import static?

### 3.1 Annotations

All core annotations are located in the `org.junit.jupiter.api` package in the `junit-jupiter-api` module (Is that a Java 9 module?).

JUnit Jupiter supported annotations for configuring tests and extending the framework:

| Annotation | Description |
|------------|-------------|
| @Test | Denotes that a method is a test method, is different to JUnit 4's `@Test` annotation. Such methods are *inherited* unless they are *overridden*. |
| @ParameterizedTest | Denotes that a method is a [parameterised test](http://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests). Such methods are *inherited* unless they are *overridden*. |
| @RepeatedTest | Denotes that a method is a test templte for a [repeated test](http://junit.org/junit5/docs/current/user-guide/#writing-tests-repeated-tests). Such methods are *inherited* unless they are *overridden*. |
| @TestFactory | Denotes that a method is a test factory for [dynamic tests](http://junit.org/junit5/docs/current/user-guide/#writing-tests-dynamic-tests). Such methods are *inherited* unless they are *overridden*. |
| @TestInstance | Used to configure the [test instance lifecycle](http://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle) for the annotated test class. Such annotations are *inherited*. |
| @TestTemplate | Denotes that a method is a [template for test cases](http://junit.org/junit5/docs/current/user-guide/#writing-tests-test-templates) designed to be invoked multiple times depending on the number of invocation contexts returned by the registered [providers](http://junit.org/junit5/docs/current/user-guide/#extensions-test-templates). Such methods are *inherited* unless they are *overridden*. |
| @DisplayName | Declares a custom display name for the test class or test method. Such annotations are not *inherited*. |
| @BeforeEach | Denotes that the annotated method should be executed *before* _each_ `@Test`, `@RepeatedTest`, `@ParameterizedTest`, or `@TestFactory` method in the current class; analagous to JUnit 4's `@Before`. Such methods are *inherited* unless they are *overridden*. |
| @AfterEach | Same as `@BeforeEach`, except after each test, analagous to JUnit 4's `@After`. Such methods are *inherited* unless they are *overridden*. |
| @BeforeAll | Denotes that the annotated method should be executed *before* _all_ `@Test`, `@RepeatedTest`, `@ParameterizedTest`, or `@TestFactory` method in the current class; analagous to JUnit 4's `@BeforeClass`. Such methods are *inherited* (unless they are *hidden* or *overridden*) and must be `static` (unless the "per-class" [test instance lifecycle](http://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle) is used). |
| @AfterAll | Same as `@BeforeAll`, except after all tests, analagous to JUnit 4's `@AfterClass`. Such methods are *inherited* (unless they are *hidden* or *overridden*) and must be `static` (unless the "per-class" [test instance lifecycle](http://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle) is used). |
| @Nested | Denotes that the annotated class is a nested, non-static test class. `@BeforeAll` and `@AfterAll` methods cannot be used directly in a `@Nested` test class unless the "per-class: [test instance lifecycle](http://junit.org/junit5/docs/current/user-guide/#writing-tests-test-instance-lifecycle) is used. Such annotations are not *inherited*. |
| @Tag | Used to declare *tags* for filtering tests, either at the class or method level; analagous to test groups in TestNG (never heard of that) or Categories in JUnit 4. Such annotations are *inherited* at the class level but not at the method level. |
| @Disabled | Used to *disable* a test class or test method; analagous to JUnit 4's @Ignore. Such annotations are not *inherited*. |
| @ExtendWith | Used to register custom [extensions](http://junit.org/junit5/docs/current/user-guide/#extensions). Such annotations are *inherited*. |

Methods annotated with `@Test`, `@TestTemplate`, `@RepeatedTest`, `@BeforeAll`, `@BeforeEach`, `@AfterAll`, or `@AfterEach` annotations must not return a value.

Note: Some annotations may currently be _experimental_, consult the [experimental API table](http://junit.org/junit5/docs/current/user-guide/#api-evolution-experimental-apis) for details.

#### 3.1.1 Meta-Annotations and Composed Annotations

_Reread this section and write it up once I understand it._

### 3.2 Standard Test Class

_*A standard test case.*_, example from JUnit documentation:

```Java
import static org.junit.jupiter.api.Assertions.fail;

import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.Test;

class StandardTests {

    @BeforeAll
    static void initAll() {
    }

    @BeforeEach
    void init() {
    }

    @Test
    void succeedingTest() {
    }

    @Test
    void failingTest() {
        fail("a failing test");
    }

    @Test
    @Disabled("for demonstration purposes")
    void skippedTest() {
        // not executed
    }

    @AfterEach
    void tearDown() {
    }

    @AfterAll
    static void tearDownAll() {
    }
}
```

Note: Neithe test classes nor test methods need to be `public`.

### 3.3 Display Names

Test classes and test methods can declare custom display names - with spaces, special characters, and even emojis - that will be displayed by test runners and test reporting.

```Java
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;

@DisplayName("A special test case")
class DisplayNameDemo {

    @Test
    @DisplayName("Custom test name containing spaces")
    void testWithDisplayNameContainingSpaces() {
    }

    @Test
    @DisplayName("╯°□°）╯")
    void testWithDisplayNameContainingSpecialCharacters() {
    }

    @Test
    @DisplayName("😱")
    void testWithDisplayNameContainingEmoji() {
    }
}
```
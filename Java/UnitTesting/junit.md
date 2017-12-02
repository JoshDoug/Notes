# JUnit info

Example provided by Junit for setting up junit with ant [here](https://github.com/junit-team/junit4/wiki/Getting-started-%E2%80%93-Ant)

Overview/Introduction to JUnit 5 and the changes from JUnit 4, video: [JUnit 5 by Marc Philipp](https://www.youtube.com/watch?v=0qI6_NKFQsY)

## [JUnit 5](http://junit.org/)

* Documentation: [JUnit 5 Docs](http://junit.org/junit5/docs/current/api/)
* JUnit 5 [User Guide](http://junit.org/junit5/docs/current/user-guide/)

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

#### 2.1.1 Junit Platform

* GroupID: `org.junit.platform`
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


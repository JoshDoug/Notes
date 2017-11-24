# JUnit info

Example provided by Junit for setting up junit with ant [here](https://github.com/junit-team/junit4/wiki/Getting-started-%E2%80%93-Ant)

Overview/Introduction to JUnit 5 and the changes from JUnit 4, video: [JUnit 5 by Marc Philipp](https://www.youtube.com/watch?v=0qI6_NKFQsY)

## [JUnit 5](http://junit.org/)

* Documentation: [JUnit 5 Docs](http://junit.org/junit5/docs/current/api/)
* JUnit 5 [User Guide](http://junit.org/junit5/docs/current/user-guide/)

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
  * `junit-platform-console`
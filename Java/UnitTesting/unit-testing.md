# Generic Notes on Unit Testing

Notes on Unit Testing and Test Driven Development (TDD).

* [A Set of Unit Testing Rules](http://www.artima.com/weblogs/viewpost.jsp?thread=126923)
* [Introduction to Test Driven Devlopment](http://agiledata.org/essays/tdd.html)

## The Scope of a Unit Test

A Unit test should be a check on small components of a program with limited scope, such as a method or the interaction of a couple methods.

A test is not a unit test if:

* It talks to a database
* It communicates across a network
* It touches a file system
* It can't run in parrallel with other unit tests
* It has to be specially configured to run (shouldn't need to alter your development environment)

It's not bad to have tests that cover these, but it's important to isolate them from true unit tests to avoid getting bogged down. Tests that cover these are really integration tests instead of unit tests.
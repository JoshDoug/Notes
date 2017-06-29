# [Java Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/index.html)

Java uses exceptions to handle error and other exceptional events.

## [What is an Exception](https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html)

An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions.
The term exception is short for 'exceptional event'.

When an error occurs within a method, the method creates an exception object and hands it off to the runtime system. The object contains information about the error, including its type, and the state of the program when the error occurred. Creating an exception object and handing it to the runtime system is called throwing an exception. After a method throws an exception the runtime system attempts to find something to handle it - which is the ordedred list of methods (the call stack) that had been called to get to the method where the error occurred.

![Call Stack](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-callstack.gif)

The runtime system searches the call stack for a method that can handle the exception - using an exception handler. The search is done in the reverse order in which the methods were called, when an appropiate handler is found the runtime system passes the exception to the handler. The exception handler is appropiate if the type of exception object thrown matches the type that can be handled by the handler. The exception handler that is passed the exception object is said to *catch the exception*. If the runtime systems traverses back up the stack without finding an appropiate exception handler then the runtime system, and then the program, terminate.

![Searching the Call Stack for the exception handler](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-errorOccurs.gif)

Apparently using exceptions to manager errors has some advantages over traditional error-management techniques - but i guess those were before my time. The advantages of this are covered in the [Advantages of Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/advantages.html) section.

## The Catch or Specify Requirement

Code that might throw certain exceptions has to either Catch or Specify, this means either using a try-catch statement or specifying on a method what exceptions it might throw so that a method that uses it uses a try-catch to handle any exceptions that are thrown.

### The Three Kinds of Exceptions

First kind: the checked exception. These are exceptions that a well designed application should anticipate and recover from. Involves a try-catch.

Second kind: the error. These are exception conditions external to the application that the application usually can't anticipate or recover from. E.g. caused by a system or hardware malfunction when reading a file. These could still be caught, but javac will still compile the code without a handler for such an error. Can be caught with try-catch, not required.

Third kind: the runtime exception. These are exceptional conditions that are internal to an application that the application usually cannot anticipate or recover from. These usually indicate programming bugs, such as logic errors or improper API use. Can be caught with a try-catch, but not required and probably best to eliminiate the bug that is the root cause of the exception.

Errors and runtime exceptions are collectively known as unchecked exceptions and are not subject to the 'Catch or Specify Requirement'.

### Bypassing Catch or Specify

[Contreversial](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html).

## [Catching and Handling Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html)

The three exception handler components - the `try`, `catch`, and `finally` blocks - to write an exception handler, and `try`-with, introduced in Java SE7, which is suited to situations with Closeable resources, such as streams.

## How to Throw Exceptions

THe throw statemtn, and the throwable class and its subclasses.

## The try-with-resources Statement

The try-with statement is a try statement that declares one or more resources, a resource is an object that must be closed after the program is finished with it. The try-with-resources ensures that each resource is closed at the end of the statement.

Hmm, what does this mean??

## Unchecked Exceptions - The Convtroversy

THe correct and incorrect use of unchecked excpetions indicated by subclasses of RuntimeException.

## Advantages of Exceptions

The advantages of exceptions to manage errors over traditional error-management techniques.

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

## How to Throw Exceptions

## The try-with-resources Statement

## Unchecked Exceptions - The Convtroversy

## Advantages of Exceptions

# JShell

Using JShell, the Java 9 REPL.

* [Official Java Shell User Guide](https://docs.oracle.com/javase/9/jshell/toc.htm)
* [JShell - Java Platform SE Tools Reference](https://docs.oracle.com/javase/9/tools/jshell.htm#JSWOR-GUID-C337353B-074A-431C-993F-60C226163F00)
* [CalliCoder - JShell Introduction](https://www.callicoder.com/java-9-jshell-repl-tutorial/)

## Intro

JShell is a typical REPL useful for exploring APIs and code snippets.

* To start JShell just run `jshell`, to start it in verbose mode run `jshell -v`.
* To exit JShell run `/exit`.
* For built-in help run `/help`.

## Snippets

Snippets of Java code entered into JShell are immediately evaluated, feedback about results, actions performed, and errors are shown. Use verbose mode to get more feedback.

## Commands

* `/help`
* `/exit`
* `/list` - list currently active snippets typed in or read with `/open`
  * `/list -start` - list the automatically evaluated start-up snippets
  * `/list -all`  - list all snippets including failed, overwritten, dropped, and start-up snippets
  * `/list <name>` - list snuppets with the specified name (preference for active snippets)
  * `/list <id>` - list the snippet with the specified id
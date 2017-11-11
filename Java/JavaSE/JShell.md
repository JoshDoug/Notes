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

Example snippets:

* `int x = 10` - assign variables, no need to add a semicolon
* `x + x` - evaluate expressions, even though this doesn't explicitly assign the result, JShell well give it an Id that can be used to access the result again
* `2 + 2` - same as above, this is assigned to a 'scratch variable', which is accessible via its Id

Mutliline snippets can be entered and the prompt will switch to `...>` until the snippet is entered:

```Java
jshell> String twice(String s) {
   ...>   return s + s;
   ...> }
|  created method twice(String)
```

No public/private is necessary when creating methods. To change a method just reenter it to overwrite the previous definition. Definitions can also be changed in incompatible ways, such as changing the type of a method or variable, this 'replaces' it instead of 'modifying' it.

## Commands

* `/help`
* `/exit`
* `/list` - list currently active snippets typed in or read with `/open`
  * `/list -start` - list the automatically evaluated start-up snippets
  * `/list -all`  - list all snippets including failed, overwritten, dropped, and start-up snippets
  * `/list <name>` - list snuppets with the specified name (preference for active snippets)
  * `/list <id>` - list the snippet with the specified id
* Set feedback level (toggle verbose mode)
  * `/set feedback silent` - no feedback, simplifies prompt
  * `/set feedback concise` - lowers the amount of feedback
  * `/set feedback normal` - set default feedback
  * `/set feedback verbose` - set verbose feedback, same as starting JShell with `-v` option
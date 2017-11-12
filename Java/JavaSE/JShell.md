# JShell

Using JShell, the Java 9 REPL.

* [Official Java Shell User Guide](https://docs.oracle.com/javase/9/jshell/toc.htm)
* [JShell - Java Platform SE Tools Reference](https://docs.oracle.com/javase/9/tools/jshell.htm#JSWOR-GUID-C337353B-074A-431C-993F-60C226163F00)
* [CalliCoder - JShell Introduction](https://www.callicoder.com/java-9-jshell-repl-tutorial/)
* [Interacting with an application using JShell and Netbeans](https://www.youtube.com/watch?v=d6YcG4zEYKc)

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

To call the method just run `twice("Hello, World!")`.

No public/private is necessary when creating methods. To change a method just reenter it to overwrite the previous definition. Definitions can also be changed in incompatible ways, such as changing the type of a method or variable, this 'replaces' it instead of 'modifying' it.

## Commands

JShell commands control the environment and display information within a session. Commands are distinguished from snippets by a leading forward slash, `/`.

* `/help`
* `/exit`
* `/list` - list currently active snippets typed in or read with `/open`
  * `/list -start` - list the automatically evaluated start-up snippets, these are numbered and prefixed with `s` (presumably short for 'start')
  * `/list -all`  - list all snippets including failed, overwritten, dropped, and start-up snippets
  * `/list <name>` - list snuppets with the specified name (preference for active snippets)
  * `/list <id>` - list the snippet with the specified id
* Set feedback level
  * `/set feedback silent` - no feedback, simplifies prompt
  * `/set feedback concise` - lowers the amount of feedback
  * `/set feedback normal` - set default feedback
  * `/set feedback verbose` - set verbose feedback, same as starting JShell with `-v` option
* `/vars` - list currently active variables, to see more options tab complete after enterings the command
  * `/vars -all`
  * `/vars -start` - no startup variables are set by default in JDK9
  * `/vars 1` or `/vars $1` - list snippet 1 which is a variable, both options can be used, difference between them is unclear.
* `/methods` - list currently active methods. Sames as `/vars`, `/methods` has `-all` and `-start` options as well as options to select specific method snippets

## Forward References

To aid exploratory programming JShell accepts method definitions that reference methods, variables, or classes that aren't yet defined. When a method is defined that references undefined methods, variables, or classes, JShell output notes that the method cannot be invoked until they are defined. Due to the nature of JShell any variable defined is within the scope of everything else being used(?). JShell will point out what needs to be declared if a method is invoked.

For example, creating a method to get the volume of a sphere:

```Java
jshell> double volume(double radius) {
   ...>    return 4.0 / 3.0 * PI * cube(radius);
   ...> }
|  created method volume(double), however, it cannot be invoked until variable PI, and method cube(double) are declared
```

Then setting PI but without defining the cube method:

```Java
jshell> double PI = 3.1415926535
PI ==> 3.1415926535
|  created variable PI : double

jshell> volume(2)
|  attempted to call method volume(double) which cannot be invoked until method cube(double) is declared

jshell> double cube(double x) { return x * x * x; }
|  created method cube(double)
|    update modified method volume(double)

jshell> volume(2)
$5 ==> 33.510321637333334
|  created scratch variable $5 : double
```

If the precision of `PI` is changed, and verbose mode is in use, then JShell will warn of the incompatibility with any methods in which `PI` is referenced:

```Java
jshell> BigDecimal PI = new BigDecimal("3.141592653589793238462643383")
PI ==> 3.141592653589793238462643383
|  replaced variable PI : BigDecimal
|    update modified method volume(double) which cannot be invoked until this error is corrected: 
|      bad operand types for binary operator '*'
|        first type:  double
|        second type: java.math.BigDecimal
|          return 4.0 / 3.0 * PI * cube(radius);
|                 ^------------^
|    update overwrote variable PI : double
```

And repeat warnings if a method currently incompatible with `PI` is invoked:

```Java
jshell> volume(2)
|  attempted to call method volume(double) which cannot be invoked until this error is corrected: 
|      bad operand types for binary operator '*'
|        first type:  double
|        second type: java.math.BigDecimal
|          return 4.0 / 3.0 * PI * cube(radius);
|                 ^------------^
```

## Exceptions

In an exception backtrace, feedback identifies the snippet and location within the snippet that the error occurred, similar to how a line number and a class would be given with an IDE. The location within the code snippets is displayed as `#ID:line-number` where the ID identifies the snippet and the line-number identifies the line within the snippet. The `/list` command can then be used to view the snippets, and `/list n` where n is the number corresponding with a snippet Id to narrow down the listed snippets. The `/list` command can take multiple IDs: `/list 1 3` to narrow the output down to just the offending snippets. Example:

```Java
jshell> int divide(int x, int y) {
   ...> return x / y;
   ...> }
|  created method divide(int,int)

jshell> divide(4, 2)
$2 ==> 2

jshell> divide(5, 0)
|  java.lang.ArithmeticException thrown: / by zero
|        at divide (#1:2)
|        at (#3:1)

jshell> /list

   1 : int divide(int x, int y) {
       return x / y;
       }
   2 : divide(4, 2)
   3 : divide(5, 0)

jshell> /list 1 3

   1 : int divide(int x, int y) {
       return x / y;
       }
   3 : divide(5, 0)
```

## Snippet Tab Completion

Tab completion can be used to try and determine what's being entered, if it can't be determined then possible options are listed.

* `div<Tab>` - this will tab complete to the divide method from the Exception snippet examples above
* `System.c<Tab>` - as there are multiple possibilities here, they are listed below the prompt, although any common characters will be added.

At a method call's open parenthesis, tab completion will list possible parameter types:

```Java
jshell> "hello".startsWith(
startsWith(   

jshell> "hello".startsWith(
Signatures:
boolean String.startsWith(String prefix, int toffset)
boolean String.startsWith(String prefix)

<press tab again to see documentation>

jshell> "hello".startsWith(
```

Tabbing again will list documentation for the method:

```Java
jshell> "hello".startsWith(
boolean String.startsWith(String prefix, int toffset)
Tests if the substring of this string beginning at the specified index starts with the
specified prefix.

Parameters:
prefix - the prefix.
toffset - where to begin looking in this string.

Returns:
true if the character sequence represented by the argument is a prefix of the substring of this
          object starting at index toffset ; false otherwise. The result is false if toffset is
          negative or greater than the length of this String object; otherwise the result is
          the same as the result of the expression
                    this.substring(toffset).startsWith(prefix)


<press tab to see next documentation>

jshell> "hello".startsWith(
```

Tabbing again will provide additional documentation (e.g. different parameters), and tabbing again will list all possible completions.

## Snippet Transformation

Importing a class can be done with `Shift+Tab i`, `Shift` and `Tab` at the same time, then followed by `i`. JShell will then provide an option for importing the class, more than one import option could be provided. E.g. `new JFrame<Shift+Tab i>`.

This expression can be converted into a variable declaration with `Shift+Tab v`. So starting with: `jshell> new JFrame("Demo")` and using the keyboard combiniation would result in: `jshell> JFrame  = new JFrame("Demo")`, with the cursor placed before the equals ready to enter the variable name.

If the result of an expression hasn't been imported then `Shift+Tab v` can be used to create the variable and import the class:

```Java
jshell> frame.getGraphics() <Shift+Tab v>
0: Do nothing
1: Create variable
2: import: java.awt.Graphics. Create variable
Choice: 2
Imported: java.awt.Graphics

jshell> Graphics | = frame.getGraphics()
```

Assuming the JFrame in the prior example was called frame, and `|` represent the final cursor position.
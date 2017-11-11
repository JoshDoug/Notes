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

To call the method just run `twice("Hello, World!")`.

No public/private is necessary when creating methods. To change a method just reenter it to overwrite the previous definition. Definitions can also be changed in incompatible ways, such as changing the type of a method or variable, this 'replaces' it instead of 'modifying' it.

## Commands

* `/help`
* `/exit`
* `/list` - list currently active snippets typed in or read with `/open`
  * `/list -start` - list the automatically evaluated start-up snippets
  * `/list -all`  - list all snippets including failed, overwritten, dropped, and start-up snippets
  * `/list <name>` - list snuppets with the specified name (preference for active snippets)
  * `/list <id>` - list the snippet with the specified id
* Set feedback level
  * `/set feedback silent` - no feedback, simplifies prompt
  * `/set feedback concise` - lowers the amount of feedback
  * `/set feedback normal` - set default feedback
  * `/set feedback verbose` - set verbose feedback, same as starting JShell with `-v` option

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
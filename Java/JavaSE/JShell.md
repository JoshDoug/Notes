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

JShell commands control the environment and display information within a session. Commands are distinguished from snippets by a leading forward slash, `/`. Tab after a command to see options, tab again to see a synopis, and tab again to see full documentation for the command.

* `/help`, `/help intro`, `/help /list` or `/help list` or `/he l`
* `/exit`
* `/list` - list currently active snippets typed in or read with `/open`
  * `/list -start` - list the automatically evaluated start-up snippets, these are numbered and prefixed with `s` (presumably short for 'start')
  * `/list -all`  - list all snippets including failed, overwritten, dropped, and start-up snippets
  * `/list <name>` - list snuppets with the specified name (preference for active snippets)
  * `/list <id>` - list the snippet with the specified id
  * `/l` - short alias/abbreviation for `/list`, will also tab complete but doesn't need to be, this also works with options, e.g. `/l -a` to list all
* Set feedback level
  * `/set feedback silent` - no feedback, simplifies prompt
  * `/set feedback concise` - lowers the amount of feedback
  * `/set feedback normal` - set default feedback
  * `/set feedback verbose` - set verbose feedback, same as starting JShell with `-v` option
* `/vars` - list currently active variables, to see more options tab complete after enterings the command
  * `/vars -all`
  * `/vars -start` - no startup variables are set by default in JDK9
  * `/vars 1` or `/vars $1` - list snippet 1 which is a variable, both options can be used, difference between them is unclear.
  * `/v` - short alias
* `/methods` - list currently active methods. Sames as `/vars`, `/methods` has `-all` and `-start` options as well as options to select specific method snippets
  * `/m` - short alias

Commands can be abbreviated provided the abbreviation is unique to a command, e.g. `/se fe v` to set feedback to verbose, this works because `/se` doesn't conflict but just `/s` would conflict with `/save`, and `fe` doesn't conflict, although just `f` would conflict with `format`, and `v` works with `verbose` which is the only feedback argument that starts with v.

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

## Editing

JShell supports editing input at the `jshell` prompt and editing in an external editor. Shell editing enables editing of snippets and commands as they're entered, and to retrieve and previously ented snippets and commands. Alterantively an external editor can be chosen, which is more convenient for multiline snippets.

### Shell Editing

Shell editing in JShell is built on [JLine2](https://github.com/jline/jline2/wiki/Using-JLine), which is functionally similar to BSD `editline` and GNU [`readline`](https://tiswww.case.edu/php/chet/readline/rluserman.html) in Emacs mode.

#### Input Line Navigation

Editing via the prompt, by editing the current line or accessing snippet history. The input line can be navigated with the Ctrl key and Meta/Alt key.

* Left Arrow & Right Arrow, or `C-b` & `C-f` - navigating back and forth by single characters within a line, common Emacs shortcuts
* Up Arrow & Down Arrow - move through history
* `C-a` & `C-e` - move to the start and end of the current line
* `M-b` & `M-f` - move backawards and forwards one word

#### History Navigation

Using example:

```Java
jshell> class FooBar {
   ...> int x;
   ...> int y;
   ...> }
|  created class FooBar
```

Once entered, this class can be edited by using the Up Arrow to move to it in history and edit specific lines (this will move to a line in history, not the snippet as a whole). To move through history by snippets use `C-Up Arrow`. Of course this conflicts with a popular macOS keyboard shortcut, but this just jumps to the first line of each snippet.

This doesn't seem to work as expected for multiline snippets, the line is simply entered as a new snippet on its own, instead of editing that part of the existing snippet.

#### Input Line Modification

* Delete, or `C-d` - delete the character at or after the cursor, as opposd to backspace - deleting the character at or before the cursor
* `C-k` - delete the text from the cursor to the end of the line
* `M-d` - delete the text from the cursor to the end of the word
* `C-w` - delete the text from the cursor to the start of the word/previous whitespace
* `C-y` - paste the most recently deleted text into the line (using the commands above, but not including backspace or `C-d`)
* `M-y` - after `C-y`, `M-y` cycles through previously deleted text

#### Search and More

The search feature works similarly to history searching in Bash. Use `C-r` to enter search, enter a search string and the closest match will be found, use `C-r` again to go to a prior match, or `C-s` to return to a more recent match.

* `C-r` - start search, and search further back through history
* `C-s` - return to more recent history matches

Macros cna be defined with `C-x (`, enter text and finished with `C-x )`, and `C-x e` to use. But I don't really understand them. TKTK.

### External Editor

An editor can be used to edit and create snippets. JShell can be configured to use a specific editor. To edit all existing snippets at one use `/edit` with an option, to edit a specific option use `/edit` with a specific snippet name or ID. E.g. edit the `volume` method defined in the Forward References section: `/edit volume`.

Setting the editor. This can be done with the `/set` command, `/set editor nvim` which will set the editor for the session. If an editor is not set then JShell will check the following environment variables in this order: `JSHELLEDITOR`, `VISUAL`, and `EDITOR`. If none of these are set then a simple editor is used (probably vi?).

New variables, methods, and classes can be defined with the editor, semicolons will still be automatically added when saving and exiting the editor. Exiting the editor restores the JShell prompt.

### External Code

External code is accessible within a JShell sesssion, classes through the class path, modules can be accessed through the module path, additional modules setting, and module exports setting.

#### Setting the Class Path

This can be set when starting JShell: `jshell --class-path myClassPath`, where the class path is either a path or an environment variable containing a path (TKTK?). The code the class path points to must be compiled into class files in directories or JAR files. Code in the default package, aka the unnamed package (?), can't be accessed from JShell. After setting the class path, the packages can be imported into the session.

Alternatively the `/env` command can be used from within the session: `/env --class-path myClassPath`, this will reset the execution state, relaoding any current snippets with the new class path setting.

#### Setting Module Options

JShell supports modules. The module path can be set, additional modules to resolve specified, and module exports given. These options, same as class path, can be set as options when running JShell or with the `/env` command during a session.

Setting module path when starting JShell: `jshell --module-path myOwnModulePath  --add-modules my.module`

Setting module path and other options within a JShell session: `/env --add-modules my.module --module-path myModulePath --class-path myClassPath` (not sure if this is correct or how exactly it works yet, TKTK).

Using `/env` without options will list all the currently set options (nothing by default).

For more details about the options see `/help context` which will give a rundown of each configurable option.
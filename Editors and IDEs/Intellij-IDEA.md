# IntelliJ IDEA

* [JetBrains Confluence Page](https://confluence.jetbrains.com)

## [Meet IntelliJ IDEA](https://www.jetbrains.com/help/idea/meet-intellij-idea.html)

Starter page linking to tutorials.

### [Install and set up IntelliJ IDEA](https://www.jetbrains.com/help/idea/install-and-set-up-intellij-idea.html)

Covers setup on macOS, Windows, Linux, and using Toolbox.

### [Discover IntelliJ IDEA](https://www.jetbrains.com/help/idea/discover-intellij-idea.html)

Walkthrough of the IDE.

#### User Interface

You can access most tool windows via a shortcut and then interact with them, to then return to the editor just hit esc.

|Tool Window|Shortcut|
|-----------|--------|
|Project Files|`⌘1`|
|Navigation Bar|`⌘↑`|
|Version Control|`⌘9`|
|Run|`⌘4`|
|Debug|`⌘5`|
|Terminal|`⌥F12`|
|Editor|`Esc`|

To toggle between hiding & showing all tool windows: `⇧⌘F12` (Shift-Command-Fn-F12).

#### Editor Basics - The most useful editor shortcuts

* [Editor Basics page - more useful editor info](https://www.jetbrains.com/help/idea/editor-basics.html)

|Action|Description|
|------|-----------|
|Move the current line of code|`⇧⌘↑` or `⇧⌘↓`|
|Duplicate a line of code|`⌘D`|
|Remove a line of code|`⌘⌫`|
|Comment/uncomment a line of code|`⌘/`|
|Comment a block of code|`⌥⌘/`|
|Find in the current file|`⌘F`|
|Find and replace in current file|`⌘R`|
|Next occurrence|`⌘G`|
|Previous occurence|`⇧⌘G`|
|Navigate between opened tabs|`⇧⌘]` or `⇧⌘[`|
|Navigate back/forward between last actions*|`⌘]` or `⌘[`|
|Expand or collaps a code block in the editor|`⌘+` or `⌘-`|
|Create a new..|`⌘N`|
|Surround with..**|`⌥⌘T`|
|Highlight usages of a symbol***|`⌘F7`|
|Expand/shrink a selection based on grammar|`⌥↑` or `⌥↓`|
|Select/deslect code|`⌃G` or `⌃⇧G`|

*Navigate back between last places the cursor was put/tab chosen, kinda odd.

**If/else, try/catch etc, not quotes, html tags etc unfortunately. Might be different for different IntelliJ IDEs though.

***E.g. with the cursor in a variable, this will highlight where else the variable is used and allow to shift between them with `⌘G`. Not sure what exactly symbol refers to though...

Note: to try and find the shortcut for an action use the _Find action_ with `⇧⌘A` (Shift-Command-A), type an actions name to see its shortcut or to call it.

#### Code Completion

* [Auto-Completing Code for in-depth info](https://www.jetbrains.com/help/idea/auto-completing-code.html)

Access basic completion by pressing `^Space` to get basic suggestions for variables, types, methods, expressions, etc. Press it again to get more results, including private members and non-imported static members.

Access smart completion by pressing `^⇧Space`, this offers options relevant to the context inlcuding chains.

[Statement Completion](https://www.jetbrains.com/help/idea/auto-completing-code.html#statements_completion) is iniated by pressing `⇧⌘⏎`, this will automatically add missing parentheses, brackets, braces, and the necessary formatting.

To see suggested parameters for any method or constructor press `⌘P`.

The [PostFix Completion](https://www.jetbrains.com/help/idea/auto-completing-code.html#postfix_completion) feature helps transform an already typed expression to anothero ne, based on the postfix typed after a dot.

Still not totally sure how basic and smart completion differ, although on an empty line smart sometimes adds code without providing options, such as methods and arguments in methods. In other cases, such as calling a method on an object, basic and smart will have the same options. Further reading on [basic completion](https://www.jetbrains.com/help/idea/auto-completing-code.html#basic_completion) and [smart completion](https://www.jetbrains.com/help/idea/auto-completing-code.html#smart_completion).

#### Navigation

##### Recent Files

* Use `⌘E` to bring up a window showing tool windows and recent files.
* Navigate to a Class: `⌘O` brings up a search box that can be used to search for Classes
* Navigate to a File: `⇧⌘O` brings up a search box that can be used to search for files or folders (might need to end folder names with a Slash character)
* Navigate to a Symbol: `⌥⌘O` brings up a search box that can be used to find a method or field by its name

##### Structure

Navigate within a file using `⌘F12`, this brings up a modal version of the Structure tool window (it doesn't open or use the normal structure tool window, even if it's already open).

##### Select in

Highlight the current file in a particular tool window (or Finder) with `⌥F1`.

#### Quick pop-ups

|Action|Shortcut|
|------|--------|
|Documentation|`F1`|
|Quick definition|`⌥Space`|
|Show usages|`⌥⌘F7`|
|Show implementation|`⌥⌘B`|

#### Refactoring basics

* [In-depth refactoring info](https://www.jetbrains.com/help/idea/refactoring-source-code.html)

|Action|Shortcut|
|------|--------|
|Rename|`⇧F6`|
|Extract variable|`⌥⌘V`|
|Extract field|`⌥⌘F`|
|Extract a constant|`⌥⌘C`|
|Extract a method|`⌥⌘M`|
|Extract a parameter|`⌥⌘P`|
|Inline|`⌥⌘N`|
|Copy|`F5`|
|Move|`F6`|
|Refactor this|`⌃T`|

Copy and Move refer to methods and fields, instead of currently highlighted code. Need to explore further.

#### Finding usages

* [In-depth Finding Usage info](https://www.jetbrains.com/help/idea/finding-usages.html)

Find Usages helps quickly find all pieces of code referencing the symbol at the caret/cursor, no matter if the symbol is a class, method, field, parameter, or another statement. Use `⌥F7` and get a list of references grouped by usage, type, module, and file.

* To set custom option for Find Usages use: `⌥⇧⌘F7` or the settings option on the Find Usages panel toolbar
* To use plain text search, use Find in Path with `⇧⌘F`

#### Inspections

* [In-depth Code Inspection info](https://www.jetbrains.com/help/idea/code-inspection.html)

Inspections are built-in static code analysis tools to help find possible bugs, locate dead code, detect perf issues, and improve overall code structure. Most inspections point to where the problem is and even offer a quick fix to deal with it using `⌥⏎` (alt-enter) to off one or more fixes.

To perform code analysis on an entire project use *Analyse > Inspect* Code from the main menu, or by slecting *Analyse > Run Inspection by Name*

#### Code style and formatting

See also:

* [Code Style settings](https://www.jetbrains.com/help/idea/code-style.html)
* [Java Code Style settings](https://www.jetbrains.com/help/idea/code-style-java.html)

Useful formatting shortcuts:

|Action|Shortcut|
|------|--------|
|Reformat code|`⌥⌘L`|
|Auto-indent lines|`⌃⌥I`|
|Optimize imports|`⌃⌥O`|

#### [Version control basics](https://www.jetbrains.com/help/idea/discover-intellij-idea.html#VCSBasics)

#### Make

#### Running and debugging

#### Application servers

#### Working with build tools (Maven/Gradle)

### [Mastering IntelliJ IDEA keyboard shortcuts](https://www.jetbrains.com/help/idea/mastering-intellij-idea-keyboard-shortcuts.html)

### [IntelliJ IDEA Pro Tips](https://www.jetbrains.com/help/idea/intellij-idea-pro-tips.html)

### [Keep IntelliJ IDEA up to date](https://www.jetbrains.com/help/idea/keep-intellij-idea-up-to-date.html)

Use Toolbox.

### [Getting Help](https://www.jetbrains.com/help/idea/getting-help.html)

## [Configuring Project and IDE Settings](https://www.jetbrains.com/help/idea/configuring-the-ide.html)

### [Keyboard Shortcuts](https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html)

### [Pro Tips](https://www.jetbrains.com/help/idea/2017.1/intellij-idea-pro-tips.html)

### [Getting Help](https://www.jetbrains.com/help/idea/2017.1/getting-help.html)

## [How-to](https://www.jetbrains.com/help/idea/2017.1/how-to.html)

### [General Guidelines](https://www.jetbrains.com/help/idea/2017.1/general-guidelines.html)

#### [Editor](https://www.jetbrains.com/help/idea/2017.1/intellij-idea-editor.html)

#### [Auto-Completing Code](https://www.jetbrains.com/help/idea/2017.1/auto-completing-code.html)

### [Langauge and Framework-Specific Guidelines](https://www.jetbrains.com/help/idea/2017.1/language-and-framework-specific-guidelines.html)

#### [Java SE](https://www.jetbrains.com/help/idea/2017.1/java-se.html)

##### [Creating, Running and Packaging Your First Java Application](https://www.jetbrains.com/help/idea/2017.1/creating-running-and-packaging-your-first-java-application.html)

#### [Java EE](https://www.jetbrains.com/help/idea/2017.1/java-ee.html)

#### [Developing a Java EE Application](https://www.jetbrains.com/help/idea/2017.1/developing-a-java-ee-application.html)

Developing a Java EE Application. Only supported in Ultimate.

#### [Getting Started with Android Development](https://www.jetbrains.com/help/idea/2017.1/getting-started-with-android-development.html)

#### [Getting Started with Grails](https://www.jetbrains.com/help/idea/2017.1/getting-started-with-grails-3.html)

#### [Getting Started with Groovy](https://www.jetbrains.com/help/idea/2017.1/getting-started-with-groovy.html)

#### [Getting Started with Scala](https://www.jetbrains.com/help/idea/2017.1/creating-and-running-your-scala-application.html)

## [Migration Guides](https://www.jetbrains.com/help/idea/2017.1/migration-guides.html)

Not particularly interesting.

## [Tutorials](https://www.jetbrains.com/help/idea/2017.1/tutorials.html)

## [Reference](https://www.jetbrains.com/help/idea/2017.1/reference.html)

## [IntelliJ Platform SDK  DevGuide](http://www.jetbrains.org/intellij/sdk/docs/index.html)

Developing plugins for IntelliJ.

Useful overview of an IntelliJ [project structure](http://www.jetbrains.org/intellij/sdk/docs/basics/project_structure.html).

## Personal Notes

Tips and tricks I've picked up that I haven't seen specifically outlined in the official documentation, if I find any there I'll migrate them.

### Setting up a project with multiple modules of the same hierachy

Just create a new project but specify the empty option, then create new modules for it. Simples.
# IntelliJ IDEA

* [JetBrains Confluence Page](https://confluence.jetbrains.com)

## [Meet IntelliJ IDEA](https://www.jetbrains.com/help/idea/2017.1/meet-intellij-idea.html)

Starter page linking to tutorials.

### [Discover IntelliJ IDEA](https://www.jetbrains.com/help/idea/2017.1/discover-intellij-idea.html)

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

To toggle between hiding & showing all tool windows: ⇧⌘F12 (Shift-Command-Fn-F12).

#### Editor Basics - The most useful editor shortcuts

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

#### Code Completion

Access basic completion by pressing `^Space` to get basic suggestions for variables, types, methods, expressions, etc. Press it again to get more results, including private members and non-imported static members.

Access smart completion by pressing `^⇧Space`, this offers options relevant to the context inlcuding chains.

[Statement Completion](https://www.jetbrains.com/help/idea/2017.1/auto-completing-code.html#statements_completion) is iniated by pressing `⇧⌘⏎`, this will automatically add missing parentheses, brackets, braces, and the necessary formatting.

To see suggested parameters for any method or constructor press `⌘P`.

The [PostFix Completion](https://www.jetbrains.com/help/idea/2017.1/auto-completing-code.html#postfix_completion)

Still not totally sure how basic and smart completion differ, although on an empty line smart sometimes adds code without providing options, such as methods and arguments in methods. In other cases, such as calling a method on an object, basic and smart will have the same options. Further reading on [basic completion](https://www.jetbrains.com/help/idea/2017.1/auto-completing-code.html#basic_completion) and [smart completion](https://www.jetbrains.com/help/idea/2017.1/auto-completing-code.html#smart_completion)

### [Keyboard Shortcuts](https://www.jetbrains.com/help/idea/2017.1/keyboard-shortcuts-you-cannot-miss.html)

### [Pro Tips](https://www.jetbrains.com/help/idea/2017.1/intellij-idea-pro-tips.html)

### [Getting Help](https://www.jetbrains.com/help/idea/2017.1/getting-help.html)

## [How-to](https://www.jetbrains.com/help/idea/2017.1/how-to.html)

### [General Guidelines](https://www.jetbrains.com/help/idea/2017.1/general-guidelines.html)

### [Langauge and Framework-Specific Guidelines](https://www.jetbrains.com/help/idea/2017.1/language-and-framework-specific-guidelines.html)

#### [Getting Started with Java EE](https://www.jetbrains.com/help/idea/2017.1/developing-a-java-ee-application.html)

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
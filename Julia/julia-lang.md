# Julia Language

## Juno

Juno is the defacto IDE for Julia, and is a plugin for Atom. Julia can also be used via the REPL on the command line or with a text editor.

## Julia and Jupyter with IJulia

IJulia can be used by installing the `IJulia` package with `Pkg.add("IJulia")`, then simply run `notebook()` from the REPL.

* [Using Git and Jupyter notebooks together](http://timstaley.co.uk/posts/making-git-and-jupyter-notebooks-play-nice/)

IJulia sets up a Jupyter notebook which is accessed via a browser (normally) and can include embedded, inline code samples that are runnable.

* Shift + Enter - runs an inline code sample.

## Language Basics

* `;` use a semicolon to suppress output for a statement, postfixed, much likes MatLab does.
* `?` prefix a question mark to get docs for a function
* `;` to use a shell command, *prefix* it with a semicolon
* `#` single line comment
* `#=` starts a multiline comments, `=#` ends a multiline comment
# GHCi

The Glasgow Haskell Compiler interpreter is an interactive Haskell REPL that comes with GHC. At the GHCi prompt you can evaluate expressions, load files and more.

Command list:

* `:load file` shorthand `:l file` - used to load a haskell file, no file extension needs to be specified, e.g. to load test.hs: `:load test`
* `:reload` shorthand `:r` - reload a file that has been edited
* `:type 123` shorthand `:t 123` - ask for the type of an expression
* `:quit` shorthand `:q` - exit GHCi
* `:?` - get a list of commands
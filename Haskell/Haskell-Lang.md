# Haskell Programming Language

Haskell is a pure functional language.

Haskell has 3 installation options, because why not.

* Minimal
* Stack - the modern recommended install, can be installed with Homebrew on macOS
* Haskell Platform - everything included

## Using Haskell with Stack

Going with the assumption Haskell was installed with Stack from now on.

Getting setup:

* `stack setup` installs some additional components
* `stack ghci` setups interpreter/REPL and starts it

* GHC - Glasgow Haskell Compiler
* GHCi - Haskell Interpreter

## Using GHCi

Starting the REPL with `stack ghci` lands you on a prompt called Prelude where you can test out haskell options.

* `:?` list of commands
* `:quit` to quit the REPL
* `123 + 123` returns `246`
* `['H','e','l','l','o']` returns "Hello", Strings in Haskell are just char arrays
* `length "Hello"` returns 5
* `:type True` returns `True :: Bool`
* `:type pi` returns `pi :: Floating a => a` - what?
* `:type 123` returns `123 :: Num t => t`
* `:type "String"` returns `"String" :: [Char]`
* `:info Bool`

Working with files in GHCI:

* Set editor: `:set editor vim` - set the editor to vim, or emacs, or nano, etc
* Load a file: `:load file.txt`
* Run a method: `:load method`
* Run main: `:main`
* Edit file: `:edit` - this will auto reload the file when exiting the editor

## Compiling source code

* Compiling a single file: `stack ghc test.hs` - this will create some intermediate files and an executable

## Built-in Data Structures

### Lists

Simples list examples:

* `['H','e','l','l','o']`
* `[1,2,3,4]`
* `[1.0, 2.0, 3.0, 4.0]`
* `[1..10]` sets a range which returns an array of 1 to 10, similar to R
* `[1,2..10]` returns 1 to 10 but `[1,3..10]` returns `[1,3,5,7,9]` ?
* `1 : []` returns `[1]`, prepends the values to the empty list
* `1 : [2]` returns `[1,2]`
* `1 : 2 : []` returns `[1,2]`
* `1 : [2,3]` returns `[1,2,3]`
* `'h' : 'e' : 'l' : 'l' : 'o' : []` returns `"hello"`
* `'h' : 'e' : "llo"` returns `"hello"`
* `[1,2,3] ++ [4,5,6]` returns `[1,2,3,4,5,6]`
* `head [1,2,3]` returns `1`
* `tail [1,2,3]` returns `[2,3]`

### Tuples

* `(1,2,3,4,5,6)` a tuple of numbers
* `(1, "String", False)` try running `:type` on this
* `[("one", 1), ("two", 2), ("three", 3)]` a list of tuples, can be used like an enum?

Simple dictionary with lookup

Maybe
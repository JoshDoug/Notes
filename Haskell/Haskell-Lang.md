# Haskell Programming Language

Haskell is a pure functional language.

Haskell has 3 installation options, because why not.

* Minimal
* Stack - the modern recommended install, can be installed with Homebrew on macOS
* Haskell Platform - everything included

Links:

* [Haskell Site](https://www.haskell.org/)
* [Haskell Wiki](https://wiki.haskell.org/Haskell)
* [Tutorials](https://wiki.haskell.org/Tutorials)
* [Learning Haskell](https://wiki.haskell.org/Learning_Haskell)
* [School of Haskell](https://www.schoolofhaskell.com/)
* [Why Functional Programming Matters](http://www.cse.chalmers.se/~rjmh/Papers/whyfp.pdf)

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

## Simple variables

To assign a value to a variable in GHCI: `let varName = "A value"`

## Functions

Basic function definitions

A function called add, which takes parameters a and b, and returns a + b: `add a b = a + b` and use the function: `add 12 4` which returns `16`.

Example of a function, called add:

* Function declaration which takes parameters a and b, and returns a + b: `add a b = a + b`
* Calling the function with parameters: `add 12 4` which returns `16`
* Add a type signature before the declaration: `add :: Int -> Int -> Int` - not sure why this is important?

Types

Partial functions - Return a value or an error?
Total functions? - Return a value and always works?

Currying

Point-free style

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

Simple example of a basic dictionary with lookup using a tuple:

* Create tuple dictionary thing: `let dict = [("one", 1), ("two", 2), ("three", 3)]`
* Use lookup function to find corresponding value: `lookup "one" dict`, which returns `Just 1`

Maybe - it may or may not be set? It may or may not return a certain type?

## Building Data Structures

```Haskell
data Compass = North | East | South | West
    deriving(Eq, Ord, Enum, Show)
```
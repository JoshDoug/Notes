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
* `length "Hello"` returns 5
* `:type True` returns `True :: Bool`
* `:type pi` returns `pi :: Floating a => a` - what?
* `:type 123` returns `123 :: Num t => t`
* `:info`
# Haskell Programming Language

Haskell is a pure functional language.

Haskell has 3 installation options, because why not.

* Minimal
* Stack - the modern recommended install, can be installed with Homebrew on macOS
* Haskell Platform - everything included

Components:

* GHC - Glasgow Haskell Compiler
* GHCi - Haskell Interpreter

## Links

* [Haskell Site](https://www.haskell.org/)
* [Haskell Wiki](https://wiki.haskell.org/Haskell)
* [Tutorials](https://wiki.haskell.org/Tutorials)
* [Learning Haskell](https://wiki.haskell.org/Learning_Haskell)
* [School of Haskell](https://www.schoolofhaskell.com/)
* [Why Functional Programming Matters](http://www.cse.chalmers.se/~rjmh/Papers/whyfp.pdf)
* [Why Haskell Matters](https://wiki.haskell.org/Why_Haskell_Matters)
* [Comparison of Haskell to other Functional languages](https://wiki.haskell.org/Comparison)
* [Functional lang FAQ](http://www.cs.nott.ac.uk/~pszgmh//faq.html)
* [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/chapters) (Can buy a hardcopy or read free online)
* [Haskell Wikibook](https://en.wikibooks.org/wiki/Haskell)
* [Yet Another Haskell Tutorial](http://www.umiacs.umd.edu/~hal/docs/daume02yaht.pdf)
* [Functional Programming Course Notes](http://www.staff.science.uu.nl/~fokke101/courses/fp-eng.pdf)

### Monad Links

* [All About Monads](https://wiki.haskell.org/All_About_Monads)
* [IO Inside](https://wiki.haskell.org/IO_inside)
* [You Could Have Invented Monads! (And Maybe You Already Have.)](http://blog.sigfpe.com/2006/08/you-could-have-invented-monads-and.html)
* [Monads for functional programming](http://homepages.inf.ed.ac.uk/wadler/papers/marktoberdorf/baastad.pdf)

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

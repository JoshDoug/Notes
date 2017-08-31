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

## [What is Haskell](https://www.schoolofhaskell.com/school/starting-with-haskell/introduction-to-haskell/1-haskell-basics#what-is-haskell-)

Haskell is a lazy, functional programming language created by a committee of academics in the 1980s using the best ideas from exisiting functional langauges, and a few new ideas of their own.

### Functional

Haskell conforms to the functional programming paradigm:

* Functions are first-class - functions are values which can be used in exactly the same ways as any other sort of value.
* The meaning of Haskell programs is centered around evaluating expressions rather than executing instructions.

This resuolts in an entirely different way of thinking about programming, apparently.

### Pure

Haskell expressions are always referentially transparent (not all functional languages are pure):

* No mutation - Everything (variables, data structures, ...) is immutable.
* No Side effects - expressions never have 'side effects' such as updating global variables or printing to the screen.
* Consistent results - calling the same function with the same arguments results in the same output every time.

This does require a shift in thinking.

* Equational reasoning and refactoring - In Haskell one can always “[replace equals by equals](https://stackoverflow.com/questions/30145271/what-is-meant-by-replace-equals-by-equals)”.
* Parallelism - Evaluating expressions in parallel is easy when they are guaranteed not to affect one another.
* Fewer headaches - Haskell elimintes unrestricted effects and action-at-a-distance which makes for programs that are hard to debug, maintain, and reason about.

### Lazy

In Haskell, expressions are not evaluated until their results are actually needed. This has some consequences, which include:

* Easy to define a new control structure just by defining a function
* Possible to define and work with infinite data structures
* Enables a more compositional programming style
* One major downside though - reasoning about time and space usage becomes much more complicated

### Statically Typed

Speaks for itself: Every Haskell expression has a type, and types are all checked at compile-time. Programs with type errors will not even compile, much less run.

Haskell's type system is apparently great, and not annoying like Java and C++'s type systems are (not sure I've found them annoying though). Part of this is down to Haskell's type system being more expressive.

It helps clarify thinking and express program structure. The first step in writing a Haskell program is usually to write down all the types. Because Haskell's  type ssystem is so expressive, this is a non-trivial design step. *So far this is actually sounding more annoying.*

Serves as a form of documentation. Given an expressive type system, just looking at a function's type tells you a lot about what the function might do and how it can be used, even before you've read a single word of written documentation. *Okay but with well written Java you should be able to garner the same amount of info from a method signature right?*

Turns run-time errors into compile-time errors, some of the time. Okay, so the same as all statically typed langauges then, if you're not doing anything too pesky with generics.

### Abstraction

Haskell is good for abstraction with features like parametric polymorphism, higher-order functions, and type classes which all aid in the fight against repetition.

### Wholemeal programming

A quote from Ralf Hinze:

> “Functional languages excel at wholemeal programming, a term coined by Geraint Jones. Wholemeal programming means to think big: work with an entire list, rather than a sequence of elements; develop a solution space, rather than an individual solution; imagine a graph, rather than a single path. The wholemeal approach often offers new insights or provides new perspectives on a given problem. It is nicely complemented by the idea of projective programming: first solve a more general problem, then extract the interesting bits and pieces by transforming the general program into more specialised ones.”

#### Example

Consider this C style pseudocode:

```java
lst = [2,3,5,7,11]

int total = 0;
for ( int i = 0; i < lst.length; i++) {
  total = total + 3 * lst[i];
}

print total;
```

This code suffers from what Richard Bird refers to as “indexitis”: it has to worry about the low-level details of iterating over an array by keeping track of a current index. It also mixes together what can more usefully be thought of as two separate operations: multiplying every item in a list by 3, and summing the results.

Vs Haskell, which is more readable, concise, and is less likely to have errors:

```haskell
lst = [2,3,5,7,11]

total = sum (map (3*) lst)

main = print total
```

## Using GHCi - Consider splitting into own section

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

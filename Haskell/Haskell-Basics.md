# Haskell Basics

Haskell language basics, such as using variables, creating functions, and common language features. Anything requireing an extensive explanation can be broken into a seperate section.

## Comments

A comment in Haskell: `-- This is a comment, because it is preceded by two hyphens`

A multiline comment:

```haskell
{- this is a multiline comment
    because it is enclosed in a curly brace hypen pair -}
```

## Declarations and Variables

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
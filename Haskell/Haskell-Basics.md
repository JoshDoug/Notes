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

It looks quite simple:

```haskell
x :: Int -- read :: as 'has type'
x = 3
```

But note that because variables in Haskell are immutable, the value of x cannot be changed, setting `x = 4` a few lines later would result in the error `Multiple declarations of 'x'`. In Haskell, variables are not mutable boxes; they are just names for values!

Put another way, = does not denote assignment like it does in many other languages. Instead,  = denotes definition, like it does in mathematics. That is, x = 4 should not be read as “x gets 4” or “assign 4 to x”, but as “x is defined to be 4”.

And watch out:

```haskell
y :: Int
y = y + 1
```

Now clearly this doesn't make a whole lot of sense because Haskell variables are immutable, so you can't assign a variable to itself + 1 as you would in other languages to increment a value. The type signature is also specified above it, indicating that this is the first time the value `y` is assigned, so in most languages this would fail as you cannot add 1 to a null value and assign it. So what is going on? Well because in Haskell = denotes definition rather than assignment, this does not increment the value of `y`. Instead, this statement is taken as a recursive definition; evaluation of `y` yields

```haskell
y = y + 1
  = (y + 1) + 1
  = ((y + 1) + 1) + 1
-- repeat ad infinitum
```

resulting in an infinite loop.

### Basic Types

```haskell
i :: Int
i = -78
```

Ints can accomadate values at least up to ±2^29, and on most 64-bit archs the range is ±2^63, which is a big number, run the following to find the limit on your computer:

```haskell
main = print
-- show
  (minBound :: Int, maxBound :: Int)
-- /show
```

Mine output `(-9223372036854775808,9223372036854775807)`

In addition to the `Int` type, there is the `Integer` type which is only limited by the amount of memory the machine has.

For floating-point numbers there is `Double`:

```haskell
d1, d2 :: Double
d1 = 4.5387
d2 = 6.2831e-4
```

Note that multiple variables can have their type declared on a single line.
There is also a single-precision floating point type, `Float`, but it is not used much. But isn't that always the case?

Some more type examples with Bools, Chars, and Strings (char arrays):

```haskell
-- Booleans
b1, b2 :: Bool
b1 = True
b2 = False

-- Unicode characters
c1, c2, c3 :: Char
c1 = 'x'
c2 = 'Ø'
c3 = 'ダ'

-- Strings are lists of characters with special syntax
s :: String
s = "Hello, Haskell!"
```

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
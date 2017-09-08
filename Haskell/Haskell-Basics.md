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

Some more type examples with Bools, Chars, and Strings (char list):

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

### Arithmetic

Probably makes sense to try these in GHCi:

```haskell
ex01 = 3 + 2
ex02 = 19 - 27
ex03 = 2.35 * 8.6
ex04 = 8.7 / 3.1
ex05 = mod 19 3
ex06 = 19 `mod` 3 -- the `backticks` make a function into an infix operator
ex07 = 7 ^ 222
ex08 = (-3) * (-7) -- negative numbers must often be surrounded by parentheses, to avoid having the negation sign parsed as subtraction
```

Addition is only between values of the same numeric type, and Haskell doesn't do implicit conversion so this will give an error:

```haskell
i = 30 :: Int
n = 10 :: Integer
main = print (i + n)
```

Instead it is necessary to explicitly convert with:

* `fromIntegral`: convert from any integral type (`Int` or `Integer`) to any other numeric type
* `round`, `floor`, `ceiling`: convert floating-point numbers to `Int` or `Integer`

This example will also give an error:

```haskell
i = 30 :: Int
main = print (i / i)
```

This is an error since / performs floating-point division only. For integer division we can use `div`:

```haskell
i = 30 :: Int
main = print (i `div` i, 12 `div` 5)
```

Quite annoying if you're used to a language with implicit conversion of numeric types, an argument against implicit conversion are that is encourages sloppy thinking about numeric code.

## Boolean Logic

As with most languages, Boolean values can be compared with `&&` (logical and), and `||`, although Haskell uses `not` instead of `!`.

```haskell
ex11 = True && False -- Evaluates to False
ex12 = not (False || True) -- Evaluates to False
```

Comparing for equality is also fairly typical with `==`, `<`, `>`, `<=` `>=`, although not equal is different: `/=`.

```haskell
ex13 = ('a' == 'a')
ex14 = (16 /= 3)
ex15 = (5 > 3) && ('p' <= 'q')
ex16 = "Haskell" > "C++"
```

Haskell also has `if` expressions: `if b then t else f` is an expression which evaluates to `t` if the Boolean expression `b` evaluates to `True`, and `f` if `b` evaluates to `False`. Note that Haskell has `if` *expressions* not `if` *statements*, this is important because with an `if` *statement* the `else` part can be optional, whereas with an `if` expression the `else` part is required since the `if` *expression* must result in some value. TL:DR when using `if` in Haskell the `else` is also required.

## Functions

In Haskell functions are called by writing the function name, a space and then the parameters, also separated by spaces, e.g. `min 8 14`, as opposed to typical C-Style syntax which might look like: `min(8,14);`. Function application (calling a function by putting a space after it and then typing out the parameters) has the highest precedence of them all. What that means for us is that these two statements are equivalent:

```haskell
ghci> succ 9 + max 5 4 + 1
16
ghci> (succ 9) + (max 5 4) + 1
16
```

This means that to get the successor of the product of numbers 9 and 10, `succ 9 * 10` wouldn't work because that would get the successor of 9, which would then be multiplied by 10. So 100. Instead write `succ (9 * 10)` to get 91.

### Basic function definitions

A function called add, which takes parameters a and b, and returns a + b: `add a b = a + b` and use the function: `add 12 4` which returns `16`.

Example of a function, called add:

* Function declaration which takes parameters a and b, and returns a + b: `add a b = a + b`
* Calling the function with parameters: `add 12 4` which returns `16`
* Add a type signature before the declaration: `add :: Int -> Int -> Int` - not sure why this is important?

A second example:

A functin that doubles a number: `doubleMe x = x + x`, so the name is `doubleMe`, the first (and in this case only) paramater, `x`, is specified after the name and before the equals, and the logic of the function is specified after the equals (`x + x`).

Types

Partial functions - Return a value or an error?
Total functions? - Return a value and always works?

Currying

Point-free style

### Infix Functions

These are functions in Haskell (and other languages such as Kotlin) that are placed between two arguments, operators such as `+` or `*` are [*infix* operators](https://wiki.haskell.org/Infix_operator) (which are functions). This is different to most functions in Haskell which are typically *prefix* functions, or *prefix* notation where the function comes before the arguments.

If a prefix function takes two parameters then it can also be called as an infix function by surrounding it with backticks. For instance, the `div` function takes two integers and does integral division between them. Doing `div 92 10` results in a 9 (as opposed to 9.2). When calling it using *prefix* syntax there could be some confusion as to which number is doing the division and which one is being divided, so it can be called as an infix function like so: ```92 `div` 10```, which clears it up a little.

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
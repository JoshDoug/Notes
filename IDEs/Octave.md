# [GNU Octave](https://www.gnu.org/software/octave/)

Octave is an Open Source Matlab replacement, that provides a source compatible language compiler and an equivalent - although not identical - IDE/GUI environment.

The prompt can be changed in a way similar to bash, e.g. `PS1 >>` would change the prompt to `>>`, `PS1 '>> '` to add a space after the prompt. This change only lasts for the duration of the session.

## Installing

Ports and Homebrew can be used to install Octave, but Homebrew doesn't currently support the a version with a GUI due to Qt incompatibilities. Ports and Homebrew may not play well either, so don't just try Ports if already using Brew. The alternative is to just install the version provided by GNU, it doesn't look great, but it does work (mostly).

## Help System

Octave has [online documentation here](https://www.gnu.org/software/octave/doc/interpreter/), and a handy [wiki](https://wiki.octave.org/GNU_Octave_Wiki).

To get help on help: `help help`

* Help on pi: `help pi`

The full documentation can be displayed using `doc`, but this is more easily navigated online. The default macOS installation is incomplete and doesn't include doc.

## Built in Commands

* Alter significant figures shown: `format long` and `format short` change the number of signifcant figures displayed by following commands/output, such as `pi`.
* Display the content of a variable: `disp(a)`, short for display, but just the variable on its own on a line will have the same effect.
* Generate a random value: `b = rand()` sets `b` to a random decimal number between 0 and 1. Alternatively `randn()` will generated a random number based on a normal distrobution with a mean of 0 and a standard deviation of 1.

### Useful Built-in Mathematical Functions

* `sqrt(x)`
* `nthroot(x, n)` e.g. `nthroot(27,3)` returns `3` as it's the cube root.
* `fix(x)` truncates a number and returns just the integer part, it doesn't round the number, so `fix(1.9)` will return `1`.
* `ceil(x)` rounds a number up
* `floor(x)` rounds a number down
* `round(x)` rounds a number to the closes integer (.5 goes up)
* `max(x)` finds the largest number in a set
* `min(x)` finds the smallest number in a set
* `factorial(x)` finds the factorial of an input, e.g. 5! is 120.
* `primes(x)` returns primes up to and including `x`
* `list_primes(x)` lists the first `x` primes

## Variables

* Assignment: `a = pi` creates variable `a` and sets it to `pi`.
* Assignment with suppressed output: `b = pi;` assigns `pi` to `b` but doesn't display the result.
* String assignment: `c = 'Hello World'`, single or double quotes work.

### Sets

A set is similar to an array or vector ?

* a = [1, 3, 4, 9]

## Operators

As with most languages there are two types of operators, mathematical operators, and logical operators.

Mathematical operators, few surprises here:

* Addition `+`
* Subtraction `-`
* Multiplication `*`
* Division `/`
* Exponenation `^` or `**`: `6^3` or `6**3`
* Modular division `mod(x,y)` where `x` is the number being divided and `y` is the divisor.

Logical operators, 0 is false, 1 is true:

* Equality `==`
* Not equal `!=`, or `~=`, although the tilde version is outdated.
* AND `&&`
* OR `||`
* XOR `xor(x, y)`, determines whether one of the values is true but not both
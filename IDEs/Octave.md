# [GNU Octave](https://www.gnu.org/software/octave/)

Octave is an Open Source Matlab replacement, that provides a source compatible language compiler and an equivalent - although not identical - IDE/GUI environment.

These notes cover Octave IDE and langauge specific variations to MatLab, for the MatLab language check MatLab notes section.

The prompt can be changed in a way similar to bash, e.g. `PS1 >>` would change the prompt to `>>`, `PS1 '>> '` to add a space after the prompt. This change only lasts for the duration of the session.

## Installing

Ports and Homebrew can be used to install Octave, but Homebrew doesn't currently support the a version with a GUI due to Qt incompatibilities. Ports and Homebrew may not play well either, so don't just try Ports if already using Brew. The alternative is to just install the version provided by GNU, it doesn't look great, but it does work (mostly).

## Help System

Octave has [online documentation here](https://www.gnu.org/software/octave/doc/interpreter/), and a handy [wiki](https://wiki.octave.org/GNU_Octave_Wiki).

To get help on help: `help help`

* Help on pi: `help pi`
* Help on classes and types: `help class`

The full documentation can be displayed using `doc`, but this is more easily navigated online. The default macOS installation is incomplete and doesn't include doc.

## Built in Commands

## Variables

Variable assignments are largely the same as MatLab.

### Strings

String concatenation and manipulation:

* String assignment: `c = 'Hello World'`, single or double quotes work.
* Concatenate strings but keep whitespace: `cstrcat(s1, s2...)`

### Sets

A set is similar to an array or vector ?

* a = [1, 3, 4, 9]

## Operators

As with most languages there are two types of operators, mathematical operators, and logical operators.

Mathematical operators are the same with a couple of changes:

* Exponenation `^` or `**`: `6^3` or `6**3`

Logical operators, 0 is false, 1 is true:

* Not equal `!=`, or `~=`, although the tilde version is outdated.

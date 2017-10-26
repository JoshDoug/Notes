# MatLab - Matrix Labratory

Everything is a matrix, when `a = 1`, a is a 1x1 matrix.

* [MathWorks Tutorials](https://uk.mathworks.com/support)
* [MatLab Academy](https://matlabacademy.mathworks.com/)

## Comments

A comment in MatLab is the percentage symbol: `%`

A mutliline comment: `%{` commented out code `%}`

An inline comment: `...`, the elipsis is weird to use, but can be used to break code over several lines with comments within.

A help comment: this is the first comment, or set of comments, within a script of function (I think?).

## Common Functions and Commands

* Alter significant figures shown: `format long` and `format short` change the number of signifcant figures displayed by following commands/output, such as `pi`.
* Display the content of a variable: `disp(a)`, short for display, but just the variable on its own on a line will have the same effect.
* Generate a random value: `b = rand()` sets `b` to a random decimal number between 0 and 1. Alternatively `randn()` will generated a random number based on a normal distrobution with a mean of 0 and a standard deviation of 1.
* To bring up documentation: `doc`

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

### Timing functions

* `tic` - Starts a built-in millisecond stopwatch
* `toc` - Returns the time elapsed since the last tic

Basic setup is simpyl putting the `tic` before the code block/line to be measured and the `toc` after. These can be easily run from the interpeter as well. The value of `toc` can be stored in a variable which is useful when measuring multiple parts of a program.

## Operators

As with most languages there are two types of operators, mathematical operators, and logical operators.

Mathematical operators, few surprises here:

* Addition `+`
* Subtraction `-`
* Multiplication `*`
* Division `/`
* Exponenation `^`: `6^3`
* Modular division `mod(x,y)` where `x` is the number being divided and `y` is the divisor.

Logical operators, 0 is false, 1 is true:

* Equality `==`
* Not equal `~=`
* AND `&&`
* OR `||`
* XOR `xor(x, y)`, determines whether one of the values is true but not both

## Variables

MatLab is a weakly typed language, variable types do not need to be declared.
By default, MatLab considers any variable to be a double, so 1 would be a double by default.
Datastructures in MatLab are typically Scalar (single value), Vector (an array of values), or Matrix (grid of values), but really everything is a matrice, a scalar value is just a 1x1 matrix, a vector is just a 1xN matrix.

* Assignment: `a = pi` creates variable `a` and sets it to `pi`.
* Assignment with suppressed output: `b = pi;` assigns `pi` to `b` but doesn't display the result.
* String assignment: `c = 'Hello World'`, single or double quotes work.
* Optionally specify the type of a variable on assignment: `d = uint16(1)` would set to 1 with a class/type of an unsigned 16 bit integer, instead of a double.
* A scalar: `x = 1`, with a class of double, and which is really a 1x1 matrix.
* A vector or array: `e = [1 2 3]` or `e = [1,2,3]`, either works. This is still technically a matrix.

### Strings

String manipulation and concatenation.

* Class char: `a = 'Test'` sets `a` to the string `Test`, MatLab requires single quotes to be used, Octave allows double quotes.
* Class string: `b = string('Test')`, this stores `Test` as a String with double quotes. `b = "Test"` would cause an error.
* Concatenate strings: `strcat(s1, s2...)`, concatenates however many strings are included as arguments, literals or variables. This function also removes whitespace at the end of each string.
* Convert numbers to strings: `num2str(x)`, `num2str(x,n)` converts to a string rounded to `n` significant figures.
* Compare strings: `strcmp(s1, s2)`
* Compare strings and ignore case: `strcmpi(s1, s2)`
* Compare the first n characters of two strings: `strncmp(s1, s2, n)`
* Compare first n chars and ignore case: `strncmpi(s1, s2, n)`

Trimming and processing strings:

* Remove trailing whitespace from a string or arrya: `deblank(s)`
* Remove leading and trailing whitespace: `strtrim(s)`

### Matrices

* `a = [1,2;3,4]` or `a = [1 2;3 4]`, commas don't seem to matter. This would set up a 2x2 matrix.

Output:

```matrix
1 2
3 4
```

* Matrix transpose: `a'`, the `'` apostrophe/single quote transposes a matrix, basically flipping it on its side.
* Matrix product transpose: `a' * a`

Transpose example:

```MatLab
b = [1 2 3; 4 5 6; 7 8 9]

b =

   1   2   3
   4   5   6
   7   8   9

b' % Transpose b

ans =

   1   4   7
   2   5   8
   3   6   9
```

Matrix of matrices: create four matrices, e.g. `a = [1,2;3,4]` x4, these can then be made into a 'super matrix' using a slightly different syntax: `e = {a,b;c,d}`, which is also accessed with that syntax, so to get `a` use `e{1,1}`

Matrix generation functions:

* `zeros`
* `ones`
* `rand`
* `randn`

These matrix generation functins can be useful when it comes to performance. Creating a 100x100 matrix and then filling each cell is more efficient than creating a 1x1 matrix and then adding additional columns and rows.

#### Matrix and Scalar Operations

Piece wise Matrix operations involve using a `.` after the first matrix, e.g. `a.*b`, each cell only interacts with its corresponding cell, in this case multiplying them together. Unlike `a*b` which would multiple by rows and columns (get the dot product of each cell?).

#### 3D Matrix

* Defining an all zero 3D matrix `zeros(2,2,2)`, this creates a 2x2x2 matrix of zeros. MatLab display it in slices.
* `ones()` creates a matrix filled with ones, `rand()` creates a matrix with number between 0 and 1, `randn()` creates a matrix of normally distributed random numbers.

Parts of the matrix can be specified and set to other values easily, so a 2x2x2 matrix `a`, set to all zeroes like so `a = zeros(2,2,2)` can be changed to have the 2nd slice (or 2nd z index) to a different matrix like so: `a(:,:,2) = [1,2;3,4]`. MatLab arrays start at 1, not 0.

### Structures

Structures are a storage mechanism allowing multiple peices of data to be associated, similar to an array of objects.
A structure is built up via a name.attribute, so for example a structure of people could be started with the name: `person.name = 'John Doe`, then the address could be set with `person.address = "Fake Address 1"`, this on its own is similar in concept to an object, but it can be extended to multiple of these objects very easily. To add a second person: `person(2).name = "Joe Bloggs` and `person(2).address = "Fake Address 2"`. As this is MatLab this structure is still considered a matrix.

## Control Flow

Simple if-else statement:

```MATLAB
if a != b
    print('A doesn't equal b.')
else
    print('A equals b.')
end
```

Switch statement:

```MATLAB
switch a(3,3)
    case 3
        a = a';
    otherwise
        a = inv(a);
end
```

Switches can also have a `break` and `continue`. Using `break` jumps out of the loop/conditional and resumes at the corresponding `end` statement, `continue` jumps back to the beginning of a loop and increments that counter as if the loop had completed normally.

## Functions

Boilerplate function:

```MATLAB
function [ output_args ] = UntitledFunction( input_args )
% UntitledFunction Summary of the function goes here
%   Detailed explanation goes here

% Function code

end
```

## Graphing and Drawing

* `gcf` returns a handle to the current figure, or creates one if no figures are active.
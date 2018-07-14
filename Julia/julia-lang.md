# Julia Language

* [Julia Documentation](https://docs.julialang.org/en/stable/)
* [JuliaBox Tutorial Notebooks](https://github.com/JuliaComputing/JuliaBoxTutorials)
* [Cheatsheet](http://math.mit.edu/~stevenj/Julia-cheatsheet.pdf)
* [JuliaDocs Getting Started](https://docs.julialang.org/en/stable/manual/getting-started/#Getting-Started-1)
* [Julia Editor Support](https://github.com/JuliaEditorSupport)

## Juno

Juno is the defacto IDE for Julia, and is a plugin for Atom. Julia can also be used via the REPL on the command line or with a text editor.

## Julia and Jupyter with IJulia

IJulia can be used by installing the `IJulia` package with `Pkg.add("IJulia")`, then simply run `notebook()` from the REPL.

* [Using Git and Jupyter notebooks together](http://timstaley.co.uk/posts/making-git-and-jupyter-notebooks-play-nice/)
* [Getting Started with Jupyter and Julia](https://lectures.quantecon.org/jl/getting_started.html)

IJulia sets up a Jupyter notebook which is accessed via a browser (normally) and can include embedded, inline code samples that are runnable.

* Start IJulia notebook: `using IJulia; notebook()`
* Start detached IJulia notebook: `using IJulia; notebook(detached=true)`
* Shift + Enter - runs an inline code sample.

Slightly more complex but most likely better way to install IJulia, this seems to ensure the Julia version stays up to date:

* Install Jupyter (without using Anaconda) with pip: `pip install jupyter` (might need to use `pip3`)
* In the Julia REPL use: `ENV["JUPYTER"]="jupyter"`
* Install the IJulia package: `Pkg.add("IJulia")`, if it's already installed then it can be either removed or switched from using the environment variable

## REPL

* [Julia REPL Documentation](https://docs.julialang.org/en/latest/stdlib/REPL/)
* `exit()` or `^D` to exit
* `^L` to clear console

## Packages

Julia has about 1800 native registered packages and growing. Julia also has first class function calls to other languages, providing excellent foreign function interfaces, so it's easy to call into Python or R, using `PyCall` or `Rcall` for example.

* Package listings at [pkg.julialang.org](https://pkg.julialang.org/) and [juliaobserver.com](https://juliaobserver.com/)

The first use of a package on a given Julia installation requires it to be explicitly added: `Pkg.add("Example")`. The package can then be loaded for a notebook, REPL, program, etc (each session) using the `using` keyword: `using Example`.

* `Pkg.add("Colors")`
* `using Colors`
* `palette = distinguishable_colors(100)` - use package
* `rand(palette, 3, 3)`

Simple!

## Language Basics

* `;` use a semicolon to suppress output for a statement, postfixed, much likes MatLab does.
* `?` prefix a question mark to get docs for a function
* `;` to use a shell command, _prefix_ it with a semicolon
* `#` single line comment
* `#=` starts a multiline comments, `=#` ends a multiline comment

### Strings

Julia String documentation [here](https://docs.julialang.org/en/stable/manual/strings/).

* `s1 = "I am a string"`
* `s2 = """I am also a \n\n\nstring."` - this can be a multiline string with formating etc, it can also include quotation marks
* `char = 'a'` - single quotes create chars, not strings (single quoting multiple characters will cause an error)

String interpolation can be done using the `$` sign to insert existing variables into a string and to evaluate expressions within a string.

```Julia
name = "Josh"
num_fingers = 10
num_toes = 10

println("My name is $name.")
println("I have $num_fingers fingers and $num_toes toes.")
println("That is $(num_fingers + num_toes) digits in all!")
```

String concatentation:

```Julia
s3 = "How many cats ";
s4 = "is too many cats?";
😺 = 10

string(s3, s4)
string("I don't know, but ", 😺, " is too few.")
```

This can also be done with string interpolation.

* `s3*s4` - looks like multiplying but it concatenates them
* `$s3$s4` - and string interpolation
* `"hi "^100` - concatenate the string `"hi "` 100 times.

### Loops

While looops:

```Julia
while condition
    # Do something
end
```

Examples:

```Julia
# Example 1
n = 0
while n < 10
    n += 1
    println(n)
end

# Example 2
myfriends = ["Ted", "Robyn", "Barney", "Lily", "Marshall"]

i = 1
while i <= length(myfriends)
    friend = myfriends[i]
    println("Hi $friend, it's great to see you!")
    i += 1
end
```

For loops:

```Julia
for var in loop_iterable
    # Do Something
end
```

Examples:

```Julia
# Example 1
for n in 1:10
    println(n)
end

# Example 2
myfriends = ["Ted", "Robyn", "Barney", "Lily", "Marshall"]

for friend in myfriends
    println("Hi $friend, it's great to see you!")
end
```

Addition table example, where every entry is the sum of its row and column indices:

```Julia
m, n = 5, 5 # Can initialise multiple variables on a single line
A = fill(0, (m, n)) # Creates a 5x5 two dimensional array

# Set the addition table values
for i in 1:m
    for j in 1:n
        A[i, j] = i + j
    end
end

A # Output the table

# For loop syntactic sugar
B = fill(0, (m, n))

for i in 1:m, j in 1:n
    B[i, j] = i + j
end
B
```

Alternatively, the more "Julia" way to create this addition table would be with _array comprehension_.

```Julia
# 1D array comprehension
oned = [x for x in 1:10]

# Addition table example
twod = [i + j for i in 1:m, j in 1:n]

# 3D Array example
threed = [(i + j)^k for i in 1:5, j in 1:5, k in 2:2:6]
```

### Conditionals

Julia has the trusty old if statement and some shorthands, but no switch statements!

```Julia
if condition
    # Do something
elseif condition
    # Do something
else
    # Do something
end
```

Example using FizzBuzz:

```Julia
N = 42
if (N % 3 == 0) & (N % 5 == 0)
    println("FizzBuzz")
elseif N % 3 == 0
    println("Fizz")
elseif N % 5 == 0
    println("Buzz")
else
    println(N)
end
```

Ternary operators:

```Julia
x = 5
y = 8

# Long version
if x > y
    x
else
    y
end

# Short version using ternary operator
(x > y) ? x : y
```

Short circuit evalutation:

Boolean expressions can be compared like so: `a & b` for two expressions or values a and b. Julia will evaluate this expression eagerly, so: `false & (println("hi"); true)` prints "hi" to stdout before returning false.

On the other hand, when we replace `&` with `&&`, as in `a && b` we get short-circuit evaluation. `b` is only evaluated if `a` is true, which can help us out if evaluating `b` is expensive. For example:

* `false && (println("hi"); true)` returns false without printing "hi".

This means we can use `a && b` to conditionally evaluate `b` if `a` is true!

### Functions

Julia function can be declared in a few ways, the most typical is similar to most languages, declaring with a keyword, function name, parameters, function logic, and then a function end. Julia doesn't require the usage of return statements, but does support them, otherwise Julia just returns whatever is on the last line of the function.

```Julia
function sayhi(name)
    println("Hi $name, it's great to see you!")
end

function f(x)
    x^2
end

# Calling the functions
sayhi("C-3PO")
f(42)

# Shorter versions of these functions:

sayhi2(name) = println("Hi $name, it's great to see you!")
f2(x) = x^2

# Anonymous function examples bound to a variable
sayhi3 = name -> println("Hi $name, it's great to see you!")
f3 = x -> x^2
```

The long, short, and anonymous functions are all called with the same syntax.

TODO: Look up Julia's anonymous functions

#### Duck-typing

Julia functions will just work on whatever inputs make sense - *"if it quacks like a duck, it's a duck"*, so the `sayhi` function example above will work with integers as well as strings, and `f` will work on a matrix. This will not work on inputs that don't make sense, when no behaviour is defined for it.

#### Mutating vs. non-mutating functions

By convention, functions followed by `!` alter/mutate their contents, and functions lacking `!` do not, e.g. `sort` and `sort!`.

```Julia
a = [3, 5, 2]
b = sort(a)
a # Output a, a is unchanged
b # Output b, b is the sorted version of a

sort!(a)
a # a is now sorted
```

#### Some higher order functions

Higher order functions take other functions as their inputs, this makes them a great place to use anonymous functions!

Looking at map, this is a higher order functions which applies the input function to every element of the data structure passed to it, examples:

* `map(f, [1, 2, 3])` the function `f` (shown above) squares its input, so each value of the array/vector is passed to `f` and squared.
* `map(x -> x^3, [1, 2, 3])` here the anon function is used, and cubes each value of the array/vector
* `broadcast(f, [1, 2, 3])`, `broadcast` is a generalisation of `map`, so it can do everything `map` does and more.
* `f.([1, 2, 3])`, here's some syntactic sugar to use `broadcast` via a shorthand `.`, this is different from `f([1, 2, 3])` which would try and square the entire vector
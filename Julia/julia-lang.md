# Julia Language

* [JuliaBox Tutorial Notebooks](https://github.com/JuliaComputing/JuliaBoxTutorials)

## Juno

Juno is the defacto IDE for Julia, and is a plugin for Atom. Julia can also be used via the REPL on the command line or with a text editor.

## Julia and Jupyter with IJulia

IJulia can be used by installing the `IJulia` package with `Pkg.add("IJulia")`, then simply run `notebook()` from the REPL.

* [Using Git and Jupyter notebooks together](http://timstaley.co.uk/posts/making-git-and-jupyter-notebooks-play-nice/)

IJulia sets up a Jupyter notebook which is accessed via a browser (normally) and can include embedded, inline code samples that are runnable.

* Start IJulia notebook: `using IJulia; notebook()`
* Start detached IJulia notebook: `using IJulia; notebook(detached=true)`
* Shift + Enter - runs an inline code sample.

## REPL

* `exit()` or `^D` to exit
* `^L` to clear console

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

## Loops

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

## Conditionals

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
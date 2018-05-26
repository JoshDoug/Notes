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
# Pkg - Julia's Package Manager

* [Getting started with Julia 1.0's package manager](https://julialang.org/blog/2018/09/Pkgtutorial)
* [Pkg Docs](https://docs.julialang.org/en/latest/stdlib/Pkg/)
* [Creating a Project](https://docs.julialang.org/en/latest/stdlib/Pkg/#Creating-your-own-projects-1)

Julia has about 1800 native registered packages and growing. Julia also has first class function calls to other languages, providing excellent foreign function interfaces, so it's easy to call into Python or R, using `PyCall` or `Rcall` for example.

* Package listings at [pkg.julialang.org](https://pkg.julialang.org/) and [juliaobserver.com](https://juliaobserver.com/)

## Using the Pkg CLI

Pkg now has it's own REPL CLI accessed by pressing `]` which allows easy interfacing with pkg, to exit just hit delete/backspace. Other pkg commands:

* `status` - lists installed packages and the root toml.
* `add LinearAlgebra` - install a package
* `update LinearAlgebra` or `up LinearAlgebra` - update a package
* `rm LinearAlgebra` - remove a package

## Using Pkg from the normal Julia REPL

As of Julia 1.0 `Pkg` has to be loaded with `using Pkg` before it can be used.

The first use of a package on a given Julia installation requires it to be explicitly added: `Pkg.add("Example")`. The package can then be loaded for a notebook, REPL, program, etc (each session) using the `using` keyword: `using Example`.

* `Pkg.add("Colors")`
* `using Colors`
* `palette = distinguishable_colors(100)` - use package
* `rand(palette, 3, 3)`

Simple!
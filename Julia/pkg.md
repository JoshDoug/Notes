# Pkg - Julia's Package Manager

Julia has about 1800 native registered packages and growing. Julia also has first class function calls to other languages, providing excellent foreign function interfaces, so it's easy to call into Python or R, using `PyCall` or `Rcall` for example.

* Package listings at [pkg.julialang.org](https://pkg.julialang.org/) and [juliaobserver.com](https://juliaobserver.com/)

The first use of a package on a given Julia installation requires it to be explicitly added: `Pkg.add("Example")`. The package can then be loaded for a notebook, REPL, program, etc (each session) using the `using` keyword: `using Example`.

* `Pkg.add("Colors")`
* `using Colors`
* `palette = distinguishable_colors(100)` - use package
* `rand(palette, 3, 3)`

Simple!
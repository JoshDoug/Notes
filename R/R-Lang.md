# R Language Basics

A general collection of R information, sections - such as IO - can be split into specific files when they get extensive enough.

## General

`#` - a comment in R.

`1:100` - simple loop that prints out 1 to 100.

`print("Hello World)` # Print Statement, no semicolons necessary in R.

`x` - running this will just print the variable to the console.

`ls()` - function that lists the current objects, when using RStudio these are already listed in the workspace tab.

### Variables

`x <- 1:5` # Assigning the values 1 to 5 to variable x, sometimes described as 'x *gets* values 1 to 5'

`y <- c(6,7,8,9,10)` # The concatenate/collection/combine function, useful for specifying non-sequential data to put in the variable

`x + y` # Add the contents of each vector/array, such that the output would be: 7,9,11,13,15 (but no assignment)

`x * 2` # Multiplies each element in the vector, such that the output would be: 2,4,6,8,10 (but no assignment)

### Reading data in from a spreadsheet

`data.csv <- read.csv("/path/to/data.csv")` # Read in a csv, provide the path to it.

* Path can use forward slashes on Windows which don't need to be escaped, can also handle relative paths.
* For header/column names add parameter: `header = TRUE` or `header = T`.

### Turning data into bar charts

Creating bar charts for categorical variables.

### Packages

CRAN - the Comprehensive R Archive Network is a package repository for R.

`browseURL("http://cran.r-project.org/web/views/")` - link to CRAN package list, can be run from within R to open a tab in default browser, [embedded link]("http://cran.r-project.org/web/views/").
`browseURL("http://cran.stat.ucla.edu./web/packages/available_packages_by_name.html")` - same as above, but for UCLA's package list, [embedded link]("http://cran.stat.ucla.edu./web/packages/available_packages_by_name.html").

* `library()` - list currently installed & available packages
* `search()` - list currently active installed packages
* `install.packages("packageName")` - download and install a package (but doesn't activate/load it), e.g. `install.packages("psych")`
* `library("packageName")` - load the library for scripts that use it later on
* `require("packageName")` - loads the library, but probably complains like php's require/include mechanism if the resource cannot be found
* `library(help = "packageName")` - loads up a man page for the package in the editor window (or maybe in Less from CLI?)
* `vignette(packge = "packageName")` - brings up a list of vignettes (examples) in the editor window
* `browseVignettes(package = "packageName")` - opens the examples page in the browser, with PDFs, etc
* `vignette()` - bring up a list of all vignettes for currently installed packages
* `browseVignettes()` - bring up list of all vignettes in the browser
* `update.packages()` - checks for updates and gives option to install updates in console
* `detach("package:packageName", unload=TRUE)` - deactivate a package
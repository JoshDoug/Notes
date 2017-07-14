# R Language Basics

A general collection of R information, sections - such as IO - can be split into specific files when they get extensive enough.

## General

`#` - a comment in R.

`print("Hello World)` # Print Statement, no semicolons necessary in R.

`x` - running this will just print the variable to the console.

`ls()` - function that lists the current objects, when using RStudio these are already listed in the workspace tab.

`? barplot` - find help on any R function, shows in editor help tab

`T` and `F` are shorthands for `TRUE` & `FALSE`

### Variables

`x <- 1:5` # Assigning the values 1 to 5 to variable x, sometimes described as 'x *gets* values 1 to 5'

`x + y` # Add the contents of each vector/array, such that the output would be: 7,9,11,13,15 (but no assignment)

`x * 2` # Multiplies each element in the vector, such that the output would be: 2,4,6,8,10 (but no assignment)

#### Vectors

`c(4, 7, 9)` - an array of a values of a single type, c is short for combine, but is also commonly reffered to as concatenate and collection

`y <- c(6,7,8,9,10)` # The ccombine function is useful for specifying non-sequential data to put in the variable

`hi <- c("Hello", " ", "world", "!")` - another example

`1:10` - this is a sequence vector which uses a `start:end` notation to create a sequence of - in this case - numbers

`x <- 1:100` - creates a vector of 1 to 100 and assigns to x

`9:5` - can also be reversed

`seq(5, 9)` - can also be used to create sequences, but also allows increments to be specified

`seq(5, 9, 0.5)` - this time with an increment of 0.5 specified, if it is not set then it defaults to an increment of 1 I guess.

`hi[3]` - retrieve a value from a vector, in R array indices start at 1 instead of 0. In this case it would return "world", from the vector above.

`hi[3] <- "England"` - change the value in the 3rd indice, from world to England.

`hi[4] <- "nice"` - extend the vector with new values, the vector will grow to accomadate them

`hi[c(1,3)]` - retrieve multiple values from the vector by specifying the indices to retrieve within another vector

`hi[1:3]` - you can also retrieve a range of values

`hi[5:7] <- c('some', 'more', 'words')` - you can also set ranges of values by providing them in a vector

Vector Names, crikey - like a HashMap...kind of?

`ranks <- 1:3` - create a vector of numbers 1 to 3

`names(ranks) <- c("first", "second", "third")` - assign names to a vector's elements by passing a second vector filled with names to the `names` assignment function

`ranks` - this will now print out the names and associated values of each indice

`ranks["first"]` - this will retrieve the value associated with the name

`ranks["third"] <- 4` - the name can then be used to refer to a value of the vector when reassigning values

Plotting One Vector

* `vesselsSunk <- c(4, 5, 1)` - create simple vector
* `barplot(vesselsSunk)` - create a barplot from it, which will be 3 columns of heights 4, 5, and 1.

Use the `names` assignment function to label each bar.

* `names(vesselsSunk) <- c("England", "France", "Norway")` - nothing new here
* `barplot(vesselsSunk)` - now the barplot will be nicely labelled

Barplots also accept ranges, and other vectors

`barplot(1:100)` - displays a barplot of 100 columns at heights 1 to 100

Vector Math

`a <- c(1, 2, 3)` - create a vector
`a + 1` - add one to it, this will add 1 to each value, so this will return: `2, 3, 4` (not the vector has not changed, as the result has not been reassigned to it, the values are just returned)
`a / 2` - it can also be multiplied or divided, this will return: `0.5, 1, 1.5`
`a * 2` - returns `2, 4, 6`

`b <- c(4, 5, 6)` - create a second vector
`a + b` - returns `5, 7, 9`
`a - b` - returns `-3, -3, -3`

`a == c(1, 99, 3)` - compare two vectors, which returns TRUE or FALSE for each indice that is equal to the corresponding indice (R doesn't test whether the whole vectors are equal to each other)
`a < c(1, 99, 3)` - checks if each value in a is less than in the compared vector

NA Values

If data is missing certain values these values are set as NA, and many functions treat this value specially. Most functions will reject vectors or other data contianing NA, e.g. sum and will just return NA, but functions can be told to handle NA values if they occur.

`a <- c(1, 3, NA, 7, 9)` - create a vector with a missing value, NA.
`sum(a)` - running this will just return the value NA.
`sum(a, na.rm = T)` - this will tell sum to remove/ignore NA values and sum will return the value of 20 in this case. `na.rm` is false by default, and presumably means 'remove NA valyes'.

#### Matrices

Matrices, for working with data that isn't just a simple list of values. Matrices are useful when data is in rows and columns, and the data structure is essentially a 2-dimensional array.
The matrix function takes values in the form of data, row number, column number. So `matrix(0, 3, 4)` would produce a matrix 4 columns by 3 rows with all fields set to 0.
You can also use a vector to initialise a matrix's value, the length of the vecotr has to align with the number of fields, so a 4 by 3 matrix would need a 12-item vector to set its values. Or, more specifically, the vector needs to be a sub-multiple or multiple of the number of rows, according to the warning message.

`a <- 1:12` - create a vector containing 1 to 12
`matrix(a, 3, 4)` - create a 3 row, 4 column matrix

`b <- 1:8` - create a vector contianing 1 to 8
`dim(b) <- c(2, 4)` - b is then converted in place from a vector to a 2x4 matrix

To get a value back from a matrix you have to provide two indices instead of one, e.g. `b[2, 3]` would fetch the value in the indice of the 3rd column on the 2nd row, which is 6 in this case.
New values are also assigned in the same way:

`b[1, 4] <- 0` - assign 0 to the indice at 4th column of the 1st row.

Access an entire row or column of a matrix:

`b[2,]` - retrieves the 2nd row
`b[,4]` - retrieves the 4th column

### Popular Functions

#### Maths

`sum(1, 4, 8)` - takes however many numbers and returns the sum

`rep("Repeat", times = 4)` - repeats the first argument by the number of times specified, in this case "Repeat" is repeated 4 times.

`sqrt(16)` - take the square root of the argument

`a <- c(1, 2, 3)` - create a vector
`sin(a)` - get the sine of each value in the vector
`sqrt(a)` - get the square root of each value in the vector

#### Files & IO

`list.files()` - list files in the current directory, or the directory specified in the parameters. The function can also take additional parameters such as masks, recursive listing, etc

`source("code.R")` - source an R script

#### Misc

`help(functionName)` - brings up help for the specified function, e.g. `help(sum)`

`example(functionName)` - brings up examples for the specified function

`print(variable)` - not sure how this is different from just running a variable on its own, but yeah, this'll print it

### IO - Reading data in from a spreadsheet

`data.csv <- read.csv("/path/to/data.csv")` # Read in a csv, provide the path to it.

* Path can use forward slashes on Windows which don't need to be escaped, can also handle relative paths.
* For header/column names add parameter: `header = TRUE` or `header = T`.

## Charts and Statistics for One Variable

### Scatter Plots

The plot function takes two vectors, one for X values and one for Y values, and draws a graph of them.

`x <- seq(1, 20, 0.1)` - create a vector from 1 to 20 in 0.1 increments
`y <- sin(x)` - create a vector of x values run through the sine function
`plot(x, y)` - plot the scatter graph!

### Turning data into bar charts

Creating bar charts for categorical variables. A categorical variable is a variable that can take on one of a limited, and usually fixed, number of possible values, assigning each individual or other unit of observation to a particular group or nominal category on the basis of some qualitative property.

Feed the csv into a data frame, as you would when reading in a csv spreadsheet normally, with headers preferably: `data.csv <- read.csv("data.csv", header = T)`

Create a table from the data for a specific column: `data.freq <- table(data.csv$ColumnName` # The column name is case sensitive.

Create the barchart: `barplot(data.freq)` # This is a very simple bar chart, with no additional options set.

Additional options:

* `barplot(data.freq[order(data.freq, decreasing = T)])` to creat the barchart in decreasing order
* `barplot(data.freq[order(data.freq)], horiz = T)` make the barchart ordered (defaults to increasing) and horizontal

Create a vector of colour specifications: `colomnColours <- c(rep("gray", 5), rgb(59, 89, 152, maxColorValue = 255))` # Rep repeats gray five times, setting that colour for five colours, and then the final colour is blue.

* `barplot(data.freq[order(data.freq)], horiz = T, col = columnColours)` # Extend prior barplot to use specific colours using vector created above.

Other paramters:

* `border = NA` - turn of borders
* `xlim = c(0,100)` - set x limits to 0 and 100, needs to be a vector
* `main = "Title of Graph\nA second line of Title"` - set a title, this can include newline chars to make it multiline
* `xlab = "Description of X"` - title of X axis, presumably `ylab` is the y axis equivalent.

### Creating Histograms

Creating histograms for quantitative variables. Variables that have are measured on a numeric or quantitative scale. Ordinal, interval and ratio scales are quantitative. A country's population, a person's shoe size, or a car's speed are all quantitative variables. Variables that are not quantitative are known as qualitative variables (aka catergorical variables).

`hist(data.csv$ColumnName)` - create a simple histogram, other parameters are similar to barplots.

### Calculating Frequencies

`prop.table(data.freq` - converts the data into proportions, this often produces results with lots of decimal places, this can be simplified with round!
`round(prop.table(site.freq), 2)` - this will round the result to 2 decimal places, how can you rounad to significant figures?

### Calculating Descriptives

`summary(data.csv)` - gets a summary of the data, qualitative and quantitative.
`summary(data.csv$ColumnName)` - gets a summary of the data in the specified column

Tukey's five-number summary: minimum, lower-hinge (first quartile), median, upper-hinge (third quartile), maximum, doesn't print labels though: `fivenum(data.csv$ColumnName)` - doesn't seem that useful though for general use, but is apparently what's used to draw the box plots.

## Modifying Data

### Recoding Variables

Recoding variables with the psych package. Gonna need to rewatch this explainer.

### Computing New Variables

Gonna need to rewatch this.

## Charts ofr Associations

### Creating simple bar charts of group means

### R Colours

R colours: [R Colour Palette](http://research.stowers.org/mcm/efg/R/Color/Chart/)

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
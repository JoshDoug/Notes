# Go

The Go programming language, created at Google.

## Commands and Programs

* `go install`
* `go run`
* `go get`

## Imports

Either single line: `import "fmt"`, or multiline:

```Go
import (
    "fmt"
    "strings"
)
```

## Variables

Go is statically typed, all variables have assigned types. You can set types explicitly or implicitly.

```Go
// Explicit Typing
var anInterger int = 42
var aString string = "This is Go!"

// Implicit Typing - type is still static
anInteger := 43
aString := "Hello World"

// Constants
const anInteger int = 44
const anInteger = 45 // No need for : with a const
```

Types:

* `bool`
* `string`
* `int8`, ints can be signed or unassigned and have a number in bits, e.g. `uint64` (16 and 32 are alternate numbers)
* `byte`, `uint`, `int`, `uintptr` are aliases for the different ints, although these depend on the OS, on macOS the `uint` and `int` are 64 bit.
* `float32`, `float64`
* `complex64`, `complex128` for complex numbers?
* Data collections:
  * `Arrays`
  * `Slices`
  * `Maps`
  * `Structs`
* Language organisation:
  * `Functions` are types
  * `Interfaces`
  * `Channels`
* Data management: `Pointers` yep Go supports pointers, reference variables

Functions can return variables (kind of like MatLab) and by providing returns it will infer the variables, example:

```Go
stringLength, err := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

If you don't want all the return types, use an underscore:

```Go
stringLength, _ := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

Avoiding assigning a variable is useful because you need to use any assigned variables.

## Output

### Printing

* `fmt.Println(str1, str2, str3)` will automatically concatenate, include spaces between strings, and return a newline
* `fmt.Printf("Number: %v\n", aNumber)` will insert the number into the string, can use other data types as well
* `fmt.Printf("Boolean: %v\n", aBoolean)` will insert the result of the boolean into the string
* `fmt.Printf("Float: %.2f\n", aFloat)` will insert the float into the string and round to 2 decimal places
* `fmt.Printf("Variable types: %T, %T, %T, %T\n", str1, aNumber, aBoolean, aFloat)` get the type of the variable
* `fmt.Sprintf("Variable types: %T, %T, %T, %T\n", str1, aNumber, aBoolean, aFloat)` return as a string and print it

## Input

### Console Input

Basic but not optimal:

```Go
var s string
fmt.Scanln(&s) // Passes the string in by reference
fmt.Println(s) // Prints the input, but only up until the first space because of reasons
```

Much better to use `bufio` and `os`:

```Go
reader := bufio.NewReader(os.Stdin)

fmt.Print("Enter text: ")
str, _ := reader.ReadString('\n') // Using single string makes it a byte value?
fmt.Println(str)
```
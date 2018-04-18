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

Multiple assignments are supported: `i1, i2, i3 := 12, 45, 68` - probably all have to be the same type?

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
* Math: `math/big` package includes types for working with decimal numbers

Functions can return variables (kind of like MatLab) and by providing returns it will infer the variables, example:

```Go
stringLength, err := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

If you don't want all the return types, use an underscore:

```Go
stringLength, _ := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

Avoiding assigning a variable is useful because you need to use any assigned variables.

### Pointers

Referencing values with pointers:

* Create a pointer: `var p *int` - creates a pointer for an int, but it doesn't point to anything yet
* Pointers can be changed at runtime to point at other values

Make the pointer use safe:

```Go
var p *int

if p != nil {
    fmt.Println("Value of p:", *p)
} else {
    fmt.Println("p is nil")
}

var v int = 42 // Could var v := 42 be used here as well?
p = &v // connect the pointer to the variable

if p != nil {
    fmt.Println("Value of p:", *p)
} else {
    fmt.Println("p is nil")
}

// Can set pointers implicitly:
var floatVal float64 = 42.13
floatPtr := &floatVal
fmt.Println("Value 1:", *floatPtr)

*floatPtr = *floatPtr / 31
fmt.Println("Value 1:", *floatPtr) // Print pointer
fmt.Println("Value 1:", floatVal) // Print underlying value, both are changed
```

### Strings

* `strings.ToUpper(str)`
* `strings.ToLower(str)`
* `str1 == str2` - case sensitive string comparison
* `strings.EqualFold(str1, str2)` - case insensitive comparison

### Arrays and Slices

Recommended to use slices instead of arrays to represent ordered collections of values.

Array:

```Go
var colours[3] string // [3] doesn't can have spaces either side
colours[0] = "Red"
colours[1] = "Green"
colours[2] = "Blue"
fmt.Println(colours)

// Array literal
var numbers = [5] int {5,3,1,2,4}
fmt.Println(numbers)
fmt.Println("Number of colours:", len(colours))
fmt.Println("Number of numbers:", len(numbers))
```

Slices:

```Go
// Empty [] indicates a slice, with a number it would be an array
var colors = [] string {"Red", "Green", "Blue"}
fmt.Println(colors)

colors = append(colors, "Purple") // Will return a new slice reference so set the original slice to it
```

Slices are resizable, have a built in append function, and more.

### Maps

As with Slices and Arrays(?) memory needs to be allocated with `make()`, example using maps:

```Go
states := make(map[string]string) // Make a map to store strings with a key of type string

states["WA"] = "Washington"
states["OR"] = "Oregon"
states["CA"] = "California"
fmt.Println(states)

california := states["CA"]
fmt.Println(california)

delete(states, "OR")
fmt.Println(states)

states["NY"] = "New York"

// Loop through, k for key, v for value
for k, v := range states {
    fmt.Println("%v: %v\n", k, v) // No guarentted order
}

keys := make([]string, len(states))
i := 0
for k := range states {
    keys[i] = k
    i++
}
sort.Strings(keys) // Requires the "sort" package

fmt.Println("\nSorted")

// Now print in alphabetical order
for i := range keys {
    fmt.Println(states[keys[i]])
}

```

## Structs

Structs are groupings of related values and optionally methods. There's no inheritance supported.

```Go
// Struct to group pointers of a docker client and associated host URL
type Handler struct {
  dc      *client.Client
  hostUrl *url.URL
}
```

Functions as methods of custom types:

```Go
// Can also make the struct and method names lowercase
type Dog struct {
    Breed string
    Weight int
    Sound string
}

// Pass a pointer otherwise a copy is made
func (d *Dog) Speak() {
    fmt.Println(d.Sound)
}

func main() {
    poodle := Dog{
        "Poodle",
        37,
        "Woof",
    }

    fmt.Println(poodle)
    poodle.Speak()
}
```

## Math Operators

Numeric types don't implicitly convert, so you can't add an int to a float.

Using `math/big`:

```Go
var b1, b2, b3, bigSum big.Float
b1.SetFloat64(23.5)
b2.SetFloat64(65.1)
b3.SetFloat64(76.3)

bigSum.Add(&b1, &b2).Add(&bigSum, &b3) // Use pointers, you can chain the Add method!
fmt.Printf("BigSum = %.10g\n", &bigSum) // Needs to be passed as a pointer, not directly
```

* `math` package includes useful functions and constants such as `math.Pi`

## Dates and Times

Working with dates and times using the `time` package:

```Go
// Params: year, date constant, day, hour, minute, second, nano second, timezone
t := time.Date(2009, time.November, 10, 23, 0, 0, 0, time.UTC)
fmt.Printf("Go released at %s\n", t)

now := time.Now()
fmt.Printf("The time now is %s\n", now)

// You can use methods from the time object that's returned
fmt.Printf("The month is", t.Month())
fmt.Printf("The day is", t.Day()) // Numeric
fmt.Printf("The weekday is", t.Weekday()) // Day name

tomorrow := t.AddDate(0, 0, 1)
fmt.Printf("Tomorrow is %v, %v %v, %v\n", tomorrow.Weekday(), tomorrow.Month(), tomorrow.Day(), tomorrow.Year())

// Much neater date time formats using constants or using a format string:
longFormat := "Monday, January 2, 2006" // Sets the date format, not the content
fmt.Println("Tomorrow is", tomorrow.Format(longFormat))
shortFormat := "1/2/06"
fmt.Println("Tomorrow is", tomorrow.Format(shortFormat))
```

## Output

### Printing

* `fmt.Println(str1, str2, str3)` will automatically concatenate, include spaces between strings, and return a newline
* `fmt.Printf("Number: %v\n", aNumber)` will insert the number into the string, can use other data types as well
* `fmt.Printf("Boolean: %v\n", aBoolean)` will insert the result of the boolean into the string
* `fmt.Printf("Float: %.2f\n", aFloat)` will insert the float into the string and round to 2 decimal places
* `fmt.Printf("Variable types: %T, %T, %T, %T\n", str1, aNumber, aBoolean, aFloat)` get the type of the variable
  * To print the full contents of a struct (including field names) use `"%+v"`
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
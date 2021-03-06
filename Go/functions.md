# Go Functions

Go functions don't support overloading, so Go has no polymorphism. If the function starts with a lowercase letter then it's private to the current package. Starting with a capital letter makes it publically accessible outside the package.

Simple function declaration:

```Go
func doSomething() {
    fmt.Println("Does something")
}
```

Function with arguments:

```Go
// Two parameters in parentheses, return value after
func addValues(val1 int, val2 int) int {
    return val1 + val2
}

// Because we have the same type for our arguments we can simplify it a little and only declare the type once:

func addValues(val1, val2 int) int {
    return val1 + val2
}
```

Functions that accept arbritary numbers of values (must be of the same type), similar to Java:

```Go
func addAllValues(values ...int) int {
    sum := 0
    fmt.Printf("%T\n" values) // Print the type of the values, in this case []int, a slice of integers

    for i := range values {
        sum += values[i]
    }

    return sum
}
```

Functions can return multiple values, most commonly this is a normal return value and an error, the error is `nil` if nothings gone wrong. This is important because Go doesn't have conventional structured syntax handling. Example:

```Go
// Go typically doesn't include get, that's not a Go convention
func fullName(f, l string) (string, int) {
    full := f + " " + l
    length := len(full)
    return full, length
}

fullName, nameLength := fullName("Josh", "String")
```

Another example, here the value names are declared in the function signature:

```Go
func fullName(f, l string) (full string, length int) {
    full = f + " " + l // No need for := as the type is already assigned and doesn't need to be infered
    length = len(full)
    return // No need to explicitly return the values as they're named in the sig
}
```

## Deferring function calls

Using the `defer` keyword sets the code to execute after everything else in the function has finished, so in this case the output would read: "Open the file" and then "Close the file". Defers are in lifo order: last in, first out.

```Go
func main() {
    defer fmt.Println("Close the file")
    fmt.Println("Open the file")
}
```
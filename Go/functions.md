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
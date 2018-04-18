# Error Handling in Go

```Go
func main() {
    f, err := os.Open("filename.txt") // This file doesn't exist!

    if err == nil {
        fmt.Println(f)
    } else {
        fmt.Println(err.Error())
    }

    // Create our own error objects
    // This allows creating custom error objects for functions
    myError := errors.New("My error string") // Requires "errors" import
    fmt.Println(myError)
}
```

Find out if an item is in a data structure like a map:

```Go
attendance := map[string][bool]{
    "Ann": true,
    "Mike": true}
}
attended, ok := attendance["Mike"]

if ok {
    fmt.Println("Mike attended?", attended)
} else {
    fmt.Println("No info for Mike")
}
```
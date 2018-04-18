# Go IO

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

### Read a file

```Go
func main() {
    fileName := "./hello.txt"

    content, err := ioutil.ReadFile(filename)
    checkError(err)

    result := string(content) // Convert content from bytes to a string
    fmt.Println("Read from file:", result)
}

func checkError(err error) {
    if err != nil {
        panic(error)
    }
}
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

## Writing to a file

```Go
func main() {
    content := "Hello from Go!"

    file, err := os.Create("./fromString.txt")
    checkError(err)
    defer file.Close()

    ln, err := io.WriteString(file, content)
    checkError(err)

    fmt.Printf("All done with file of %v characters", ln)

    // Write binary file

    bytes := []byte(content)
    ioutil.WriteFile("./fromBytes.txt", bytes, 0644)
}

func checkError(err error) {
    if err != nil {
        panic(error)
    }
}
```
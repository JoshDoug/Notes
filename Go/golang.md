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

## Variable assignments

Functions can return variables (kind of like MatLab) and by providing returns it will infer the variables, example:

```Go
stringLength, err := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

If you don't want all the return types, use an underscore:

```Go
stringLength, _ := fmt.Println(str1, str2, str3) // Print the length of the strings and return the length and an error object(?)
```

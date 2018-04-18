# Go HTTP  Server

Go provides a simple HTTP server!

Example of a simple implementation that just returns a heading:

```Go
package main

import (
  "net/http"
  "fmt"
)

type Hello struct{}

func (h Hello)  ServeHTTP(w http.ResponseWriter, r *http.Request) {
  fmt.Fprint(w, "<h1>Hello from the Go web server!</h1>")
}

func main() {
  var h Hello
  err := http.ListenAndServe("localhost:4000", h)
  checkError(err)
}

func checkError(err error) {
  if err != nil {
    panic(err)
  }
}
```
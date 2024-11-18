# Tour of Go

I am documenting my learnings from [Tour of Go](https://go.dev/tour/list)

```bash
go version
# The go version that I am using:
go version go1.23.3 linux/amd64 # output of go version command
```

## Packages

The best practice of naming a package is same as the last import of the package; for example when we import "math/rand" then the files should have a package name as "rand" by convention

The following is factored import statement:

```go
import (
  "fmt",
  "math/rand"
)
```

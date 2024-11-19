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

A package can have any number of files based on our requirement in the following case we can create two **separate** files with package name as `main`, but the beauty of a package is we can access any variable, constants, types and functions within the package even if the code exists in separate files.


File 1: 

```go
======
random.go
======

package main

import "math/rand"

func getRandomNumber() int {
  return rand.Intn(10)
}
```

File 2:

```go
======
main.go
======
package main

import "fmt"

func main() {
  fmt.Printf("Lucky number is: %d!\n",getRandomNumber())
}

```

The package named `main` is a special case because in a codebase with a `package main` files indicates it contains code which can be run or build for an executable application. It is not necessary that `main.go` should contain the function `main()` but it a convention.  


## Exported names

A rule of thumb for exported names from a package is the first letter of the name is in uppercase for example `math.Pi`, but names without uppercase are private within the package and cannot be exported by another file.

## Functions

In golang, functions can take zero or more arugments

For example:

```go
package main

import "fmt"

func add(a int, b int) int {      
  return a+b
}

func main() {
  fmt.Println(add(2+3))
}

```

The below function is same as the above function declaration because the only difference is we make use of the shorthand of using the only one type for function parameters if they share the same type.

```go
func sum(a,b int) int {
  return a+b
}
```

> NOTE: main function does not take any argument

Functions can multiple return values in golang

```go
package main

import "fmt"

func swap(a,b string) (string,string) {
  return b,a
}

func main() {
  a, b := swap("Hello", "World")
  fmt.Println(a,b)
}
```

The following code is an example of "naked" return in golang where the return statement has no arguments and the two named variables values are returned

```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

func main() {
	var a, b int=split(17)
	fmt.Println(a,b)
}
```

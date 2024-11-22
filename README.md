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

Functions can return multiple return values as shown below

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

The following code is an example of "naked" return where the return statement has no arguments and the two variables are defined on top of the function type syntax

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

## Variables

With variable statement we can declare list of variables followed by the type similar to function arguments.

Variables can be scoped at package or function level

```go
package main

var c, java, python bool

func main() {
  var i int
  fmt.Println(i, c, java, python) // 0 false false false
}
```

Variables can include initializers for each variable declared

```go
package main

import "fmt"

var i, j int = 1, 2

func main() {
  var c, python, java = true, false, "no!"
  fmt.Println(i, j, c, python, java) // 1 2 true false no!
}

```

Variables can be declared without the `var` keyword (with `:=` syntax) which implicitly assigns the type based on the value defined during declaration

```go
package main

import "fmt"

a := 3 // this is not valid

func main() {
 var i,j int=1,2
 k := 3
 c, python, java := true, false, "no!"
 fmt.Println(i,j,k,c,python,java)
}

```

## Basic Types

- `bool`
- `string`
- Signed Integer
  - `int`
  - `int8`
  - `int16`
  - `int32`
  - `int64`
- Unsigned Integer
  - `uint`
  - `uint8`
  - `uint16`
  - `uint32`
  - `uint64`
  - `uintptr`
- `byte` //alias for uint8
- `rune` // alias for int32
- `float32`
- `float64`
- `complex64`
- `complex128`

NOTE: `int`, `uint` and `uintptr` consists 32 bits for 32-bit systems and 64 bits for 64-bit systems.



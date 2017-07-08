# Go Language Overview

## Types

- int, int8 etc
- bool
- string
- float32, float64 (64 by default)

## Packages - public and private variables

When it comes to declaring variables, to have them available to other files when the package is imported, declare the variable with a capital letter.

Lowercase variables are private.

## Variables

```go
// outside of func
var greeting = "hello"

func main() {
	// inside of func
	greeting := "Hello from Go"
	fmt.Println(test)
	fmt.Println(greeting)
}
```

### Variable declarations and assigning

```go
func main() {
	var a int
	a = 2
	var b, c int
	b = 2
	c = 3
	d := 5	// same as var d = 5
	var e = 10 // type is inferred

	// you'll need to use all the above variables
	// otherwise there will be a declaration err
	// thrown
}
```

- Variable names must start with a letter
- Uppercase variables and funcs can be used outside of the package
- Lowercase cannot
- Declaring type can come after the variable name eg `var floating float64 = 1.4`
- Casting `float64(variable)`
- Errors are thrown for mismatched types
- For scope, you are able to declare blocks by themselves
	- Each package is a implicit block

## Functions

```go
// not available outside the package
func main() {
	myFunction()
}

func myFunction() {
	fmt.Println("Running myFunction")
}

func MyPublicFunction() {
	fmt.Println("Running MyPublicFunction")
}
```

You can enforce type safety for parameters by adding the type expected to the function `func myFunc(test string, number int) {}`

- Go doesn't allow default parameter values
- No named values
- No method overloading

For returning a certain value, you can enfore this by the following
```
func myFunc(test string, number int) int {}
func myFuncTwo(numberOne int, number int) (sum int) {
	return number + numberOne;
}
func myFuncThree(number int) (difference int) {
	difference = number + 4;
}
```

### Multiple return values

```go
package main

import (
	"fmt",
	"math",
	"log"
)

func main() {
	squareRoot, err := squareRoot(-1)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(squareRoot)
}

func squareRoot(x float64) (float64, error) {
	x < 0 {
		return 0, fmt.Errorf("Can't take a negative number")
	}
	return math.Sqrt(x), nil
}
```

As for errors

```go
package main

import (
	"fmt",
	"os"
)

// panic errors - no good!
func mainBad() {
	fileInfo, _ := os.Stat("existent.txt")
	fmt.Println(fileInfo.Size())
	fileInfo, _ := os.Stat("nonexistent.txt")
	fmt.Println(fileInfo.Size())
}

// instead, do this
func main() {
	fileInfo, error := os.Stat("existent.txt")
	if error != nil {
		fmt.Println(error)
	} else {
		fmt.Println(fileInfo.Size())
	}
	fileInfo, error := os.Stat("nonexistent.txt")
	if error != nil {
		fmt.Println(error)
	} else {
		fmt.Println(fileInfo.Size())
	}
}
```

### The Go Formatting Tool

`go fmt <filename>` will update the file itself and it will nicely format it.

## Control Structures

### For loops

```go
for i := 1; i <= 3; i++ {
	fmt.Println(i)
}
```

### If statements


```go
if true {
	fmt.Println("You'll come here")
} else if false {
	// ...
} else {
	// ...
}
```

### Switch statement

Switch statements look like they do not need a break.

```go
switch doorNumber {
	case 1:
		fmt.Println("new car ")
	case 2:
		// ...
	default:
		// ...
}
```
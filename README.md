# Go

* Go is the statically type language.
* Is is strongly typed language.
* It is compiled language.
* It has fast compile time.
* It have built-in concurrency (goroutines)
* It also have garbage collection, which is used to free up the memory which is unused.
* It is used for the high-performance server side applications.
* Performance is faster thean compared to FastAPI.
* The ideal use of Go is for high through put and low latency API's 
* source code is directly converted to the machine code

The main difference between package and module:

Package is the collection of files and module is the collection of packages.

## Constants, Variables and Basic Data types

### constants

Once you declare the constant you can change the value of the constant

``` go
const myConst string = "anu"

myConst = "another value"    // gives you an error
```

### variables

```go
var intNum int = 2
var intNum2 uint8 = 67    // unsigned 8 byte integer
var myString string = "my name is anu"
fmt.Println(len("test"))     // it gives the length of the string, here the length is not the number of charaters but the number of bytes.
// Go uses UTF encoding
var myRune rune = 'a'
var myBoolean bool = false
```
### types

Types of Int - int, int8, int16, int32, int64 (default value - 0)

Types of Unsigned Int  - uint, uint8, uint16, uint32, uint64 (default value - 0)

Types of Float - float32, float64

Default value for rune - 0

default value for string - ''

default value for boolean - false

Arthematic operations - you can't perform operations with mix type. (Go is strongly typed)

one datatype is not added to another datatype, if you want to do that you need to cast to the common datatype. 

```go
var intNum int = 3
var floatNum float32 = 2.6
var resultNum float32 = floatNum + float32(intNum)      // casting int to float
```

## Type Interface
  
Type Interface a compiler feature that automatically determines the data type of a variable or expression based on its context and usage within a program

``` go
intNum := 3

var int1, int2 int = 1, 2
var int1, int2 = 1, 2
int1, int2 := 1, 2

// all gives the same value
```

## Functions and Control Statements


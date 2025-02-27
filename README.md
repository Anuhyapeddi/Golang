# Go

* Go is the statically type language.
* Is is strongly typed language.
* It is compiled language.
* It has fast compile time.
* It have built-in concurrency (goroutines)
* It also have garbage collection, which is used to free up the memory which is unused.
* It is used for the high-performance server side applications.
* Performance is faster then compared to FastAPI.
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
fmt.Println(len("test"))
// it gives the length of the string, here the length is not the number of charaters but the number of bytes.
// Go uses UTF encoding
var myRune rune = 'a'
var myBoolean bool = false
```
### types

* Types of Int - int, int8, int16, int32, int64 (default value - 0)
* Types of Unsigned Int  - uint, uint8, uint16, uint32, uint64 (default value - 0)
* Types of Float - float32, float64
* Default value for rune - 0
* default value for string - ''
* default value for boolean - false

Arthematic operations - you can't perform operations with mix type. (Go is strongly typed)

You cannot add two different datatypes, if you want to do that you need to cast to the common datatype. 

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

``` go
package main        // it is the special file, this files tells the complier to start you compilation from this file
import "fmt"        // fmt package is used to display on the terminal/ console

func main(){        // This is the main function
    var variable1 string = "Hi my name is anu"
    var variable2 string = "This is my third day of the work"
    myfirst(variable1, variable2)
}

func myfirst(variable1 string, variable2 string){
    fmt.Println(variable1)
    fmt.Println(variable2)
}

```
### errors

* error is an another built-in type in go
* Rather then returning error, we use this error type
* The default value of error is nil

``` go
package main

import (
    "fmt"
    "errors"    // import errors type to use them
)

func main(){
    var num1 int = 2
    var num2 int = 4
    var res, rem, err= division(num1, num2)
    if err!=nil{         // checking if the err is nil or not
        fmt.Println(err.Error())
    }else if rem == 0{
        fmt.Printf("This result of this integer divisor is %v ", res)
    }else {
         fmt.Println(res, rem)
         fmt.Printf("The is the divisor %v and this is the remainder %v ", res, rem)
    }

}

func division(num1 int, num2 int) (int, int, error){
    var err error      // initizing the error type
    if num2==0{
        err = errors.New("Cannot divide with zero")      // calling new method
        return 0, 0, err
    }
    var res int = num1/num2
    var rem int = num1%num2
    return res, rem, err
}
```
### if else statements

``` go
package main

import (
    "fmt"
)

func main(){
    var sub1 int = 20
    var sub2 int = 30
    var res string = subjects(sub1, sub2)
    fmt.Println(res)
}

func subjects(sub1 int, sub2 int) (string){
    var res int =  sub1 + sub2
    if res >= 60{
        return "eligible for next sem"
    } else if res < 60 && res > 40{
        return "Need to take an extra credit to get eligible"
    } else {
        return "You failed! Need to take this subject again"
    }
}
```
### and or 

and - &&
or - ||

### switch statements

``` go
package main

import (
    "fmt"
)

func main(){
    var sub1 int = 20
    var sub2 int = 30
    var res string = subjects(sub1, sub2)
    fmt.Println(res)
}

func subjects(sub1 int, sub2 int) (string){
    var res int =  sub1 + sub2
    switch{
        case res >= 60:
            return "eligible for next sem"
        case res < 60 && res > 40:
            return "Need to take an extra credit to get eligible"
        case res < 40:
            return "You failed! Need to take this subject again"
        default:
            return "contact admin"
    }
}

```

### conditional switch statements

``` go
package main

import (
    "fmt"
)

func main(){
    var sub1 int = 20
    var sub2 int = 70
    var res string = subjects(sub1, sub2)
    fmt.Println(res)
}

func subjects(sub1 int, sub2 int) (string){
    var res int =  sub1 + sub2
    switch res{             // confitional switch statement
        case 100:
            return "A"
        case 90:
            return "B"
        case 80:
            return "C"
        default:
            return "F"
    }
}

```

## Arrays, Slices, Maps and Loops

### Arrays

* Fixed Length
* same type
* indexable
* Contiguous in Memory

``` go
package main

import (
    "fmt"
)

func main(){
    var intArr [3]int32 = [3]int32{1,2,3}     // assigning the 
    intArr := [3]int32{1,2,3}
    intArr := [...]int32{1,2,3}
    var intArr [3]int32      // declaring the array with size 3 and with int32 datatype
    intArr[0] = 43      // Assigning the vale
    fmt.Println(intArr[0])
    fmt.Println(intArr[1:3])        // 3 is excluded
    fmt.Println(&intArr[0])         // memory location
    fmt.Println(&intArr[1])
    fmt.Println(&intArr[2])
}
```

### slices
slice is a dynamically-sized, flexible view into a contiguous sequence of elements within an array. It provides a way to work with portions of an array without copying the underlying data.

In other words slices are wrapper around the arrays, which gives a more general, powerful and convenient interface to sequences of data.

Operations on slices include:
* Accessing elements: slice[index]
* Slicing: slice[low:high], slice[:high], slice[low:]
* Appending: append(slice, elements...)
* Copying: copy(destSlice, srcSlice)
* Getting length: len(slice)
* Getting capacity: cap(slice)

``` go
// by emitting the length value we have slice

package main

import (
    "fmt"
)

func main(){
    var intSlice []int32 = []int32{1,2,4}
    intSlice = append(intSlice, 6)      // append method takes 2 arguments; slice name and number to be appended
    fmt.Println(intSlice)

    var intSlice2 []int32 = []int32{3,4}
    intSlice = append(intSlice, intSlice2...)       // ... -> spread function; it appends entire list to the intSlice
    fmt.Println(intSlice)

    var intSlice3 []int32 = make([]int32, 4, 8)  //  make -> it takes 3 arguments; type and size, length, capacity
    
}
```
### maps

``` go
package main

import (
    "fmt"
)

func main(){
    var myMap map[string]uint8 = make(map[string]uint8)     // defining the map
    myMap = map[string]uint8{"anu": 24, "chinnu": 25}   // assigning values
    fmt.Println(myMap)
    fmt.Println(myMap["anu"])       // get a value using key
    fmt.Println(myMap["abhi"])      // it will return 0; map will always return a value if the key is not present in the map.
    var age, ok = myMap["anu"]      // ok -> will return true if the value is present in the map
    if ok{
        fmt.Printf("The age is %v", age)
    } else{
        fmt.Println("Invalid name")
    }
    delete(myMap, "anu")        // deleting from the map -> map name, key (which key, value should be deleted)    

}
```
### loops

``` go
package main

import (
    "fmt"
)

func main(){
    var myMap map[string]uint8 = make(map[string]uint8)
    myMap = map[string]uint8{"annu": 24, "chinnu": 34}
    
    // prints the names in the map
    for name := range myMap{
        fmt.Printf("name: %v \n", name)
    }
    
    // prints numbers from 1 to 10
    for i:=0; i<=10; i++{
        fmt.Println(i)
    }
}
```
## Strings and Rune

* Strings represent UTF-8 in go
* Strings represent in binary formate by using ASCII encoding using 7-bits
* rune is generally used to represent string in byte formate
* strings are not changable

## Structs and Interfaces

### structs

* It can hold difference types of datatypes

``` go
```







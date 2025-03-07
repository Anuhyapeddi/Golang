# Go

* Go is the statically type language.
* It is strongly typed language.
* It is compiled language.
* It has fast compile time.
* It have built-in concurrency (goroutines)
* It also have garbage collection, which is used to free up the memory that is unused.
* It is used for the high-performance server side applications.
* Performance is faster then compared to FastAPI.
* The ideal use of Go is for high through-put and low latency API's 
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
    var res, rem, err = division(num1, num2)
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
    var intArr [3]int32 = [3]int32{1,2,3}     // assigning the array
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
    var myMap map[string]uint8 = make(map[string]uint8)     // defining the map; map[string]uint8 -> string = key datatype and uint8 = value datatype
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

Structs are composite data types that group together variables (fields) under a single name. They provide a way to create custom data structures, similar to classes in other languages, but without inheritance.

* structs is defining your own type
* type gasEngine struct{} ; type - keywords, gasEngine - name of the type, struct - defining the struct type
* struct can store any datatypes in it

``` go
package main

import (
    "fmt"
)

type gasEngine struct{
    mpg uint8           // mpg and gallons are the fields
    gallons uint8
//     ownerName owner
    owner
    int
}

type owner struct{
    name string
}

func main(){
    var myEngine gasEngine = gasEngine{25, 15, owner{"anu"}, 17 }   // assigning values to the fields
    myEngine.mpg = 20                       // reassigning the value
//     fmt.Println(myEngine.mpg, myEngine.gallons, myEngine.ownerName.name)
    fmt.Println(myEngine.mpg, myEngine.gallons, myEngine.name, myEngine.int)
}
```
Defining methods in structs 

``` go
package main

import (
    "fmt"
)

type gasEngine struct{
    mpg uint8
    gallons uint8
}

// defining methods in structs

func (e gasEngine) milesLeft() uint8{
    return e.gallons*e.mpg
}

func canMakeIt(e gasEngine, miles uint8){
    if miles <= e.milesLeft(){
        fmt.Println("you can make it there")
    } else {
        fmt.Println("need to fuel up first")
    }
}

func main(){
    var myEngine gasEngine = gasEngine{25, 15}
    fmt.Printf("Total miles left in the tank : %v", myEngine.milesLeft())
}
```
### interfaces

Interfaces define a set of methods that a type must implement to satisfy the interface. They specify behavior without dictating implementation, enabling polymorphism and loose coupling. Any type that implements all the methods of an interface implicitly satisfies that interface. 

``` go
package main

import (
    "fmt"
)

type gasEngine struct{
    mpg uint8
    gallons uint8
}

func (e gasEngine) milesLeft() uint8{
    return e.gallons*e.mpg
}

func canMakeIt(e gasEngine, miles uint8){
    if miles <= e.milesLeft(){
        fmt.Println("you can make it there")
    } else {
        fmt.Println("need to fuel up first")
    }
}

type engine interface{
    milesLeft() uint8
}

func main(){
    var myEngine gasEngine = gasEngine{25, 15}
    canMakeIt(myEngine, 50)
}
```
## Pointer

* Pointer are the special type
* These are the variables which store the memory locations rather than the integers/ floats
  
## Goroutines

* goroutines are used to handle multiple functions and run concurrently
  
## Channels
* channels enable goroutines which to pass around information
* they hold data like integer, slices
* they are thread safe i.e we avoid data races while reading or writing from the memory
* we can listen data -> we can listen when the data is added or removed from the channel
* And we can block code execution when one of these events got executed

NOTE: A "data race" is a concurrency bug that occurs when multiple threads in a program attempt to access the same memory location concurrently

The below program gives you a deadlock error, we assigned channel c with 1 after that we are moving 1 to i. but when we are running this program it is trying to access element which is in channel, but the channel is empty. So that is why we are getting deadlock error.

``` go
package main
import("fmt")
func main(){
    var c = make(chan int)      // channel to hold a value, it's holding int value  // c: []
    c <- 1                      // to assign a value to the channel                 // c: [1]
    var i = <- 1                // retrieving the channel and storing in i          // c: [ ] channel becomes empty and i = 1 i becomes 1
    fmt.Println(i)              // deadlock error                                   // we are trying to access the element which is not present in the channel.
}
```

To solve this issue we have to use goroutines.

``` go
package main

import("fmt")

func main(){
    var c = make(chan int)
    go process(c)       // setting the goroutine
    fmt.Println(<-c)    // rather than storing the value in any variable; we are directly printing it right after it popped out of the channel
}

func process(c chan int){
    defer close(c)      // do this stuff right before the function exists
    c <- 123            // write a value to it
}
```

### buffer channel

Rather than storing one value in the channel, it can store multiple values at the same time.

In the regular channel the process function will stay active till the main function is done with the channel.

But there is no need for process function to hang around, it can work and get exited from the loop. Let the main function do it's thing. By using buffer channel we can add 5 values in the channel, so we are creating the space for 5 integers. we can use that space rather than waiting for the variable get empty for the popped element.

``` go
// without buffer channel

package main

import(
"fmt"
"time"
)

func main(){
    var c = make(chan int)
    go process(c)
    for i := range c {
        fmt.Println(i)
        time.Sleep(time.Second*1)
    }

}

func process(c chan int){
    defer close(c)
    for i := 0; i <= 5; i++ {
        c <- i
    }
    fmt.Println("Exiting the process")

}

// output

// 1
// 2
// 3
// 4
// 5
// Exiting the process
```

``` go
// with buffer channel

package main

import(
"fmt"
"time"
)

func main(){
    var c = make(chan int, 5)
    go process(c)
    for i := range c {
        fmt.Println(i)
        time.Sleep(time.Second*1)
    }

}

func process(c chan int){
    defer close(c)
    for i := 0; i <= 5; i++ {
        c <- i
    }
    fmt.Println("Exiting the process")

}

// output

// Exiting the process
// 1
// 2
// 3
// 4
// 5
```
## Generics

Allowing a function receving additional parameters

Imagine you are having a different functions which accepts different data types. Rather than writing all functions, we can use generics which can accept different data types in one function. 

``` go
// Generics in Go allow you to write functions and data structures that work with different types without repeating code. Instead of specifying a single type, you use **type parameters**, making the code more flexible and reusable.

// Example:
package main

import "fmt"

// Generic function with a type parameter T
func Print[T any](value T) {
    fmt.Println(value)
}

func main() {
    Print(10)       // Works with int
    Print("Hello")  // Works with string
    Print(3.14)     // Works with float
}
```

## API Gateway

An API Gateway is a software component that acts as a single entry point for all API requests, essentially a "front door" to a system, receiving client requests and routing them to the appropriate backend services, while also performing tasks like authentication, authorization, load balancing, and request processing based on defined policies; effectively managing interactions between clients and application services by providing a centralized point of access

* Authentication & Authorization: May integrate with RBAC or external identity systems.
* Routing & Load Balancing: Distributes incoming requests to the appropriate backend service or microservice.

NOTE: 
* RBAC - Role-based access control (RBAC) is a security method that limits access to systems based on a user's role
* Unmarshalling - loading the JSON into the struct (the process of converting data from a lower-level representation into a higher-level structure)

## API Creation

``` go
package main

import (
    "encoding/json"
    "net/http"
    "fmt"
)

// Struct for handling JSON data
type User struct {
    Name  string `json:"name"`
    Email string `json:"email"`
}

// Handler for GET request
func pingHandler(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(map[string]string{"message": "pong"})
}

// Handler for POST request
func userHandler(w http.ResponseWriter, r *http.Request) {
    if r.Method != http.MethodPost {
        http.Error(w, "Invalid request method", http.StatusMethodNotAllowed)
        return
    }

    var user User
    err := json.NewDecoder(r.Body).Decode(&user)
    if err != nil {
        http.Error(w, "Bad request", http.StatusBadRequest)
        return
    }

    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(user)
}

// main function

func main() {                  
    http.HandleFunc("/ping", pingHandler)
    http.HandleFunc("/users", userHandler)

    fmt.Println("Server is running on port 8080...")
    http.ListenAndServe(":8080", nil) // Start the server
}

``` 
go run main.go -  to run the above code

``` go
func homePage(w http.ResponseWriter, r *http.Request) {
    fmt.Fprint(w, "Hello, World!") // Sends "Hello, World!" as a response
}

// w http.ResponseWriter → Used to send a response back to the client (e.g., a browser or API caller).

// r *http.Request → Represents the incoming request from the client (contains details like method, headers, body, etc.)

// Here, w is used to send "Hello, World!" as the response to the client that made the request.
```
Gorilla Mux

``` go
package main

import (
"fmt"
"log"
"net/http"
"encoding/json"
"github.com/gorilla/mux"    // import gorilla mux package
)

type User struct{
    Name string `json:"Name"`
    Age int64 `json:"Age"`
}

type Users []User

func allUsers(w http.ResponseWriter, r *http.Request){
    users := Users{
        {Name: "Alice", Age: 17},
        {Name: "Bob", Age: 24},
        }
    fmt.Println(users)
    json.NewEncoder(w).Encode(users)
    }


func homePage(w http.ResponseWriter, r *http.Request){
    fmt.Fprint(w, "Homepage endpoint hit")
}

func aboutPage(w http.ResponseWriter, r *http.Request){
    fmt.Fprint(w, "This is about page")
}

func postUser(w http.ResponseWriter, r *http.Request){
    fmt.Fprint(w, "creating the POST call")
}

func handleRequest() {
    myRouter := mux.NewRouter().StrictSlash(true)    // init gorilla mux

    myRouter.HandleFunc("/", homePage)
    myRouter.HandleFunc("/about", aboutPage)
    myRouter.HandleFunc("/users", allUsers).Methods("GET")     // get call
    myRouter.HandleFunc("/users", postUser).Methods("POST")    // post call
    log.Fatal(http.ListenAndServe(":8080", myRouter))
}

func main(){
    handleRequest()
    fmt.Println("Server is running in port 8080")
}
```

## API Authentication

## Middleware

## Package Management

 







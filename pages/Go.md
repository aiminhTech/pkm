child:: [[Programming Language]]
library:: [[Chi Router]], [[Goose]], [[pgweb]], [[pgx]]
link::  https://go.dev/

-
- ## 📔 Learning
	- https://frontendmasters.com/courses/complete-go/
	- https://frontendmasters.com/courses/vanilla-js-go/
	- https://frontendmasters.com/courses/htmx/ #HTMX
	-
- ## Overview
  collapsed:: true
	- A **statically typed, compiled programming language** created by Google
	- Designed to be **simple, fast and efficient**, especially for systems programming and large-scale distributed applications
	- ### Key Features
		- **Simple & Clean**: The language has a small set of features, so it’s easier to learn and read compared to bigger languages like C++ or Java.
		- **Compiled & Fast**: Go compiles directly to machine code, so programs run quickly (like C) without needing a virtual machine.
		- **Cross-Platform**: You can compile Go programs to run on Windows, Linux, macOS, etc., with very little setup.
		- **Concurrency Support**: Go has built-in support for handling multiple tasks at the same time (via **goroutines** and **channels**). This makes it great for servers, networking, and cloud apps.
		- **Static Typing + Safety**: Variables have fixed types, which helps catch errors before running the program.
		- **Strong Standard Library**: Go provides a powerful built-in library for things like networking, web servers, file handling, and more.
- ## Installation
  collapsed:: true
	- https://go.dev/doc/install
	- **IPI:**  https://git.ipip.ch/projects/TST/repos/hello-go/browse
		- **Taskfile**
			- ```yml
			  # yaml-language-server: $schema=https://taskfile.dev/schema.json
			  version: "3"
			  
			  tasks:
			    enter:
			      interactive: true
			      cmd: nix-shell -p go -p gopls -p go-tools
			  
			    git:localrepo:usessh:
			      cmds:
			        - git config --local url."ssh://git@git.ipip.ch:7999/".insteadOf "https://git.ipip.ch/"
			  
			    setup:
			      cmds:
			        - go telemetry off
			        - go env -w GOPRIVATE=git.ipip.ch
			        - go env -w GOPROXY=https://repository.ipip.ch/repository/golang-public/,direct
			        - go env -w 'GOSUMDB=sum.golang.org https://repository.ipip.ch/repository/golang-sum-proxy/'
			        - task: git:localrepo:usessh
			  
			    build:
			      cmds:
			        - go build {{.CLI_ARGS}}
			  
			    build:static:
			      cmds:
			        - CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -trimpath -ldflags="-s -w" {{.CLI_ARGS}}
			  
			    build:static:glibc:
			      cmds:
			        - go build -ldflags "-s -w -linkmode=external -extldflags=-static" {{.CLI_ARGS}}
			  
			    build:wasm:
			      cmds:
			        - GOARCH=wasm GOOS=js go build {{.CLI_ARGS}}
			  
			    flake:update:
			      desc: "Updates flake.lock"
			      dir: "{{.ROOT_DIR}}"
			      cmds:
			        - nix flake update --refresh {{.CLI_ARGS}}
			  
			  ```
		-
-
- ## Basics
  collapsed:: true
	- ### CMD
		- |**CMD**|**Description**|
		  |--|--|
		  |**`go mod init`**|Use to start a new Go module (project) and generate `go.mod` file|
		  |**`go run [filename]`**|Compiles and immediately runs Go program|
		  |**`go build [filename]`**|Compiles Go program into binary, but **does not run it**|
	- ### `go.mod`-File
		- It’s the **module definition file** in a Go project.
		- Tells Go:
			- The **module path** (the import path others use to reference your code).
			- The **Go version** your project targets.
			- The **dependencies** your project uses (and their versions).
	- ### Printing (`fmt`)
	  collapsed:: true
		- ### `Println`
			- Prints its arguments **separated by spaces**.
			- Adds a **newline at the end automatically**.
			- No formatting needed.
			- ```go
			  go func main() {
			      name := "Alice"
			      age := 25
			      fmt.Println("Name:", name, "Age:", age)
			  }
			  
			  // Output:
			  // Name: Alice Age: 25
			  ```
		- ### `Printf`
			- Prints **formatted output** using **format verbs**
			- Does not add a newline automatically. Need `\n` if want one
			- **Common Format Verb**
				- |**Verb**|**Type**|**Example**|
				  |--|--|--|
				  |`%s`|string|"Alice"|
				  |`%d`|int|25|
				  |`%f`|float|3.14|
				  |`%t`|bool|true|
				  |`%v`|any|default format|
			- ```go
			  func main() {
			      name := "Alice"
			      age := 25
			      fmt.Printf("Name: %s, Age: %d\n", name, age)
			  }
			  
			  // Output
			  // Name: Alice, Age: 25
			  ```
		-
	- ### Declaring Variables
	  collapsed:: true
		- ```go
		  // Using var
		  var city string = "Bern"
		  
		  // Type inference
		  // -- Go infers that y is an int 
		  var y = 20
		  
		  // Short declaration
		  // -- Most common inside functions
		  // -- Cant be used at package level 
		  z := 30
		  
		  // Multiple declarations 
		  var a, b, c int = 1, 2, 3
		  var name, age = "Alice", 25
		  ```
	- ### Basic Types
	  collapsed:: true
		- #### Strings
			- ```go
			  var msg string = "Hello, Go!"
			  ```
		- #### Numbers
			- **Integers**: `int`, `int8`, `int16`, `int32`, `int64`
			- **Float**: `float32`, `float64`
			- ```go
			  var age int = 30
			  var pi float64 = 3.1415
			  ```
		- #### Booleans
			- ```go
			  var isActive bool = true
			  
			  ```
		- #### Zero Values
			- If you declare a variable without assigning a value, it gets the **zero value**
				- Numbers → `0`
				- Booleans → `false`
				- Strings → `""` (empty string)
				- Pointers, slices, maps, etc. → `nil`
			- ```go
			  var s string  // "" (empty)
			  var n int     // 0
			  var ok bool   // false
			  ```
	- ### Constants
	  collapsed:: true
		- A variable whose value **cannot change** after compilation
		- Declaring using `const`
		- Must be assigned a **compile-time constant** value
		- ```go
		  // Constant
		  const Pi = 3.1415
		  const Greeting = "Hello, Go!"
		  
		  // Multiple Constants
		  // -- Declare several constants together using parentheses
		  const (
		      StatusOK = 200
		      StatusNotFound = 404
		  )
		  
		  // Typed vs Untyped Constants
		  // -- Untyped constants are more flexible; Go infers the type when used
		  const x int = 10    // typed
		  const y = 20        // untyped (Go infers type)
		  ```
	- ### Enums (using iota)
	  collapsed:: true
		- https://go.dev/wiki/Iota
		- Go **doesn’t have a built-in enum type** like some languages, but you can simulate enums using `const` + `iota`.
		- `iota` is a **counter** that starts at 0 inside a `const` block and increments by 1.
		- ```go
		  const (
		      Sunday = iota   // 0
		      Monday          // 1
		      Tuesday         // 2
		      Wednesday       // 3
		      Thursday        // 4
		      Friday          // 5
		      Saturday        // 6
		  )
		  
		  func main() {
		      fmt.Println(Monday)   // 1
		      fmt.Println(Saturday) // 6
		  }
		  ```
	-
- ## Functions
  collapsed:: true
	- ### Basic Syntax
		- ```go
		  // func : keyword to declare a function
		  // (a int, b int) : list of inputs with names and types.
		  // int: type of value returned (optional)
		  func add(a int, b int) in {
		    return a + b
		  }
		  
		  func main() {
		      sum := add(3, 5)
		      fmt.Println(sum) // 8
		  }
		  ```
	- ### Shorter Params Syntax
		- ```go
		  // If consecutive parameters share the same type, we can write:
		  func multiply(a, b int) int {
		      return a * b
		  }
		  ```
	- ### Multiple Return Values
		- ```go
		  func divide(a, b float64) (float64, float64) {
		      quotient := a / b
		      remainder := float64(int(a) % int(b))
		      return quotient, remainder
		  }
		  
		  func main() {
		      q, r := divide(10, 3)
		      fmt.Println(q, r) // 3.333333 1
		  }
		  ```
	- ### Named Return Values
		- ```go
		  func sumAndDiff(a, b int) (sum int, diff int) {
		      sum = a + b
		      diff = a - b
		      return // automatically returns sum, diff
		  }
		  ```
	-
- ## Conditional Statements
  collapsed:: true
	- ### `if`-Statement
		- ```go
		  // if
		  age := 18
		  if age >= 18 {
		    fmt.Println("You are an adult")
		  }
		  
		  // if ... else
		  if age < 18 {
		      fmt.Println("Minor")
		  } else {
		      fmt.Println("Adult")
		  }
		  
		  // if ... else if ... else
		  if x < 0 {
		      fmt.Println("Negative")
		  } else if x == 0 {
		      fmt.Println("Zero")
		  } else {
		      fmt.Println("Positive")
		  }
		  ```
	- ### `switch`-Statement
		- Go's `switch` is more powerfull than in many languages
			- No `break` needed (automatically stops after a match)
			- Multiple values per case allowed
			- Can use conditions instead of just values
			- ```go
			  // Basic
			  day := 3
			  switch day {
			  case 1:
			      fmt.Println("Monday")
			  case 2:
			      fmt.Println("Tuesday")
			  case 3:
			      fmt.Println("Wednesday")
			  default:
			      fmt.Println("Another day")
			  }
			  
			  // Multiple Values
			  switch day {
			  case 6, 7:
			      fmt.Println("Weekend")
			  default:
			      fmt.Println("Weekday")
			  }
			  
			  // Switch Without Expression (acts like chained ifs)
			  num := -5
			  switch {
			  case num < 0:
			      fmt.Println("Negative")
			  case num == 0:
			      fmt.Println("Zero")
			  default:
			      fmt.Println("Positive")
			  }
			  
			  
			  ```
		-
- ## Loops
  collapsed:: true
	- ### Basic `for` Loop
		- ```go
		  for i := 0; i < 1; i++ {
		      fmt.Println(i)
		  }
		  
		  // Output:
		  // 0
		  // 1
		  // 2
		  ```
	- ### `for` as `while` Loop
		- If you leave out the init & post statements, it works like a **while**
		- ```go
		  i := 0
		  for {
		    if (i > 3) {
		      break
		    }
		    i++
		  }
		  ```
-
- ## Arrays
  collapsed:: true
	- An Array in Go is a**fixed-size collection**  of elements of the same type
	- Length is part of its type → `[5]int` and `[10]int` are **different types**
	- **Zero values** apply → if not initialized, numbers are `0`, strings are `""`, booleans are `false`
	- ==**Fixed size**: cannot grow/shrink.==
	- ==**Value type**: assigning copies the whole array.==
	- ### Declaring
		- ```go
		  // Fixed length
		  var nums [3]int
		  fmt.Println(nums) // [0 0 0]
		  
		  // With values
		  var primes = [5]int{2, 3, 5, 7, 11}
		  fmt.Println(primes) // [2 3 5 7 11]
		  
		  // Count length
		  evens := [...]int{2, 4, 6, 8}
		  fmt.Println(len(evens)) // 4
		  ```
	- ### Accessing Elements
		- ```go
		  nums := [3]int{10, 20, 30}
		  fmt.Println(nums[0]) // 10
		  
		  nums[2] = 99
		  fmt.Println(nums)    // [10 20 99]
		  ```
	- ### Multidimensional Arrays
		- ```go
		  matrix := [2][3]int{
		      {1, 2, 3},
		      {4, 5, 6},
		  }
		  fmt.Println(matrix[1][2]) // 6
		  ```
- ## Slices
  collapsed:: true
	- A **dynamic, flexible view** into an underlying array
	- Unlike arrays, slices dont have a fixed size
	- Think of it as **a pointer to an array segment**, with
		- **length**: number of elements it currently holds
		- **capacity**: how many elements it can hold before needing a new array
	- ### Create Slices
		- ```go
		  // From an Array
		  arr := [5]int{10, 20, 30, 40, 50}
		  s := arr[1:4] // elements at index 1,2,3
		  fmt.Println(s) // [20 30 40]
		  
		  // Using []T{} literal
		  nums := []int{1, 2, 3}
		  fmt.Println(nums) // [1 2 3]
		  ```
	- ### Properties: Length and Capacity
		- ```go
		  arr := [5]int{1, 2, 3, 4, 5}
		  s := arr[1:3]
		  fmt.Println(s)        // [2 3]
		  fmt.Println(len(s))   // 2
		  fmt.Println(cap(s))   // 4 (from index 1 → end)
		  ```
	- ### Appending to Slices
		- ```go
		  // Use 'append' to grow a slice dynamically
		  s := []int{1, 2, 3}
		  s = append(s, 4, 5)
		  fmt.Println(s) // [1 2 3 4 5]
		  
		  // If capacity is exceeded, Go automatically allocates a new underlying array.
		  ```
	- ### Iterating over Slices
		- ```go
		  fruits := []string{"apple", "banana", "cherry"}
		  for i, fruit := range fruits {
		      fmt.Println(i, fruit)
		  }
		  ```
- ## Maps
  collapsed:: true
	- Stores data in **key-value pairs**
	- Keys must be **unique**
	- ### Declaring
		- ```go
		  // Using make
		  ages := make(map[string]int) // key=string, value=int
		  ages["Alice"] = 25
		  ages["Bob"] = 30
		  
		  fmt.Println(ages) // map[Alice:25 Bob:30]
		  
		  // Using a literal
		  capitalCities := map[string]string{
		    "USA": "Washington D.C.",
		    "India": "New Delhi",
		    "UK": "London",
		  }
		  fmt.Println(capitalCities) // map[India:New Delhi UK:London USA:Washington D.C.]
		  ```
	- ### Accessing Elements
		- ```go
		  age := ages["Alice"]     // 25
		  fmt.Println(ages["Tom"]) // 0 (key doesn’t exist → zero value for int)
		  ```
	- ### Updating / Adding
		- ```go
		  ages["Alice"] = 26 // update
		  ages["Charlie"] = 22 // add new key
		  ```
	- ### Deleting Keys
		- ```go
		  delete(ages, "Bob")
		  fmt.Println(ages) // map[Alice:26 Charlie:22]
		  ```
- ## Structs
  collapsed:: true
	- A custom **data type** that groups related fields (like a record or object)
	- ### Declaring
	  collapsed:: true
		- ```go
		  type Person struct {
		      Name string
		      Age  int
		  }
		  ```
	- ### Creating Structs Instances
	  collapsed:: true
		- ```go
		  // Using a literal
		  p1 := Person{Name: "Alice", Age: 25}
		  fmt.Println(p1) // {Alice 25}
		  
		  // Partial initialization
		  p2 := Person{Name: "Bob"}
		  fmt.Println(p2) // {Bob 0} (Age defaults to 0)
		  
		  // Using new
		  p3 := new(Person)
		  p3.Name = "Charlie"
		  p3.Age = 30
		  fmt.Println(p3) // &{Charlie 30} (returns pointer)
		  
		  ```
	- ### Nested Structs
	  collapsed:: true
		- ```go
		  type Address struct {
		      City, Country string
		  }
		  
		  type Employee struct {
		      Name    string
		      Address Address
		  }
		  
		  emp := Employee{
		      Name: "Alice",
		      Address: Address{City: "Zurich", Country: "Switzerland"},
		  }
		  fmt.Println(emp.Address.City) // Zurich
		  ```
	- ### Struct Methods
		- Go does not have classes, but we can attach methods to structs
		- ```go
		  type Person struct {
		    Name string
		    Age int
		  }
		  
		  // Method with VALUE receiver
		  func (p Person) Greet() {
		      fmt.Printf("Hello, my name is %s and I am %d\n", p.Name, p.Age)
		  }
		  
		  // Usage
		  p := Person{Name: "Alice", Age: 25}
		  p.Greet() // Hello, my name is Alice and I am 25
		  ```
	- ### Pointer
		- A **pointer** stores the memory address of a value
		- Pointers are written as `*Type`
		- The `&` operator gives the address, and `*` lets us get the value
		- ```go
		  x := 10
		  p := &x       // p is a pointer to x
		  fmt.Println(*p) // 10
		  *p = 20
		  fmt.Println(x)  // 20 (changed through pointer)
		  ```
	- ### Pointer Receiver vs Value Receiver
		- **Value receiver** → method works on a copy → original struct stays the same.
		- **Pointer receiver** → method works on original → changes are visible outside.
		- If a struct is **large** or you need to **modify it**, use pointer receivers.
		- For **read-only methods**, value receivers are fine.
		- ```go
		  // Value Receiver
		  func (p Person) Birthday1() {
		      p.Age++ // modifies a COPY
		  }
		  
		  p := Person{Name: "Alice", Age: 25}
		  p.Birthday1()
		  fmt.Println(p.Age) // 25 → unchanged
		  // p is a copy of the original Person.
		  // Any changes made inside this method do not affect the original struct.
		  --------------------------------------------------------------------------------
		  
		  // Pointer Receiver
		  func (p *Person) Birthday2() {
		      p.Age++ // modifies the original
		  }
		  
		  p := Person{Name: "Alice", Age: 25}
		  p.Birthday2()
		  fmt.Println(p.Age) // 26 → updated
		  // Go automatically converts p.Birthday2() to (&p).Birthday2() under the 
		  // hood if p is not already a pointer.
		  ```
-
- ## Creating a Go Project
  collapsed:: true
	- ### Example Structure
		- **`main.go`** → the entry point of the application. This is where `main()` lives.
		- **`internal/app/app.go`** → contains the main application logic, like initializing the app, logger, etc.
		- **`internal/routes/routes.go`** → likely intended for HTTP route definitions (common in web apps).
		- **`go.mod`** → declares the module path (`git.ipip.ch/quach/learning-go`) and dependencies.
	- ### `main.go`
		- Imports your internal `app` package using the module path.
		- Calls `NewApp()` to create an `App` instance.
		- Logs a message once the app starts.
		- In Go, `nil` is a **predeclared identifier** that represents the **zero value of pointers, interfaces, maps, slices, channels, and function types**. Essentially, it means **“nothing” or “no value”**.
		- ```go
		  package main
		  
		  import (
		  	"git.ipip.ch/quach/learning-go/internal/app"
		  )
		  
		  func main() {
		  	app, err := app.NewApp() // Create a new app instance
		  
		  	if err != nil {
		  		panic(err) // stop execution if there’s an error
		  	}
		  
		  	app.Logger.Println("Application started successfully")
		  }
		  
		  ```
	- ### `app.go`
		- Defines the `App` **struct** with a `Logger` field.
		- `NewApp()` is a **constructor function** returning a pointer to `App`.
		- Sets up a simple logger that writes to `stdout` with date and time.
		- ```go
		  package app
		  
		  import (
		  	"log"
		  	"os"
		  )
		  
		  type App struct {
		  	Logger *log.Logger
		  }
		  
		  func NewApp() (*App, error) {
		  	logger := log.New(os.Stdout, "", log.Ldate|log.Ltime) // initialize logger
		  
		  	app := &App{
		  		Logger: logger, // store logger in the struct
		  	}
		  
		  	return app, nil
		  }
		  ```
	-
	-
- ## Creating HTTP Server
  collapsed:: true
	- Can also use [[Chi Router]]
	- ### Example
	  collapsed:: true
		- ```go
		  package main
		  
		  import (
		  	"fmt"
		  	"net/http"
		  	"time"
		  
		  	"git.ipip.ch/quach/learning-go/internal/app"
		  )
		  
		  func main() {
		  	app, err := app.NewApp()
		  
		  	if err != nil {
		  		panic(err)
		  	}
		  
		  	app.Logger.Println("Application started successfully")
		  
		    	// Handle Routes
		    	// Registers a handler function for the /health route.
		  	// When someone visits http://localhost:8080/health, the HealthCheck 
		    	// function will run
		  	http.HandleFunc("/health", HealthCheck)
		  
		    // Define the HTTP Server
		  	server := &http.Server{
		  		Addr:         ":8080",
		  		IdleTimeout:  time.Minute,
		  		ReadTimeout:  10 * time.Second,
		  		WriteTimeout: 30 * time.Second,
		  	}
		  
		    // Start the Server
		  	err = server.ListenAndServe()
		  	if err != nil {
		  		app.Logger.Fatalf("Failed to start server: %v", err)
		  	}
		  }
		  
		  ```
	- ### HealthCheck Handler
		- `w http.ResponseWriter` → used to write responses back to the client.
		- `r *http.Request` → contains request information (method, headers, body).
		- `fmt.Fprintln` writes `"Status is available"` to the response body.
		- ```go
		  func HealthCheck(w http.ResponseWriter, r *http.Request) {
		  	fmt.Fprintln(w, "Status is available")
		  }
		  ```
		- When you visit `/health`, the browser will show: `Status is available`
	- ### Parsing Command-Line Flags
	  collapsed:: true
		- ```go
		  func main() {
		    // Create an integer variable that will store the port number
		    var port int
		    // Bind the flag to the variable
		    flag.IntVar(&port, "port", 8080, "go backend server port")
		    // Parse the flags
		    flag.Parse()
		    
		    // Rest of code....
		    
		    server := &http.Server{
		  	Addr: fmt.Sprintf(":%d", *port), // Use the port
		  	...
		  }
		  }
		  ```
		- **Usage**
			- Run on default port: `go run main.go`
			- Run on custom port: `go run main.go -port 9090`
-
- ## Testing
  collapsed:: true
	- ### The Standard `testing` Package
		- https://pkg.go.dev/testing
		- Go has a **built-in testing framework** in the `testing` package. It gives us the basics we need to write and run unit tests.
		- #### Key Features
			- `func TestXxx(t *testing.T)` is how you define a test function.
			- Run tests with `go test ./...`.
			- Provides methods like:
				- `t.Error`, `t.Errorf` → report failure, continue execution
				- `t.Fatal`, `t.Fatalf` → report failure, stop the test
		- ```go
		  package math_test
		  
		  import "testing"
		  
		  func Add(a, b int) int {
		      return a + b
		  }
		  
		  func TestAdd(t *testing.T) {
		      result := Add(2, 2)
		      if result != 4 {
		          t.Errorf("expected 4, got %d", result)
		      }
		  }
		  ```
	- ### Testify
		- https://pkg.go.dev/github.com/stretchr/testify
		- A popular **third-party testing toolkit** that makes tests more expressive and less verbose. It works *on top of* Go’s built-in `testing` package.
		- #### Main Components
			- **`assert`**: Assertions that fail but allow the test to continue.
			- **`require`**: Assertions that fail and stop the test immediately.
			- **`mock`**: Utilities for mocking objects and functions.
			- ```go
			  package math_test
			  
			  import (
			      "testing"
			    
			  	"github.com/stretchr/testify/assert"
			      "github.com/stretchr/testify/require"
			  )
			  // example with assert
			  func TestAdd(t *testing.T) {
			      result := 2 + 2
			      assert.Equal(t, 4, result)
			      assert.NotEqual(t, 5, result)
			  }
			  
			  // example with require
			  func Divide(a, b int) (int, error) {
			      if b == 0 {
			          return 0, fmt.Errorf("division by zero")
			      }
			      return a / b, nil
			  }
			  
			  func TestDivide(t *testing.T) {
			      result, err := Divide(10, 2)
			      require.NoError(t, err)   // stop if error is not nil
			      require.Equal(t, 5, result)
			  }
			  
			  ```
	- ### When to Use Which
		- | Tool | Strength | 
		  | `testing` (built-in) |  Always available, minimal, no dependencies. Great for small/simple checks. |
		  | `testify/assert` | Cleaner syntax for multiple checks in a test. |
		  | `testify/require` | Ensures tests stop immediately when a critical condition fails. | 
		  | `testify/mock` | Helpful for mocking interfaces in larger systems. |
		- <!--EndFragment-->
-
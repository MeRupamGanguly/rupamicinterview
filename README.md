
# One Stop Solution For Interview Preparation of Golang Developer

## Introduce Yourself
I have a background in BTech IT. My first company was Sensibol, where I worked as a Golang Backend Developer. My primary role was developing microservices using Golang, AWS, MongoDB, and Redis. Currently, I am working at Calsoft for Extreme Networks, focusing on a project related to data center automation. In this project,  My primary role is developing microservices with Golang, RabbitMQ, Kubernetes, MySQL, and GoSwitch for managing Multiple Switeches with Software.

## What Projects Have You Worked On?
- **PDL (Phonographic Digital Limited)**: A music distribution and royalty management platform.
- **Singshala**: A platform similar to TikTok but with the added feature of analyzing the audio components of videos and providing rankings based on that analysis.
- **Data Center Automation**: In this project, we create profiles that are essentially configurations applied to switch ports, and bind those configurations to the ports.


## Microservices vs Monolith
- **Microservices** are better for large projects where scaling and almost zero downtime are required. Bug fixing and maintaining the codebase are easier. A disadvantage of microservices can be inter-service network calls.
- **Monolith** is suitable for smaller projects but can become difficult to scale or maintain as the application grows.

## Authentication vs Authorization
- **Authentication** is about verifying identity. Users typically provide credentials such as a username and password, or biometric data, and the system checks these credentials against stored data to confirm their validity.
- **Authorization** is about granting permissions based on the verified identity. The system checks the user’s permissions and roles to determine what they can access or modify.

## Golang Garbage Collection
Golang uses automatic garbage collection to manage memory. Developers do not need to allocate or deallocate memory manually, which reduces memory-related errors.

## Pointer
A **pointer** holds the memory address of a variable, struct, function, or any data type.

- You can reference a variable to get its address using the `&` operator.
- You can dereference a pointer to access the value at the memory address it points to using the `*` operator.

```go
package main

import "fmt"

func main() {
    a := 9           // Declare an integer variable 'a'
    p := &a          // 'p' is a pointer that stores the address of 'a' (referencing)

    fmt.Println("Address of a:", &a)    
    // Outputs the memory address of 'a'
    fmt.Println("Value of p:", p)       
    // Outputs the memory address stored in p
    fmt.Println("Value at address p:", *p) 
    // Dereferencing p to get the value (outputs: 9)

    *p = 10          // Change the value of 'a' using the pointer
    fmt.Println("New value of a:", a)   // Outputs: New value of a: 10
}
```

### Goroutine vs Thread:
Goroutines are designed for concurrency, meaning multiple tasks can run using context switching. Threads are designed for parallelism, meaning multiple tasks can run simultaneously on multiple CPU cores.

Goroutines have a dynamic stack size and are managed by the Go runtime. Threads have a fixed-size stack and are managed by the OS kernel.

### What is Closure in golang:
A closure is a special type of anonymous function that can use variables, that declared outside of the function. Closures treat functions as values, allowing us to assign functions to variables, pass functions as arguments, and return functions from other functions. 

```go
v:= func (f func (i int) int) func()int{
    c:=f(3)
    return func()int{
        c++
        return c
    }
}
f:=v()// v() returns a function address
f()// call the function which v() returns
```

### Interfaces in golang:
Interfaces allow us to define contracts, which are abstract methods, have no body/implementations of the methods.
A Struct which wants to implements the Interface need to write the body of every abstract methods the interface holds.
We can compose interfaces together.
An empty interface can hold any type of values.
name.(type) give us the Type the interface will hold at runtime. or we can use reflect.TypeOf(name)
```go
func ty(i interface{}) {
	switch i.(type) {
	case int:
		fmt.Println("Integer")
	default:
		fmt.Println("No idea")
	}
	fmt.Println(reflect.TypeOf(i))
}
func main() {
	ty(67.89)
}
```

### Panic Defer Recover combo:
panic is use to cause a Runtime Error and Stop the execution.
When a function return or panicking then Defer blocks are called according to Last in First out manner, the last defer will execute first.
Recover is use to regain the execution from a panicking situation and handle it properly then stop execution. Recover is useful for close any connection like db and websockets etc.
```go
func div(num int) int {
	if num == 0 {
		panic("Not divisible by 0")
	} else {
		return 27 / num
	}
}
func rec() {
	r := recover()
	if r != nil {
		fmt.Println("I am recovering from Panic")
		fmt.Println("I am Fine Now")
	}
}
func main() {
	defer rec()
	fmt.Println(div(0))
	fmt.Println("Main Regained") // Will not executed if divisble by 0
}
```

### Array vs Slice: 
Array can not Grow and Shrink dynamically at runtime, Slice can. Slice is just references to an existing array of a fixed length.

### Method Dispatching:
golang use Receiver function for method dispatching and has 2 way to dispatch methods at runtime.

Pointer receiver function: As obj is refrence of the Struct so any modification inside the function will affect the original Struct. More memory-efficient and can result in faster execution, especially for large structs.
```go
func (obj *class_name)method_name(argument int) (returns_name bool){
    //body
}
```
Value receiver function: As obj is copy of the Struct so any modification inside the function will not affect the original Struct. 
```go
func (obj class_name)method_name(argument int) (returns_name bool){
    //body
}
```


### Concurency Primitives:
Concurency Primitives are tools that are provided by any programming languages to handle execution behaviors of Concurent tasks.

In golang we have Mutex, Semaphore, Channels as concurency primitives.

Mutex is used to protect shared resources from being accessed by multiple threads simultaneously.

Semaphore is used to protect shared pool of resources from being accessed by multiple threads simultaneously. Semaphore is a Counter which start from Number of Reosurces. When one thread using the reosurces Semaphore decremented by 1. If semaphore value is 0 then thread will wait untils its value greater than 0. When one thread done with the resources then Semaphore incremented by 1.

Channel is used to communicate via sending and receiving data and provide synchronisation between multiple gorountines. If channel have a value then execution blocked until reader reads from the channel.
Channel can be buffered, allowing goroutines to send multiple values without blocking until the buffer is full. 

Waitgroup is used when we want the function should wait until goroutines complete its task.
Waitgroup has Add() function which increments the wait-counter for each goroutine.
Wait() is used for wait until wait-counter became zero.
Done() decrement wait-counter and it called when goroutine complete its task.


### Map Synchronisation:
In golang if multiple goroutines try to acess map at same time, then the operations leads to Panic for RACE or DEADLOCK (fatal error: concurrent map read and map write).
So we need proper codes for handeling Map.
We use MUTEX for LOCK and UNLOCK the Map operations like Read and Write. 
```go
func producer(m *map[int]string, wg *sync.WaitGroup, mu *sync.RWMutex) {
	vm := *m
	for i := 0; i < 5; i++ {
		mu.Lock()
		vm[i] = fmt.Sprint("$", i)
		mu.Unlock()
	}
	m = &vm
	wg.Done()
}
func consumer(m *map[int]string, wg *sync.WaitGroup, mu *sync.RWMutex) {
	vm := *m
	for i := 0; i < 5; i++ {
		mu.RLock()
		fmt.Println(vm[i])
		mu.RUnlock()
	}
	wg.Done()
}
func main() {
	m := make(map[int]string)
	m[0] = "1234"
	m[3] = "2345"
	wg := sync.WaitGroup{}
	mu := sync.RWMutex{}
	for i := 0; i < 5; i++ {
		wg.Add(2)
		go producer(&m, &wg, &mu)
		go consumer(&m, &wg, &mu)
	}
	wg.Wait()
}
```


### Describe Channel comunication

```go
package main

import (
	"fmt"
	"sync"
)

func print(wg *sync.WaitGroup) {
	defer wg.Done() // Decrement the counter when the goroutine completes
	fmt.Println("msg")
}

func main() {
	wg := sync.WaitGroup{}
	wg.Add(1)     // Increment the counter for the goroutine
	go print(&wg) // Start the goroutine
	wg.Wait()     // Wait for the goroutine to finish
}
```

```go
func producer(ch chan<-int){ //ch <- value // Sends value into channel ch
	for i:=0;i<5;i++{
		ch<-i
	}
	close(ch)
}
func consumer(ch <-chan int){ //value := <-ch // Receives from channel ch and assigns it to value
	for n:=range ch{
		fmt.Print("RECV: ",num)
	}
}
for main(){
	ch:=make(chan int)
	go producer(ch)
	consumer(ch)
}
```
### Describe Channel comunication with task distributions:
Lets imagine we have a number n, we have to find 0 to n numbers are prime or not.
```go
func isPrime(n int) bool {
	if n <= 1 {
		return false
	}
	for i := 2; i < n; i++ {
		if n%i == 0 {
			return false
		}
	}
	return true
}
func primeHelper(a []int, ch chan<- map[int]bool, wg *sync.WaitGroup) {
	time.Sleep(time.Second)
	defer wg.Done()
	m := make(map[int]bool)
	for i := range a {
		m[a[i]] = isPrime(a[i])
	}
	ch <- m
}
func main() {
	startTime := time.Now()
	var wg sync.WaitGroup
	n := 12
	arr := []int{}
	for i := 0; i < n; i++ {
		arr = append(arr, i)
	}
	length := len(arr)
	goroutines := 4
	part := length / goroutines
	ch := make(chan map[int]bool, goroutines)
	ma := make(map[int]bool)
	for i := 0; i < goroutines; i++ {
		wg.Add(1)
		s := i * part
		e := s + part
		if e > length {
			e = length
		}
		go primeHelper(arr[s:e], ch, &wg)
	}
	wg.Wait()
	close(ch)
	for i := range ch {
		for k, v := range i {
			ma[k] = v
		}
	}
	fmt.Println(ma)
	fmt.Println("Time Taken: ", time.Since(startTime))
}
```

### Select Statement:
Assume a development scenerio where we have 3 s3 Buckets. We spawn 3 GO-Routines each one uploading a File on each S3 bucket at same time. We have to Return SignedUrl of the file so user can stream the File as soon as possible. Now we do not have to wait for 3 S3 Upload operation, when one s3 upload done we can send the SignedUrl of the File to the User so he can Stream. And Other two S3 Upload will continue at same time. This is the Scenerio when Select Statement can help.

Select statement is used for Concurency comunication between multiple goroutines. Select have multiple Case statement related to channel operations. Select block the execution unitl one of its case return. If multiple case returns at same time, then one random case is selected for returns. If no case is ready and there's a default case, it executes immediately. If there's no default case, select blocks until at least one case is ready.
```go
func work(ctx context.Context, ch chan<- string) {
	rand.NewSource(time.Now().Unix())
	r := rand.Intn(6)
	t1 := time.Duration(r) * time.Second
	ctx, cancel := context.WithTimeout(ctx, t1)
	defer cancel()
	select {
	case <-time.After(t1):
		ch <- "Connection established"
	case <-ctx.Done():
		ch <- "Context Expired"
	}
}

func main() {
	ch1 := make(chan string)
	ch2 := make(chan string)
	go work(context.Background(), ch1)
	go work(context.Background(), ch2)
	select {
	case res := <-ch1:
		fmt.Println("ch1 ", res)
	case res := <-ch2:
		fmt.Println("ch2 ", res)
	}
}
```

```go
package main

import (
	"fmt"
	"sync"
)

func main() {
	// Create two channels, one for even numbers and one for odd numbers
	evenCh := make(chan int)
	oddCh := make(chan int)

	var wg sync.WaitGroup

	// Goroutine to send even numbers up to 30
	wg.Add(1)
	go func() {
		defer wg.Done()
		for i := 0; i <= 30; i++ {
			if i%2 == 0 {
				evenCh <- i
			}
		}
		close(evenCh)
	}()

	// Goroutine to send odd numbers up to 30
	wg.Add(1)
	go func() {
		defer wg.Done()
		for i := 1; i <= 30; i++ {
			if i%2 != 0 {
				oddCh <- i
			}
		}
		close(oddCh)
	}()

	// Alternately print even and odd numbers until both channels are closed
	go func() {
		for { 
			// This loop keeps running indefinitely (for {}), alternating between printing even and odd numbers, until both channels are closed and drained.
			select {
			case even, ok := <-evenCh:
				if ok {
					fmt.Println("Even:", even)
				}
			case odd, ok := <-oddCh:
				if ok {
					fmt.Println("Odd:", odd)
				}
			}
		}
	}()

	// Wait for all goroutines to finish
	wg.Wait()
}

```
Two goroutines generate even and odd numbers up to 30 and send them through their respective channels (evenCh and oddCh).
The third goroutine prints numbers alternately from these channels, ensuring the sequence.
The sync.WaitGroup ensures that the program waits for all goroutines to finish before exiting.

### SOLID Principles:
SOLID priciples are guidelines for designing Code base that are easy to understand maintain and extend over time.

Single Responsibility:- A Struct/Class should have only a single reason to change. Fields of Author shoud not placed inside Book Struct.
```go
type Book struct{
  ISIN string
  Name String
  AuthorID string
}
type Author struct{
  ID string
  Name String
}
```
Assume One Author decided later, he does not want to Disclose its Real Name to Spread. So we can Serve Frontend by Alias instead of Real Name. Without Changing Book Class/Struct, we can add Alias in Author Struct. By that, Existing Authors present in DB will not be affected as Frontend will Change Name only when it Founds that - Alias field is not empty.
```go
type Book struct{
  ISIN string
  Name String
  AuthorID string
}
type Author struct{
  ID string
  Name String
  Alias String
}

```
Open Close:- Struct and Functions should be open for Extension but closed for modifications. New functionality to be added without changing existing Code.
```go
type Shape interface{
	Area() float64
}
type Rectangle struct{
	W float64
	H float64
}
type Circle struct{
	R float64
}
```
Now we want to Calculate Area of Rectangle and Circle, so Rectangle and Circle both can Implements Shape Interface by Write Body of the Area() Function.
```go
func (r Rectangle) Area()float64{
	return r.W * r.H
}
func (c Circle)Area()float64{
	return 3.14 * c.R * c.R
}
```
Now we can create a Function PrintArea() which take Shape as Arguments and Calculate Area of that Shape. So here Shape can be Rectangle, Circle. In Future we can add Triangle Struct which implements Shape interface by writing Body of Area. Now Traingle can be passed to PrintArea() with out modifing the PrintArea() Function.
```go
func PrintArea(shape Shape) {
	fmt.Printf("Area of the shape: %f\n", shape.Area())
}

// In Future
type Triangle struct{
	B float64
	H float54
}
func (t Triangle)Area()float64{
	return 1/2 * t.B * t.H
}

func main(){
	rect:= Rectangle{W:5,H:3}
	cir:=Circle{R:3}
	PrintArea(rect)
	PrintArea(cir)
	// In Future
	tri:=Triangle{B:4,H:8}
	PrintArea(tri)
}
```
Liskov Substitution:- Super class Object can be replaced by Child Class object without affecting the correctness of the program.
```go
type Bird interface{
	Fly() string
}
type Sparrow struct{
	Name string
}
type Penguin struct{
	Name string
}
```
Sparrow and Pengin both are Bird, But Sparrow can Fly, Penguin Not. ShowFly() function take argument of Bird type and call Fly() function. Now as Penguin and Sparrow both are types of Bird, they should be passed as Bird within ShowFly() function.
```go
func (s Sparrow) Fly() string{
	return "Sparrow is Flying"
}
func (p Penguin) Fly() string{
	return "Penguin Can Not Fly"
}

func ShowFly(b Bird){
	fmt.Println(b.Fly())
}
func main() {
	sparrow := Sparrow{Name: "Sparrow"}
	penguin := Penguin{Name: "Penguin"}
  // SuperClass is Bird,  Sparrow, Penguin are the SubClass
	ShowFly(sparrow)
	ShowFly(penguin)
}
```
Interface Segregation:- A class should not be forced to implements interfaces which are not required for the class. Do not couple multiple interfaces together if not necessary then. 
```go
// The Printer interface defines a contract for printers with a Print method.
type Printer interface {
	Print()
}
// The Scanner interface defines a contract for scanners with a Scan method.
type Scanner interface {
	Scan()
}
// The NewTypeOfDevice interface combines Printer and Scanner interfaces for
// New type of devices which can Print and Scan with it new invented Hardware.
type NewTypeOfDevice interface {
	Printer
	Scanner
}
```

Dependecy Inversion:- Class should depends on the Interfaces not the implementations of methods.

```go
// The MessageSender interface defines a contract for 
//sending messages with a SendMessage method.
type MessageSender interface {
	SendMessage(msg string) error
}
// EmailSender and SMSClient structs implement 
//the MessageSender interface with their respective SendMessage methods.
type EmailSender struct{}

func (es EmailSender) SendMessage(msg string) error {
	fmt.Println("Sending email:", msg)
	return nil
}
type SMSClient struct{}

func (sc SMSClient) SendMessage(msg string) error {
	fmt.Println("Sending SMS:", msg)
	return nil
}
type NotificationService struct {
	Sender MessageSender
}
```
The NotificationService struct depends on MessageSender interface, not on concrete implementations (EmailSender or SMSClient). This adheres to Dependency Inversion, because high-level modules (NotificationService) depend on abstractions (MessageSender) rather than details.
```go
func (ns NotificationService) SendNotification(msg string) error {
	return ns.Sender.SendMessage(msg)
}
func main() {
	emailSender := EmailSender{}

	emailNotification := NotificationService{Sender: emailSender}

	emailNotification.SendNotification("Hello, this is an email notification!")
}
```

### Create Post and Get APIs:
```go
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
	"net/url"

	"github.com/gorilla/mux"
)

// ---------- Transport -----------

type httpTransport struct {
	Service // Interfaces use for Dependency Inversion
}

func NewHttpTransport(s Service) *httpTransport {
	return &httpTransport{
		Service: s,
	}
}

type AddReq struct {
}
type AddRes struct {
	Success bool `json:"success"`
}
type GetReq struct {
	Id string `json:"id"`
}
type GetUrlReq struct {
	Id string `url:"id"`
}
type GetRes struct {
	Count   int  `json:"Count"`
	Success bool `json:"success"`
}

func (t *httpTransport) Add(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	t.AddCounter()
	w.WriteHeader(http.StatusOK)
	json.NewEncoder(w).Encode(AddRes{Success: true})
}
func (t *httpTransport) Get(w http.ResponseWriter, r *http.Request) {
	var req GetReq
	json.NewDecoder(r.Body).Decode(&req)
	count := t.GetCounter(req.Id)
	json.NewEncoder(w).Encode(GetRes{Count: count, Success: true})
}
func (t *httpTransport) GetUrl(w http.ResponseWriter, r *http.Request) {
	u, err := url.ParseQuery(r.URL.RawQuery)
	if err != nil {
		json.NewEncoder(w).Encode(GetRes{Count: -1, Success: false})
	}
	id := u["id"][0]
	count := t.GetCounter(id)
	json.NewEncoder(w).Encode(GetRes{Count: count, Success: true})
}

// ---------- Domain -----------
type Counter struct {
	Count int
}

// ---------- Service -----------
type Service interface {
	AddCounter()
	GetCounter(id string) int
}
type service struct {
	Counter Counter
}

func NewService(c Counter) *service {
	return &service{Counter: c}
}
func (s *service) AddCounter() {
	s.Counter.Count++
}
func (s *service) GetCounter(id string) int {
	fmt.Println(id)
	return s.Counter.Count
}

// ---------- Main -----------
func main() {
	// Service
	s := NewService(Counter{})
	// Trnasport
	t := NewHttpTransport(s)
	// Routing
	r := mux.NewRouter()
	r.HandleFunc("/api/add", t.Add).Methods("POST")
	r.HandleFunc("/api/get", t.Get).Methods("GET")
	r.HandleFunc("/api/geturl", t.GetUrl).Methods("GET")
	// Server
	http.ListenAndServe(":3000", r)
}
```

### Mux Middleware
Middleware functions can be added to the Gin router for processing requests before they reach your handler functions. This is useful for logging, authentication, and other cross-cutting concerns.
Example:

```go
package middlewares

import (
	"fmt"
	"net/http"
	"time"

	"github.com/dgrijalva/jwt-go"
)

// Secret key for JWT
var secretKey = []byte("007jamesbond")

// Generate JWT Token
func GenerateJWT(username string, roles []string) (string, error) {
	// Set token claims
	claims := jwt.MapClaims{
		"roles":    roles,
		"username": username,
		"exp":      time.Now().Add(time.Hour * 24).Unix(), // Token expires in 24 hours
	}

	// Create token
	token := jwt.NewWithClaims(jwt.SigningMethodHS256, claims)

	// Sign the token with the secret key
	return token.SignedString(secretKey)
}

// Middleware to validate JWT token
func AuthMiddleware(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		// Get token from Authorization header
		authHeader := r.Header.Get("Authorization")
		if authHeader == "" {
			http.Error(w, "Missing Authorization Header", http.StatusUnauthorized)
			return
		}

		// Extract token (assumes the header is in the form "Bearer <token>")
		tokenString := authHeader[len("Bearer "):]

		// Parse the token
		token, err := jwt.Parse(tokenString, func(token *jwt.Token) (interface{}, error) {
			// Validate the signing method (it must be HS256 in this case)
			if _, ok := token.Method.(*jwt.SigningMethodHMAC); !ok {
				return nil, fmt.Errorf("unexpected signing method: %v", token.Header["alg"])
			}
			return secretKey, nil
		})

		// If there is an error or the token is invalid, return Unauthorized
		if err != nil || !token.Valid {
			http.Error(w, "invalid Token", http.StatusUnauthorized)
			return
		}

		// Token is valid, continue to the next handler
		next.ServeHTTP(w, r)
	})
}



```
```go
r := mux.NewRouter()
// Protected endpoint (requires token)
r.Handle("/protected", AuthMiddleware(http.HandlerFunc(protectedEndpoint))).Methods("GET")
```



```go
package middlewares

import (
	"log"
	"net/http"
	"time"
)

// responseRecorder is a custom ResponseWriter to capture status codes
type responseRecorder struct {
	http.ResponseWriter
	statusCode int
}

// WriteHeader captures the status code to log it
func (rr *responseRecorder) WriteHeader(statusCode int) {
	rr.statusCode = statusCode
	rr.ResponseWriter.WriteHeader(statusCode)
}

func LogMiddleware(next http.Handler) http.Handler {
	return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		// Record the start time
		start := time.Now()

		// Create a custom response writer to capture the status code
		rr := &responseRecorder{ResponseWriter: w, statusCode: http.StatusOK}

		// Call the next handler (it could be your protected endpoint or any other)
		next.ServeHTTP(rr, r)

		// Log the request details
		duration := time.Since(start)
		log.Printf("Method: %s, URL: %s, Status: %d, Duration: %s", r.Method, r.URL.Path, rr.statusCode, duration)
	})
}

```
```go
r := mux.NewRouter()
// Wrap the routes with the logging middleware
r.Use(LogMiddleware)
```

### GIN Framework

Choose Gin if you need a high-performance framework with built-in features, ease of use, and a rich set of functionalities, making it ideal for building APIs and web applications quickly.
Choose Gorilla Mux if you prefer a flexible routing library that allows for more manual control over your application’s architecture and routing logic, especially for larger projects where complex routing patterns are required.

1. Routing
Gin uses a powerful router to handle HTTP requests. You define routes using gin.Default() or gin.New(), allowing you to specify the HTTP method and the path.
Example:
```go
router := gin.Default()
router.GET("/ping", func(c *gin.Context) {
    c.JSON(200, gin.H{"message": "pong"})
})
```
2. Middleware


```go
package main

import (
    "github.com/gin-gonic/gin"
    "net/http"
)

// Logging Middleware
func Logger() gin.HandlerFunc {
    return func(c *gin.Context) {
        // Before request
        log := "Request: " + c.Request.Method + " " + c.Request.URL.String()
        c.Set("log", log) // Store log in context

        // Process request
        c.Next() // Call the next middleware/handler

        // After request
        log += " | Status: " + http.StatusText(c.Writer.Status())
        println(log) // Print the log to console
    }
}

// Authentication Middleware
func AuthMiddleware() gin.HandlerFunc {
    return func(c *gin.Context) {
        token := c.Request.Header.Get("Authorization")
        if token == "" {
            c.JSON(http.StatusUnauthorized, gin.H{"error": "Unauthorized"})
            c.Abort() // Stop the request
            return
        }
        // Assume token is valid
        c.Next() // Proceed to the next middleware or handler
    }
}

// Example Handler
func serviceHandler(c *gin.Context) {
    log := c.MustGet("log").(string) // Retrieve the log from context
    c.JSON(http.StatusOK, gin.H{"message": "Access granted", "log": log})
}

func main() {
    router := gin.Default()

    // Apply multiple middleware functions to a route
    router.GET("/service", Logger(), AuthMiddleware(), serviceHandler)

    router.Run(":8080")
}
```

3. Context
Each request is processed using a Context object, which contains methods and properties for handling request and response data. It provides access to parameters, query strings, and more.
Example:
```go

name := c.Param("name") // Access route parameters
c.JSON(200, gin.H{"name": name})
```
4. JSON Handling
Gin makes it easy to work with JSON. You can bind incoming JSON requests to structs and send JSON responses with built-in methods.
Example:
```go

var jsonData MyStruct
if err := c.ShouldBindJSON(&jsonData); err == nil {
    c.JSON(200, jsonData)
}
```
5. Error Handling
Gin provides built-in error handling. You can use the c.Error method to log errors and handle them gracefully in your application.
Example:
```go

if err != nil {
    c.Error(err) // Log and handle error
    return
}
```


## RabbitMQ Simplified Overview

## 1. What is RabbitMQ?
RabbitMQ is a tool that helps different programs (called "producers" and "consumers") talk to each other by sending messages. It acts as a middleman that stores messages and makes sure they are delivered reliably.

## 2. Core Concepts
- **Producer**: A program that sends messages to RabbitMQ.
- **Consumer**: A program that receives messages from RabbitMQ.
- **Queue**: A line where messages wait until they're picked up by consumers.
- **Exchange**: Decides where to send messages (to a queue) based on certain rules.
- **Binding**: The connection between a queue and an exchange.
- **Routing Key**: A label used by exchanges to decide how to send messages to queues.
- **Virtual Hosts (vhosts)**: Like separate workspaces in RabbitMQ, keeping things organized.
- **Message**: The actual data that is sent between producers and consumers.

## 3. Types of Exchanges
- **Direct Exchange**: Sends messages to a specific queue based on a routing key.
- **Fanout Exchange**: Sends messages to all queues it is connected to, no matter the routing key.
- **Topic Exchange**: Sends messages to queues based on matching parts of the routing key.
- **Headers Exchange**: Routes messages based on headers (metadata) rather than routing keys.

## 4. Types of Queues
- **Durable Queue**: Survives server restarts, messages are not lost.
- **Transient Queue**: Does not survive a server restart.
- **Exclusive Queue**: Only used by one consumer and deleted when that consumer disconnects.
- **Auto-Delete Queue**: Deletes itself when no consumers are using it.

## 5. Message Acknowledgement
- **Manual Acknowledgement**: The consumer confirms it has received and processed a message.
- **Automatic Acknowledgement**: The message is automatically confirmed once sent to the consumer.
- **Negative Acknowledgement (Nack)**: When a message is rejected by a consumer, RabbitMQ can retry or discard it.
- **Dead Letter Queues**: Special queues for storing messages that can't be delivered (e.g., after too many retries).



## 6. Clustering and High Availability
- **Clustering**: Running RabbitMQ on multiple servers to spread the load and ensure it's always available.
- **Mirrored Queues**: Copying queues to other servers in the cluster so that if one server fails, messages are still available.
- **Federation**: Allowing RabbitMQ instances in different locations to share messages.


## 7. Performance Tuning
- **Prefetch Count**: Limit how many messages a consumer can process at once to avoid overwhelming it.
- **Concurrency**: Running many consumers in parallel to handle more messages.
- **Flow Control**: Managing how messages are processed to avoid overloading RabbitMQ.
- **Memory and Disk Usage**: Keep track of resource usage to prevent performance issues.


##  Example
```go
package main

import (
	"fmt"
	"log"

	"github.com/streadway/amqp"
)

func main() {
	conn, err := amqp.Dial("amqp://guest:guest@localhost:5672/")
	if err != nil {
		log.Fatalf("Failed to connect: %s", err)
	}
	defer conn.Close()

	ch, err := conn.Channel()
	if err != nil {
		log.Fatalf("Failed to create channel: %s", err)
	}
	defer ch.Close()

	exchange := "topic_logs"
	ch.ExchangeDeclare(exchange, "topic", true, false, false, false, nil)

	routingKey := "animal.cat"
	message := "Topic exchange message for cat"
	err = ch.Publish(exchange, routingKey, false, false, amqp.Publishing{
		ContentType: "text/plain",
		Body:        []byte(message),
	})
	if err != nil {
		log.Fatalf("Failed to send message: %s", err)
	}
	fmt.Println("Message sent:", message)
}

```

```go
package main

import (
	"fmt"
	"log"

	"github.com/streadway/amqp"
)

func main() {
	conn, err := amqp.Dial("amqp://guest:guest@localhost:5672/")
	if err != nil {
		log.Fatalf("Failed to connect: %s", err)
	}
	defer conn.Close()

	ch, err := conn.Channel()
	if err != nil {
		log.Fatalf("Failed to create channel: %s", err)
	}
	defer ch.Close()

	exchange := "topic_logs"
	ch.ExchangeDeclare(exchange, "topic", true, false, false, false, nil)

	queue, err := ch.QueueDeclare("", false, true, true, false, nil)
	if err != nil {
		log.Fatalf("Failed to declare queue: %s", err)
	}

	routingKey := "animal.*"
	err = ch.QueueBind(queue.Name, routingKey, exchange, false, nil)
	if err != nil {
		log.Fatalf("Failed to bind queue: %s", err)
	}

	msgs, err := ch.Consume(queue.Name, "", true, false, false, false, nil)
	if err != nil {
		log.Fatalf("Failed to consume messages: %s", err)
	}

	for msg := range msgs {
		fmt.Printf("Received message: %s\n", msg.Body)
	}
}

```
Direct Exchange
In Direct Exchange, messages are routed to queues based on an exact match between the routing key in the message and the binding key in the queue.

Publisher (Direct Exchange):
Exchange Type: "direct"
Routing Key: The publisher sends a message with a specific routing key (e.g., "error"), which is used to determine which queues receive the message.
```go
// Declare direct exchange
ch.ExchangeDeclare("direct_logs", "direct", true, false, false, false, nil)

// Publish a message with a routing key (e.g., "error")
err = ch.Publish("direct_logs", "error", false, false, amqp.Publishing{
    ContentType: "text/plain",
    Body:        []byte("Error in processing the task"),
})
```
Subscriber (Direct Exchange):
Binding Key: The subscriber binds a queue to the exchange using the binding key ("error") so it will receive messages published with the same routing key.
```go
// Declare direct exchange
ch.ExchangeDeclare("direct_logs", "direct", true, false, false, false, nil)

// Declare an anonymous queue
queue, err := ch.QueueDeclare("", false, true, true, false, nil)
if err != nil {
    log.Fatalf("Failed to declare queue: %s", err)
}

// Bind the queue to the exchange with the routing key "error"
err = ch.QueueBind(queue.Name, "error", "direct_logs", false, nil)
```
In Fanout Exchange, the message is sent to all queues bound to the exchange, regardless of any routing keys. It broadcasts the message to all subscribers.

Publisher (Fanout Exchange):
Exchange Type: "fanout"
Routing Key: The routing key is ignored in this case. The message is simply sent to all bound queues.
```go
// Declare fanout exchange
ch.ExchangeDeclare("logs", "fanout", true, false, false, false, nil)

// Publish a message (routing key is ignored for fanout)
err = ch.Publish("logs", "", false, false, amqp.Publishing{
    ContentType: "text/plain",
    Body:        []byte("Fanout exchange message"),
})
```
Subscriber (Fanout Exchange):
Binding Key: Not needed because all queues bound to the fanout exchange receive the message. The subscriber simply binds to the exchange without a specific routing key.
```go
// Declare fanout exchange
ch.ExchangeDeclare("logs", "fanout", true, false, false, false, nil)

// Declare an anonymous queue
queue, err := ch.QueueDeclare("", false, true, true, false, nil)
if err != nil {
    log.Fatalf("Failed to declare queue: %s", err)
}

// Bind the queue to the exchange (routing key is ignored for fanout)
err = ch.QueueBind(queue.Name, "", "logs", false, nil)
```
 Topic Exchange
In Topic Exchange, messages are routed to queues based on the routing pattern specified by the routing key. The routing key can include wildcards (* for a single word and # for multiple words).

Publisher (Topic Exchange):
Exchange Type: "topic"
Routing Key: The routing key can include wildcard patterns to route messages to multiple queues that match the pattern.
```go
// Declare topic exchange
ch.ExchangeDeclare("topic_logs", "topic", true, false, false, false, nil)

// Publish a message with a routing key (e.g., "animal.cat")
err = ch.Publish("topic_logs", "animal.cat", false, false, amqp.Publishing{
    ContentType: "text/plain",
    Body:        []byte("Topic exchange message for cat"),
})
```
Subscriber (Topic Exchange):
Binding Key: The subscriber binds to the exchange with a pattern-based routing key (e.g., animal.*), which means it will receive messages with routing keys like animal.cat, animal.dog, etc.
```go
// Declare topic exchange
ch.ExchangeDeclare("topic_logs", "topic", true, false, false, false, nil)

// Declare an anonymous queue
queue, err := ch.QueueDeclare("", false, true, true, false, nil)
if err != nil {
    log.Fatalf("Failed to declare queue: %s", err)
}

// Bind the queue to the exchange with a wildcard routing key (e.g., "animal.*")
err = ch.QueueBind(queue.Name, "animal.*", "topic_logs", false, nil)
```
 Headers Exchange
In Header Exchange, messages are routed based on message headers rather than the routing key. The routing decisions are made based on specific header values (e.g., X-Color: Red).

Publisher (Header Exchange):
Exchange Type: "headers"
Headers: The publisher sends the message with header attributes (e.g., X-Color: Red)
```go
// Declare header exchange
ch.ExchangeDeclare("header_logs", "headers", true, false, false, false, nil)

// Define message headers
headers := amqp.Table{
    "X-Color": "Red",  // Set a header key-value pair
}

// Publish a message with headers
err = ch.Publish("header_logs", "", false, false, amqp.Publishing{
    Headers:     headers,
    ContentType: "text/plain",
    Body:        []byte("Header exchange message with color Red"),
})
```
Subscriber (Header Exchange):
Binding Key: Instead of a routing key, the subscriber binds the queue using header matching. In this case, the subscriber binds the queue to the exchange with specific headers (e.g., X-Color: Red).

```go
// Declare header exchange
ch.ExchangeDeclare("header_logs", "headers", true, false, false, false, nil)

// Declare an anonymous queue
queue, err := ch.QueueDeclare("", false, true, true, false, nil)
if err != nil {
    log.Fatalf("Failed to declare queue: %s", err)
}

// Bind the queue using header matching (e.g., "X-Color" equals "Red")
headers := amqp.Table{
    "X-Color": "Red",  // Match this header for routing
}
err = ch.QueueBind(queue.Name, "", "header_logs", false, headers)

```




## GRPC
- gRPC uses HTTP/2 and binary serialization (Protocol Buffers) for high performance and efficiency, It supports bi-directional streaming.
- REST relies on HTTP/1.1 and text-based formats like JSON, offering simplicity and ease of use for web applications. REST is stateless and leverages standard HTTP methods, making it widely adopted and easy to debug. 
- Choose gRPC if you need high performance, efficient binary serialization, and streaming capabilities, especially in microservices.
- Choose REST if you prefer simplicity, human readability, and a stateless architecture that is widely supported.


```proto
syntax = "proto3";

package chat;

service Chat {

  rpc ServerStream (Message) returns (stream Message);


  rpc ClientStream (stream Message) returns (Message);


  rpc StreamChat (stream Message) returns (stream Message);
}


message Message {
  string sender = 1;
  string content = 2;
}

```
- The Chat service contains three RPC methods.
- The Message message type contains two fields: sender (to indicate who sent the message) and content (the message text).

To generate the Go code from this .proto file, use the following command:
```bash
protoc --go_out=. --go-grpc_out=. chat.proto
```
```go
package main

import (
    "io"
    "log"
    "net"
    "time"

    "golang.org/x/net/context"
    "google.golang.org/grpc"
    pb "path/to/your/chat" // Adjust the import path
)

// Server struct
type server struct {
    pb.UnimplementedChatServer
}

// Server-side streaming method
func (s *server) ServerStream(req *pb.Message, stream pb.Chat_ServerStreamServer) error {
    for i := 0; i < 5; i++ {
        stream.Send(&pb.Message{Sender: "Server", Content: req.Content + " " + time.Now().String()})
        time.Sleep(time.Second)
    }
    return nil
}

// Client-side streaming method
func (s *server) ClientStream(stream pb.Chat_ClientStreamServer) error {
    var messages []string
    for {
        msg, err := stream.Recv()
        if err == io.EOF {
            break
        }
        messages = append(messages, msg.Content)
    }
    stream.SendAndClose(&pb.Message{Sender: "Server", Content: "Received: " + fmt.Sprint(messages)})
    return nil
}

// Bidirectional streaming method
func (s *server) StreamChat(stream pb.Chat_StreamChatServer) error {
    for {
        msg, err := stream.Recv()
        if err == io.EOF {
            break
        }
        stream.Send(&pb.Message{Sender: "Server", Content: "Echo: " + msg.Content})
    }
    return nil
}

func main() {
    lis, _ := net.Listen("tcp", ":50051")
    s := grpc.NewServer()
    pb.RegisterChatServer(s, &server{})
    go s.Serve(lis)

    conn, _ := grpc.Dial("localhost:50051", grpc.WithInsecure())
    client := pb.NewChatClient(conn)

    // Client-side streaming
    clientStream, _ := client.ClientStream(context.Background())
    for i := 0; i < 3; i++ {
        clientStream.Send(&pb.Message{Content: "Client message " + fmt.Sprint(i)})
    }
    clientStream.CloseSend()

    // Server-side streaming
    serverStream, _ := client.ServerStream(context.Background(), &pb.Message{Content: "Hello!"})
    for {
        msg, err := serverStream.Recv()
        if err != nil {
            break
        }
        log.Println(msg.Content)
    }

    // Bidirectional streaming
    bidiStream, _ := client.StreamChat(context.Background())
    go func() {
        for i := 0; i < 3; i++ {
            bidiStream.Send(&pb.Message{Content: "Bidirectional message " + fmt.Sprint(i)})
            time.Sleep(time.Second)
        }
        bidiStream.CloseSend()
    }()
    for {
        msg, err := bidiStream.Recv()
        if err != nil {
            break
        }
        log.Println(msg.Content)
    }
}
```
Summary of Steps
- Define the Server: A server struct implements the ChatServer interface, with three methods for server-side streaming, client-side streaming, and bidirectional streaming.
- Implement Streaming Methods: The ServerStream method sends multiple messages back to the client; the ClientStream method collects messages from the client and sends a summary; and StreamChat handles both incoming and outgoing messages simultaneously.
- Set Up the gRPC Server: The main function creates a listener on port 50051, registers the server, and starts serving in a separate goroutine.
- Create and Use a gRPC Client: The client connects to the server and demonstrates client-side streaming by sending messages, server-side streaming by receiving multiple messages, and bidirectional streaming in a separate goroutine.
- Run the Server and Client: The entire setup allows for real-time message exchange, showcasing the flexibility of gRPC for various streaming patterns within a single file.


## Kubernetes 
Kubernetes is designed for automate the process of deploying, scaling, and managing containerized applications.  Kubernetes uses YAML files to define resources.

A Pod can contain one or more containers that share the same network, namespace and storage.
Containers in the same Pod share a common IP address and port space. They can communicate with each other using localhost and the same port numbers. Pods can communicate with each other using their IP addresses and defined ports. Pods are often managed by higher-level controllers like Deployments, ReplicaSets, which handle scaling, updates, and ensuring that the desired number of Pod replicas are running.

ReplicaSet is a controller that ensures a specified number of identical Pods are running at any given time.   If a Pod fails or is deleted, the ReplicaSet creates a new Pod to replace it. A ReplicaSet uses a label selector to identify which Pods it should manage. The selector matches Pods based on their labels, and the ReplicaSet ensures that the Pods with these labels are created or deleted as needed.

Services provide a stable endpoint(DNS name and IP address) for accessing a set of Pods. This stable endpoint is crucial because Pods can come and go due to scaling, updates, or failures, but Services provide a consistent way to access these Pods.

Kubernetes provides built-in mechanisms for service discovery, so applications can find and communicate with other services without hardcoding IP addresses.

Types of Services:

ClusterIP : The Service is only accessible within the Kubernetes cluster. It’s used for communication between different services within the cluster.

NodePort : This allows the Service to be accessed from outside the cluster by requesting <NodeIP>:<NodePort>. This type is often used for simple testing and debugging.

LoadBalancer : Creates an external load balancer (e.g., from cloud providers like AWS, GCP, Azure) and assigns a public IP to the Service. This allows the Service to be accessed from outside the cluster using that public IP. It’s often used in production environments.

Headless Service : When you don’t need load balancing or a cluster IP, you can create a headless Service by setting the clusterIP field to None. This allows direct access to the Pods without load balancing, useful for stateful applications.

Services use selectors to determine which Pods belong to the Service. 
selector : Specifies that the Service will route traffic to Pods with the label app: my-app


Deployment is a higher-level abstraction that manages ReplicaSets and Pods. Deployments provide version control and history for your application, making it easy to roll back to previous versions if needed.
Deployments support rolling updates, allowing you to update your application with zero downtime. Kubernetes gradually replaces old Pods with new ones according to the update strategy you specify.
If a new update causes issues, you can roll back to a previous version of your application. Kubernetes maintains a history of revisions, making it easy to revert to a stable state.
Deployments allow you to scale the number of replicas (Pods) up or down easily.


Kubernetes uses a flat network model where every Pod gets its own IP address. Pods communicate directly with each other using their IP addresses, 

Cluster is a set of machines (nodes) that work together to run containerized applications. The cluster consists of a control plane(Master Node) and a set of worker nodes, and it provides the environment needed to deploy, manage, and scale applications.
What are the main components of Kubernetes architecture?
- Master Node: The node that manages the cluster. It includes:

	- API Server: The API server exposes the Kubernetes API which is used by users and other components to interact with the cluster. When we run commands using kubectl or other tools, they communicate with the API Server.  When we deploy a new application, the API Server stores the desired state in etcd and updates the cluster to match this state

	- Controller Manager: Each controller watches the API Server for changes to resources and makes adjustments to ensure that the actual state matches the desired state. For example, if a ReplicaSet specifies that three replicas of a Pod should be running, the controller will create or delete Pods as necessary to meet this requirement.

	- Scheduler: Assigns Pods to Nodes based on resource availability and constraints. if a Pod requires 2 CPU cores and 4 GB of memory, the Scheduler will find a Node with sufficient available resources and assign the Pod to that Node.
	
	- etcd: A distributed key-value store that holds all the configuration data and state of the Kubernetes cluster.  When we make changes to the cluster (e.g., deploying an application or scaling a service), the API Server updates the state in etcd.  This allows Kubernetes to recover from failures by restoring the cluster state from etcd.

- Worker Nodes: worker node refers to a machine (virtual or physical) that runs the applications and workloads in your Kubernetes cluster. On AWS, worker nodes are typically Amazon EC2 instances that are part of your Kubernetes cluster.
Kubernetes Components on Worker Nodes: 
	- Kubelet: An agent that ensures containers are running in Pods.  The Kubelet communicates with the API Server to get the desired state of Pods. It then makes sure that the containers in those Pods are running as expected. If a container fails or crashes, the Kubelet will restart it to maintain the desired state. It also collects and reports metrics about the Node and the Pods running on it.

	- Kube-Proxy: Maintains network rules and load-balances traffic to Pods. Kube-Proxy manages network traffic routing by maintaining iptables or IPVS rules on Nodes. This ensures that network traffic is properly directed to the Pods. For example, if a Service exposes multiple Pods, Kube-Proxy ensures that traffic is distributed evenly across these Pods.

	- Container Runtime: Software that runs and manages containers (e.g., Docker, containerd).

We can scale a cluster by adding or removing worker nodes as needed to handle varying workloads.

AWS provides a managed Kubernetes service called EKS. When you create an EKS cluster, you can specify the EC2 instance types and configurations for your worker nodes.

Elastic Load Balancing (ELB): Kubernetes services that are exposed as LoadBalancer types, can use AWS ELB to provide external access and distribute traffic to the worker nodes.

Amazon EBS: For persistent storage, you can use Amazon Elastic Block Store (EBS) volumes that are attached to worker nodes.

Helm is a package manager for Kubernetes that simplifies the deployment, management, and versioning of applications and services on a Kubernetes cluster.

A Helm chart is a collection of Kubernetes YAML files organized into a directory structure that defines a Kubernetes application. It includes everything needed to run an application, such as deployments, services, ingress configurations, and more.

Helm is installed on your local machine or CI/CD pipeline and communicates with your Kubernetes cluster to deploy and manage applications.

A typical Helm chart directory includes
Chart.yaml: Contains metadata about the chart, such as its name, version, and description.
values.yaml: A file containing default configuration values that can be overridden by the user.
templates/: A directory with Kubernetes manifest templates that Helm will use to generate Kubernetes resources.
charts/: A directory where dependent charts can be stored.
README.md: Documentation about the chart.

Helm can install, upgrade, rollback, and delete releases. Each release can be upgraded or rolled back independently of others.
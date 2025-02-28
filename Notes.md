## Why you left your previous organisation?
I resigned from my previous company to take care of my father's Cancer treatment. After he recovered i join Calsoft where i worked for Extreme Networks for Data Center Automation mainly at Networking domain where we have to maintain and fixes on Firmwares related things of Switch and Router. In previous company i worked on pure Web Backend Developemnts. So this Network Domain is not my preferrence. Thats why I want to change.

## Introduce yourself
I have Btech in IT, after that I joined Sensibol as a Golang Developer. My role was developing Rest APIs Microservices with Golang MongoDB Redis AWS. Get exposers on gRPC, Kubernetes, and Jenkins. Then after 3.3 years I joined Calsoft as a Senior Developement Engineer and i worked for Extreme Networks Client. My role here is Write Bussiness Logics in GoLang and Test them by Unit and Functional test cases and Bug fixses with PostgrSQL , Grpc , GoSwitch library  etc.

Now this Network domain i am not preffering as it is mainly Firmware related things of Routers and Switches.

## What Projects Have You Worked On?
I worked on 
- PDL : A music distribution and royalty management platform.
- Singshala : A platform similar to TikTok but with the added feature of analyzing the audio components of videos and providing rankings based on that analysis.
- XCO : In this project, we create profiles, which are configurations applied to switch ports, and then bind those profiles to the ports.

## Microservices vs Monolith
- **Microservices** are better for large projects where scaling and almost zero downtime are required. Bug fixing and maintaining the codebase are easier. A disadvantage of microservices can be inter-service network calls.
- **Monolith** is suitable for smaller projects but can become difficult to scale or maintain as the application grows.

## Authentication vs Authorization
- Authentication is verifying the identity by username password. Server checks this provided identity.
- Autheorization is granting permission to access or modify any apis or resources.
In authorization we mainly use JWT for Role based authorizarion.

## Golang Garbage Collection
Golang uses automatic garbage collection to manage memory. Developers do not need to allocate or deallocate memory manually, which reduces memory-related errors.

## Pointer
A **pointer** store the memory address of a variable, struct, function, or any data type.
```go
package main

import "fmt"

func main() {  
    // Rupam Ganguly : https://in.linkedin.com/in/hirupamganguly

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
## Goroutine V/S Thread:
Goroutines are designed to work on Concurency, meaning multiple task can run using Context Switching like after completion 2% of Task1 Tas2 can start and after Completion 5% of task Task3 can start and after completion of 6% of it Task 1 can agian resume its work, something like this.

Threads are designed for Paralleslism, meaning Multiple tasks can run simultaneously on multiple CPU cores.

GoRoutine have dynamic Stack size and manged by Go-Runtime. Threads have fixed size stack and managed by OS-Kernel.

## OOPS conecpts in Golang:
Encapsulation:
We use structs to store data and methods (receiver functions) to provide functionality. This allows you to hide the internal details of a struct and expose only the necessary methods to interact with it

Abstraction: Abstraction is the concept of hiding complex implementation details and exposing only the relevant parts to the user. In Go, this is typically done using interfaces. An interface defines a set of methods (behavior) without specifying how those methods should be implemented. Different types can implement the same interface in their own way, allowing you to interact with the behavior without needing to know the underlying implementation.

Polymorphism: Polymorphism allows a single function or method to work with objects of different types, and each type can provide its own implementation of the same behavior. In Go, polymorphism is achieved through interfaces and dynamic dispatch. A single interface can be implemented by multiple types, and the appropriate method is called at runtime based on the concrete type.

Inheritance (via Composition): Go does not support traditional inheritance (as in object-oriented languages like Java or C++). Instead, Go uses composition, where one struct can embed another struct. This allows the embedded struct's fields and methods to be used by the outer struct, providing functionality similar to inheritance. Go encourages composition over inheritance to promote flexibility and reusability.

## Closure in Golang:
Closure in golang treat fuctions as variable. So we can assign function to variables, pass function as arguments and return functions from a function.

```go
func main() {  
    // Rupam Ganguly : https://in.linkedin.com/in/hirupamganguly
	v := func(f func(i int) int) func() int {
		c := f(3)
		return func() int {
			c++
			return c
		}
	}
	f1 := func(i int) int {
		return i * i
	}
	f2 := func(i int) int {
		return i * 2
	}
	g := v(f1) // Make c as 9
	g()        // call the function which v() returns in this example Incremeting with 1
	g()
	g = v(f2) // Make c as 6
	g()       // call the function which v() returns in this example Incremeting with 1
	g()
}
```
## Interface in Golang
Interface is a type that holds abstract methods which are function declaration, definition or implementation will be done by any struct or type. The struct ot type which wants to implements the interface need to write body of every functions declared in the interface.

We can compose interfaces together.

An empty interface can hold any type of value. If we want to know what datatype the interface holding at runtime we use interface-name.(type)
```go
func showType(inf interface{}) {
	switch inf.(type) {
	case int:
		fmt.Println("INT")
	case string:
		fmt.Println("String")
	}
	ty := reflect.TypeOf(inf)
	if ty.Kind() == reflect.Int {
		fmt.Println("reflect.Int")
	}
	if ty.Kind() == reflect.Float64 {
		fmt.Println("reflect.Float64")
	}
	if ty.Kind() == reflect.String {
		fmt.Println("reflect.String ")
	}
}
```
## Panic Defer Recover Combo
Panic is use to cause runtime error for stoping the execution.
When a function return or Panicking then Defer blocks are called according to the Last In First Out manner, the last defer will execute first.
Recover is use to regain the execution from a panicking situation and handle that situation properly before stoping the execution. Recover is useful for close any connection like db or websocket or send Proper API responses etc.

```go
func reco() {
	r := recover()
	if r != nil {
		fmt.Println("Recovering...")
	}
}
func divi(num int) int {
	if num == 0 {
		panic("Not divisible by 0")
	} else {
		return 27 / num
	}
}
func main() {  
    // Rupam Ganguly : https://in.linkedin.com/in/hirupamganguly
	defer reco()
	fmt.Println(divi(0))
	fmt.Println("Done")
}
```
## Array V/S Slice
Array can not grow or shrink at runtime, Slice can.
Slice is just references to an existing array of a fixed lenegth, at runtime it is manulated such a way that we feel it can grow or shrink.

Empty Slice allocate memory. Nil Slice did not allocate memory on Heap.

```go
func main() {  
    // Rupam Ganguly : https://in.linkedin.com/in/hirupamganguly

	var nilSlice []int
	if nilSlice == nil {
		fmt.Println("nilSlice is nil")
	}
	fmt.Println(nilSlice)

	var emptySlice = []int{}
	if emptySlice == nil {
		fmt.Println("emptySlice is Not nil") // This block never execute
	}
	fmt.Println(emptySlice)
}
```
## Typecasting vs Typeconversion
Type conversion refers to explicitly converting a value from one type to another. Go allows explicit type conversions, but only when the two types are compatible. If they are not compatible, you can't convert them directly, and the Go compiler will throw an error.
```go
var i int = 42
var f float64 = float64(i) // Convert int to float64
var str string = string(i) // Compiler error: cannot convert num (type int) to type string
```
In Typecasting the compiler automatically converts a value from one type to another, typically from a smaller type to a larger type or between compatible types, without requiring the programmer to do anything. Golang not support it. As It ensures that you don't accidentally lose data or perform invalid conversions.

## Method Dispatching
Golang use Receiver function for method dispatching and has 2 way to dispatching method at Runtime.
Pointer Receiver Function and Value receiver function.
```go
func (obj *class_name)method_name(argument int) (returns_name bool){
    //body of Pointer Receiver Function
	As obj is refrence of the Struct so any modification inside the function will affect the original Struct. More memory-efficient and can result in faster execution, especially for large structs.
}
func (obj class_name)method_name(argument int) (returns_name bool){
    //body Value receiver function
	As obj is copy of the Struct so any modification inside the function will not affect the original Struct. 
}
```
## Concurency Primitives
Concurency primitives are tools that are provided by any Programming language to handle execution behaviours of concurent tasks.

In golang we have Mutex, Atomic, Semaphore, Channel, WaitGroup as concurency primitives.

Mutex is used to protect shared resources from being accessed by multiple threads simultaneously.

Atomic is low level operation for safely manipulate shared variables between gorutines. Unlike mutexes, atomic operations do not cause goroutines to block while waiting for access to the variable. Instead, atomic operations work by leveraging hardware-level atomic instructions like Compare-And-Swap (CAS) or Test-And-Set. When performance is crucial, and you want to avoid the locking overhead of mutexes then use Atomic.

atomic.AddInt64(&counter, 1) is used to atomically increment the counter. This ensures that the counter is updated safely, even when multiple goroutines are modifying it concurrently

```go
var counter int64

func increment() {
	for i := 0; i < 1000; i++ {
		atomic.AddInt64(&counter, 1) // atomic increment
	}
}

func main() {
	var wg sync.WaitGroup

	wg.Add(2)
	go func() {
		defer wg.Done()
		increment()
	}()
	go func() {
		defer wg.Done()
		increment()
	}()

	wg.Wait()

	fmt.Printf("Final counter value: %d\n", counter)
}
```

```go
var counter int64
atomic.AddInt64(&counter, 1) // Adds 1 to the counter
oldValue := atomic.LoadInt64(&counter)
swapped := atomic.CompareAndSwapInt64(&counter, oldValue, 5) // CAS: if counter == oldValue, set counter to 5
atomic.StoreInt64(&counter, 10) // Atomically stores a value into a variable.
oldValue := atomic.SwapInt64(&counter, 5) // Atomically swaps the value of a variable and returns its old value.
```

Semaphore is a counter which keep track of shared resources count from pool of those resources. This Counter starts from number of resources availabel. When one thread wants to use the resource it decrement the Counter value. When Semaphore Counter became 0 then any Threads want to use the resource have to wait until Counter became greater than 0. When Thread done with the resource it increment the Counter. 

Channel is used to communicate between goroutines via sending and receving data and providing synchronisation also. If channel have value then execution counter blocked until Any reader reads from that channel. Channel can be buffered by sending multiple values without blocking until buffer is full.

Waitgroup is used when we want the Caller function should wait until called goroutines complete its task.
Add() function increments the wait-counter for each goroutine called.
Wait() function use for waiting the caller function until wait-counter became zero.
Done() function is use for decrement the wait-counter and done() called from goroutine itself when it completes its task.

## Map Synchronisation:
In Golang when multiple goroutine try to acess Map at same time then Panic happens for Race or Deadlock.
We can use Mutex for LOCK and UNLOCK map operation like Read and Write.
![Image](https://github.com/user-attachments/assets/b9ad4d4a-0c72-4bf7-8a3e-5f5d348d5504)
```go
func producer(m *map[int]string, mu *sync.RWMutex, wg *sync.WaitGroup) {
	for i := 0; i < 50; i++ {
		vm := *m
		mu.Lock()
		vm[i] = fmt.Sprint("$", i)
		mu.Unlock()
	}
	wg.Done()
}
func consumer(m *map[int]string, mu *sync.RWMutex, wg *sync.WaitGroup) {
	for i := 0; i < 50; i++ {
		vm := *m
		mu.Lock()
		fmt.Println(vm[i])
		mu.Unlock()
	}
	wg.Done()
}
func main() {
	m := make(map[int]string)
	m[0] = "1234"
	wg := sync.WaitGroup{}
	mu := sync.RWMutex{}
	for i := 0; i < 50; i++ {
		wg.Add(2)
		go producer(&m, &mu, &wg)
		go consumer(&m, &mu, &wg)
	}
	wg.Wait()
}
```
## Channel Comunication
```go
func EvenPrinter(num int, ch chan int, wg *sync.WaitGroup) {
	if num%2 == 0 {
		ch <- num
	}
	wg.Done()
}

func OddPrinter(num int, ch chan int, wg *sync.WaitGroup) {
	if num%2 != 0 {
		ch <- num
	}
	wg.Done()
}
func Caller(arr []int, ch1, ch2 chan int, wg *sync.WaitGroup) {

	for i := range arr {
		wg.Add(2)
		go EvenPrinter(arr[i], ch1, wg)
		go OddPrinter(arr[i], ch2, wg)
	}
	wg.Wait()
	close(ch1)
	close(ch2)
}
func main() {
	arr := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18}
	ch1 := make(chan int)
	ch2 := make(chan int)
	wg := sync.WaitGroup{}
	go Caller(arr, ch1, ch2, &wg)
	i := 0
	for {
		if i == len(arr) {
			break
		}
		if v, ok := <-ch1; ok {
			fmt.Println(v, " EVEN")
		}
		if v, ok := <-ch2; ok {
			fmt.Println(v, " ODD")
		}
		i++
	}
}
```
## Dependent Goroutine
```go
func Step1(arr []int, out chan int, wg *sync.WaitGroup) {
	defer wg.Done()
	max := -1
	for i := 0; i < len(arr); i++ {
		if max < arr[i] {
			max = arr[i]
		}
	}
	fmt.Println("Max value:", max)
	// Signal Task 2 that Task 1 is done
	out <- max
}
func Step2(in chan int, wg *sync.WaitGroup) {
	// Wait for the signal from Task 1 that it is complete
	num := <-in
	defer wg.Done()
	fmt.Println("Calculating factorial for:", num)
	fmt.Println(factorial(num))
}
func factorial(n int) int {
	if n == 0 || n == 1 {
		return 1
	}
	return n * factorial(n-1) 
}
func main() {
	arr := []int{2, 1, 5, 4, 3, 8, 7}
	ch := make(chan int)
	wg := sync.WaitGroup{}
	wg.Add(2)
	go Step1(arr, ch, &wg)
	go Step2(ch, &wg)
	wg.Wait()
}
```
## Limited Concurency
The buffered channel ch effectively limits the number of concurrently running tasks to 5 by acting like a semaphore. when it holds 5 true value execution blocked (waiting) until one true read from the ch.
```go
func task(id int, ch chan bool, wg *sync.WaitGroup) {
	defer wg.Done()
	ch <- true // Acquire a slot (semaphore), it blocks after 5 bools until any reader reads from it.
	time.Sleep(time.Second * 2)
	fmt.Println("---", id)
	// Once Task finishes (after 2 seconds), it takes a true out of the channel, freeing up a slot.
	<-ch // Release the slot (semaphore)
}
func main() {
	wg := sync.WaitGroup{}
	ch := make(chan bool, 5)
	for i := 0; i < 40; i++ {
		wg.Add(1)
		go task(i, ch, &wg)
	}
	wg.Wait()
}
```
This mechanism effectively implements rate limiting or pooling. We are allowing only 5 tasks to run at the same time (concurrently). This is useful in scenarios where we want to limit resource usage, such as limiting concurrent database connections or network requests.

## Task distributions

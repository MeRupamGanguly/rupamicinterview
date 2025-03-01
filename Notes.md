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

## RabbitMQ

RabbitMQ is a queue service. Publisher sends Messages or Events to RabbitMQ Queue and Subscribers get those Messages or Events and then Processed accordingly.

In RabbitMQ we have conecpts like Exchanges, by which we can sends message to specific queues and receive message from specific queues based on certain rules. 

In RabbitMQ, queues should be declared in the consumer side. The publisher does not need to declare queues, but instead, it publishes messages to an exchange. The exchange is responsible for routing the messages to the appropriate queues based on the routing key and binding configuration.

In Topic Exchange Publisher sends messages to specific queues based on routing pattern specified by the routing key. The routing key can include wildcards (* for a single word and # for multiple words).


Publisher :
```go
func main() {
	// Establish a connection to RabbitMQ
	conn, err := amqp.Dial("amqp://guest:guest@localhost:5672/")
	// if err != nil {
	// 	log.Fatalf("Failed to connect: %s", err)
	// }
	// defer conn.Close() // Ensure connection is closed when the function exits

	// Create a channel to communicate with RabbitMQ
	ch, err := conn.Channel()
	// if err != nil {
	// 	log.Fatalf("Failed to create channel: %s", err)
	// }
	// defer ch.Close() // Ensure channel is closed when the function exits

	// Declare a topic exchange named "topic_logs"
	err = ch.ExchangeDeclare(
		"topic_logs",    // Exchange name
		"topic",     // Exchange type (topic exchange)
		true,        // Durable: The exchange will survive server restarts
		false,       // Auto-deleted: The exchange won't be deleted when no consumers are connected
		false,       // Internal: The exchange is not internal to RabbitMQ
		false,       // No-wait: Don't wait for confirmation when declaring the exchange
		nil,         // Additional arguments (none in this case)
	)
	// if err != nil {
	// 	log.Fatalf("Failed to declare exchange: %s", err)
	// }

	// Publish some messages
	// Routing key that matches the pattern for consumers (in this case, it will match "animal.cat")
	messages := []struct {
		routingKey string
		body       string
	}{
		{"animal.cat", "Cat message"},
		{"animal.dog", "Dog message"},
		{"animal.bird", "Bird message"},
	}

	for _, msg := range messages {
		err = ch.Publish(
			exchange, msg.routingKey, false, false,
			amqp.Publishing{
				ContentType: "text/plain",
				Body:        []byte(msg.body),
			},
		)
		// if err != nil {
		// 	log.Fatalf("Failed to publish message: %s", err)
		// }
	}

	// Print the sent message
	// fmt.Println("Message sent:", messages)
}
```
Consumer :
```go
// Consumer function to handle message processing
func consumeMessages(ch *amqp.Channel, wg *sync.WaitGroup, queueName string, prefetchCount int) {
	defer wg.Done()

	// Set the prefetch count: This ensures the consumer will not receive more than `prefetchCount` messages at once
	err := ch.Qos(prefetchCount, 0, false) // The consumer will only receive 5 messages at once
	// if err != nil {
	// 	log.Fatalf("Failed to set Qos: %s", err)
	// }

	// Start consuming messages from the queue
	msgs, err := ch.Consume(
		queueName, // Queue name
		"",        // Consumer tag (empty string means RabbitMQ will generate a tag)
		false,     // Auto-acknowledge messages (false means manual ack is required)
		false,     // Exclusive: This consumer is not exclusive to the connection
		false,     // No-local: Don't deliver messages published by the same connection
		false,     // No-wait: Don't wait for acknowledgment
		nil,       // Additional arguments (none in this case)
	)
	// if err != nil {
	// 	log.Fatalf("Failed to consume messages: %s", err)
	// }

	// Process each message
	for msg := range msgs {
		// Simulate processing of the message (you can replace this with actual business logic)
		fmt.Printf("Processing message: %s\n", msg.Body)
		time.Sleep(1 * time.Second) // Simulate processing time (can be replaced with actual logic)

		// Acknowledge the message to let RabbitMQ know it's been processed
		msg.Ack(false)

		// Flow control: If processing is too fast, we could add custom logic to slow it down
		// For example, you could use a rate limiter, or check system resource usage to control flow.
	}
}

func main() {
	// Establish a connection to RabbitMQ
	conn, err := amqp.Dial("amqp://guest:guest@localhost:5672/")
	// if err != nil {
	// 	log.Fatalf("Failed to connect: %s", err)
	// }
	// defer conn.Close() // Ensure connection is closed when the function exits

	// Create a channel to communicate with RabbitMQ
	ch, err := conn.Channel()
	// if err != nil {
	// 	log.Fatalf("Failed to create channel: %s", err)
	// }
	// defer ch.Close() // Ensure channel is closed when the function exits

	// Declare a topic exchange named "topic_logs"
	exchange := "topic_logs"
	err = ch.ExchangeDeclare(
		exchange,    // Exchange name
		"topic",     // Exchange type (topic exchange)
		true,        // Durable: The exchange will survive server restarts
		false,       // Auto-deleted: The exchange won't be deleted when no consumers are connected
		false,       // Internal: The exchange is not internal to RabbitMQ
		false,       // No-wait: Don't wait for confirmation when declaring the exchange
		nil,         // Additional arguments (none in this case)
	)
	// if err != nil {
	// 	log.Fatalf("Failed to declare exchange: %s", err)
	// }

	// Declare a queue (anonymous, will be deleted after the consumer disconnects)
	queue, err := ch.QueueDeclare(
		"",    // Empty queue name (RabbitMQ generates a random queue name)
		false, // Durable: The queue won't survive server restarts
		true,  // Delete when unused: The queue will be deleted when no consumers are connected
		true,  // Exclusive: The queue is exclusive to this connection
		false, // No-wait: Don't wait for confirmation when declaring the queue
		nil,   // Additional arguments (none in this case). will use for dead letter exchange
	)
	// if err != nil {
	// 	log.Fatalf("Failed to declare queue: %s", err)
	// }

	// Set prefetch count to 5 (each consumer will only receive 5 messages at a time)
	prefetchCount := 5
	// Bind the queue to the exchange with a routing key pattern "animal.*"
	routingKey := "animal.*"
	err = ch.QueueBind(
		queue.Name,   // Queue name
		routingKey,   // Routing key pattern
		exchange,     // Exchange to bind to
		false,        // No-wait: Don't wait for confirmation when binding the queue
		nil,          // Additional arguments (none in this case)
	)
	// if err != nil {
	// 	log.Fatalf("Failed to bind queue: %s", err)
	// }

	// Use a wait group to wait for all consumers to finish processing
	var wg sync.WaitGroup
	numConsumers := 3 // Number of consumers to start concurrently
	for i := 0; i < numConsumers; i++ {
		wg.Add(1)
		go consumeMessages(ch, &wg, queue.Name, prefetchCount)
	}

	// Wait for all consumers to finish processing
	wg.Wait()
}
```

You have a topic exchange (topic_logs) with messages being published to it with routing keys such as animal.cat, animal.dog, animal.bird. The consumers are bound to receive messages that match the animal.* pattern, so they will get messages with keys like animal.cat, animal.dog, and so on.


In Fanout Exchange Publisher sends messages to all Queues connected to Fanout Exchanges. 
```go
// Declare fanout exchange
ch.ExchangeDeclare("logs", "fanout", true, false, false, false, nil)

// Publish a message (routing key is ignored for fanout)
err = ch.Publish("logs", "", false, false, amqp.Publishing{
    ContentType: "text/plain",
    Body:        []byte("Fanout exchange message"),
})
```
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
In Direct Exchange Publisher sends message to specific Queues based on a Exact match of Routing key.
```go
// Declare direct exchange
ch.ExchangeDeclare("direct_logs", "direct", true, false, false, false, nil)

// Publish a message with a routing key (e.g., "error")
err = ch.Publish("direct_logs", "error", false, false, amqp.Publishing{
    ContentType: "text/plain",
    Body:        []byte("Error in processing the task"),
})
```
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

In Header Exchnage Publisher sends messages to all queues based on Message Headers rather than Routing Key.
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
- **Durable Queue**: Survives server restarts, messages are not lost. In `ch.QueueDeclare()` function we have one boolean argument `durable` by which we can set it.
- **Transient Queue**: Does not survive a server restart.  In `ch.QueueDeclare()` function we have one boolean argument `durable` by which we can unset it and make it Transient.
- **Exclusive Queue**: Only used by one consumer and deleted when that consumer disconnects. In `ch.QueueDeclare()` function we have one boolean argument `exclusive` by which we can set it. 
- **Auto-Delete Queue**: Deletes itself when no consumers are using it. In `ch.QueueDeclare()` function we have one boolean argument `auto-delete` by which we can set it. 

- **Dead Letter Queues**: Special queues for storing messages that can't be delivered (e.g., after too many retries).
```go
// Declare a dead letter exchange
	args := amqp.Table{
		"x-dead-letter-exchange": "dlx_exchange",
	}
	_, err = ch.QueueDeclare(
		"normal_queue",
		true,  // durable
		false, // delete when unused
		false, // exclusive
		false, // no-wait
		args,  // arguments for DLX
	)
```
- **Automatic Acknowledgement**: The message is automatically confirmed once sent to the consumer. This is the default behavior. In `ch.Consume()` function we have one boolean argument `auto-ack` by which we can set it.

- **Manual Acknowledgement**: The consumer confirms it has received and processed a message. In `ch.Consume()` function we have one boolean argument `auto-ack` by which we can unset it. In this case, the message is not considered acknowledged until you explicitly call the Ack method. `msg.Ack(false)`.

- **Negative Acknowledgement (Nack)**: When a message is rejected by a consumer, RabbitMQ can retry or discard it. In this case, you can use Nack to reject the message, and optionally, you can requeue it for another attempt. `msg.Nack(false, true)` true to requeue the message

- **Clustering**: Running RabbitMQ on multiple servers to spread the load and ensure it's always available.
- **Mirrored Queues**: Copying queues to other servers in the cluster so that if one server fails, messages are still available.
- **Federation**: Allowing RabbitMQ instances in different locations to share messages.
- **Prefetch Count**: Limit how many messages a consumer can process at once to avoid overwhelming it.
- **Concurrency**: Running many consumers in parallel to handle more messages.
- **Flow Control**: Managing how messages are processed to avoid overloading RabbitMQ.
- **Memory and Disk Usage**: Keep track of resource usage to prevent performance issues.
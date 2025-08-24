## NodeJS Architecture
## 1. Single Threaded Event Loop
- Node.js runs on a single main thread (JavaScript thread).
- It uses the event loop to manage multiple requests without creating a new thread for each.
- This makes Node.js lightweight and efficient for I/O-heavy tasks.
## 2. Event Loop + Libuv
- The event loop (part of Node.js core) manages:
     - Incoming requests
	 - Scheduling of callbacks
	 - Delegation to background workers
- Underneath, Node.js uses libuv, a C library that provides:
     - The thread pool (for heavy tasks like file system, DNS, compression, crypto).
## 3. Components of Node.js Architecture
```
Think of it like layers:
a. Application Layer
	•	Your JS code (business logic).
	•	Uses Node’s core modules (http, fs, crypto, etc.).
b. V8 Engine
	•	Node.js uses Google’s V8 JavaScript Engine (same as Chrome).
	•	Converts JS into machine code for execution.
c. Libuv
	•	Handles the event loop.
	•	Provides the thread pool for CPU-heavy or blocking tasks.
d. OS
	•	Networking, file system, CPU cores → all managed by the underlying operating system.
```
## 4. Request Handling Flow
- Client Request comes in (HTTP, file read, DB query) - event Queue.
- Event loop continuously keeps a watch on the event queue. It is based on FIFO principle (first request first served)
  - It decides whether the task is a blocking/non-blocking operation.
  - If it’s a simple task (small calc, returning cached data), non-blocking → executed directly in the single thread.
  - If it’s a heavy I/O task (file read, DB call, network call) → delegated to libuv’s thread pool or OS async APIs.
  - File I/O, crypto, compression → handled by libuv thread pool.
       - The thread pool has 4 worker threads by default. It takes up a heavy task whenever any of the thread is free.
	   - The wait time for the requests will increase, node becomes slow if there are lots of blocking request as the thread pool will be completely busy.
	   - We can maximize the threads in the thread pool equal to the CPU cores of the machine.
	   - To maintain system scalability, we should have a code with non-blocking operations and minimal blocking operations.
  - Network I/O (like HTTP, sockets) → handled by OS async APIs
       - The OS is incredibly efficient at handling thousands of simultaneous sockets because it doesn’t create one thread per connection (that would be costly, just like in Java/PHP servers).
       -  uses interrupts + system calls to handle network I/O.
       -  when the data arr
       -  ives, the event loop is notified. 
	3.	Once the task completes, the callback/promise is registered in the event loop.
	4.	Event loop executes the callback when the main thread is free.
	5.	Response sent back to client.
 
## 5. Important Idea
- Thread-per-request model (like Java/PHP): each request blocks a thread, leading to high memory usage under load.
- Node.js model: one thread + event loop, delegates blocking tasks to background thread pool, then resumes when ready.
- Cases of node process wrt server:
     - one server listening in one node process (single app.js file having one http server created) - one event loop
     - One Nodejs process, multiple servers (different ports)
     ```
     const http = require("http");

     const server1 = http.createServer((req, res) => res.end("From 3000"));
     server1.listen(3000);

      const server2 = http.createServer((req, res) => res.end("From 4000"));
      server2.listen(4000);
     ```
     - Still one process, one event loop. Both servers (server1, server2) are just two listeners registered with the OS. Multiple servers share the same event loop.
     - Multiple Node.js processes
     ```
     Example:
	•	Run node serverA.js (listening on 3000).
	•	Run node serverB.js (listening on 4000).

     ```
     - Each process has its own memory space, its own event loop. Its own V8 engine instance. They don’t share event loops.
     - They can only talk to each other via IPC (inter-process communication), OS sockets, or something like Redis/message queues.
     - ```process.exit()``` will stop the event loop for that particular process.
---
## NodeJS Lifecycle
## 1. Startup / Initialization
-  You run node app.js.
-  Node loads the JavaScript file, the built-in modules (like http, fs, etc.), and any external dependencies (require(...)).
-  It executes all top-level code (the synchronous part).
-  An event loop is started by Node.js (this is the “engine” that keeps Node alive).

## 2. Event Loop Phase
- The event loop is central to Node.js. It decides when callbacks, promises, and async tasks are executed.
- It goes through phases in a cycle:
   - Timers → Executes callbacks for setTimeout and setInterval.
   - Pending Callbacks → Executes I/O callbacks that were deferred.
   - Idle, Prepare → Internal use (not relevant for apps).
   - Poll Phase → Fetches new I/O events (file system, network, etc.), executes callbacks immediately if ready.
   - Check Phase → Executes setImmediate() callbacks.
   - Close Callbacks → Handles closing of sockets, handles, etc.

## 3. Handling Requests / Async Work
- When an HTTP request, file read, or DB query happens:
- The request is sent to the OS/libuv thread pool.
- Once the task is done, the callback (or promise resolution) is registered.
- The event loop eventually executes that callback.

## 4. Callbacks, Promises, Microtasks
- Microtasks Queue → Promises (.then, catch, finally) and process.nextTick().
- These run immediately after the current operation before the event loop continues.
- Callbacks Queue → Normal async callbacks like setTimeout, I/O completion handlers.

## 5. Exit / Termination
- When there are no more tasks, timers, or listeners, Node.js gracefully exits.
- Example: if you just run a script with no async code → Node executes it and exits immediately.

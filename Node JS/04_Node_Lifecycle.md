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
	   - Non-blocking I/O on different OS platforms.
	   - The event loop implementation.
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
	1.	Client Request comes in (HTTP, file read, DB query).
	2.	Event loop receives it.
	•	If it’s a simple task (small calc, returning cached data) → executed directly in the single thread.
	•	If it’s a heavy I/O task (file read, DB call, network call) → delegated to libuv’s thread pool or OS async APIs.
	3.	Once the task completes, the callback/promise is registered in the event loop.
	4.	Event loop executes the callback when the main thread is free.
	5.	Response sent back to client.
 
## 5. Important Idea
- Thread-per-request model (like Java/PHP): each request blocks a thread, leading to high memory usage under load.
- Node.js model: one thread + event loop, delegates blocking tasks to background thread pool, then resumes when ready.
⸻
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

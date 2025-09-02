- The event loop is basically a C program inside libuv that orchestrates execution of JS code, async callbacks, timers, I/O, etc.
- Each iteration of the loop is called a tick.
- Within a tick, Node.js goes through phases in a fixed order.

### 1. Timers Phase
- Executes callbacks scheduled by setTimeout() and setInterval() if their time has expired.
- The delay is not guaranteed. It only means “execute after at least X ms,” actual execution depends on event loop load.

### 2. Pending Callbacks Phase
- Executes I/O callbacks that were deferred to the next loop iteration.
- Example: some TCP errors, DNS lookup errors.

### 3. Idle, Prepare (internal only)
- Internal use by Node.js, you usually don’t interact with this.

### 4. Poll Phase (the heart)
- Waits for new I/O events (like network, file system).
- Executes I/O callbacks almost immediately if they are ready.
- If no timers are waiting, it can block here for new I/O.
- This is where your server reads HTTP requests, sockets, etc.

### 5. Check Phase
- Executes callbacks from setImmediate().

### 6. Close Callbacks Phase
- Executes close event callbacks for sockets/handles (e.g., socket.on('close', ...)).

## 🏎️ Microtasks (special queue)
- Alongside phases, Node.js also has a Microtask Queue for:
   - Promises (.then, .catch, await)
   - process.nextTick()
- process.nextTick() runs immediately after the current operation, before moving to the next phase.
- Promise .then() callbacks run after the current phase’s callbacks, but before moving to the next phase.

- Between every phase, Node processes:
    - process.nextTick queue
    - Promise microtask queue
```
setTimeout(() => console.log("timeout"), 0);
setImmediate(() => console.log("immediate"));
process.nextTick(() => console.log("nextTick"));
Promise.resolve().then(() => console.log("promise"));

o/p -->
nextTick
promise
timeout  OR  immediate   (depends on context, usually timeout first if in main script)
```

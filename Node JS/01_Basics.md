## What is NodeJS?
- Javascript runtime environment
    - open source (available and accessible all over the internet, anyone can use, view, modify the code)
    - cross-platform (can be run on any OS)
    - runtime environment (an ecosystem that provides all the resources to execute the program) for executing javascript code outside the browser
- It allows us to use and run Javascript on the server-side on any machine outside browser facilitating building scalable backend systems.
- Built using Chrome's V8 Engine which compiles and interprets JS to native machine code and executes the program.
- V8 is written in C++ for speed and performance.
- V8 + Backend Features = NodeJS

## What are the advantages of NodeJS?
- **Efficiency**
     - provides event-driven (listens to events and performs actions based on the event when it occurs using callback), non-blocking I/O model for efficiency.
     - asynchrous by default ( Functions don’t wait for I/O operations (like file read, DB queries); they use callbacks, promises, or async/await.
     - Node doesn’t waste CPU cycles waiting for slow I/O. A single thread can manage thousands of concurrent requests without blocking the thread.
     - Memory usage is lower compared to thread-per-request models.
- Allows using JS on both client-side and server-side.
- **Scalability**
   - system resources are used optimally (minimal overhead) when handling thousands of simultaneous requests leading to high scalability for network applications.
- **Versatility**
   - can be used real-time apps (chat apps, gaming, collaboration tools), API servers (REST, GraphQL), streaming apps and IoT solutions.
   - can be used for local utility scripts (automates tasks and processes files locally)
   - Internet Of Things (IOT) - develops server side applications for IOT devices, managing communication and data processing
   - Scripting for Automation - automates repetitive tasks in software development processes such as testing and deployment
   - cross platform desktop applications (Github Desktop, Figma etc) can be built using frameworks like electron
   - Build tools for frontend technologies like webpack, grunt etc are built using nodejs
    
## What are the features of NodeJS?
- **Non-Blocking I/O Model**
    - designed to perform non-blocking operations by default
    - Node.js runs on a single thread. Instead of spawning a new thread per request, Node.js uses an event loop which listens for incoming events (like requests, I/O operations, timers).
    - Any I/O heavy task (like reading a file, querying a DB, API call) is delegated by the event loop to the system kernel / worker threads.
    - Node.js doesn’t block waiting for the result. It registers a callback or a Promise. While waiting, Node.js immediately moves to handle other requests.
    - When the background work finishes, Node.js pushes the result back into the event loop queue. The event loop then executes the callback/Promise handler.
    - In traditional servers (thread-per-request): 1000 requests → 1000 threads, Each thread eats memory + CPU, System slows down due to context switching.
    - In Node.js: 1000 requests → still 1 main thread with event loop, Each request registers callbacks, While DB/file API is processing, Node.js continues handling other requests. No idle time → more efficient resource usage.
    - Ideal for building API servers.
- **Networking support**
    - supprts TCP/UDP sockets which are crucial for building lower level network applications that browsers can't handle
- **File System Access**
    - provides APIs to read and write files directly which is not possible in browser environments for security reasons
- **Server-Side Capabilities**
    - enables JS to run on server, handle HTTP requests, file operations and other server side functionalities
- **Modules**
    - organize code into reusable modules using require() or import.
 
## What browser features is absent in NodeJs?
- window object, document object (used to access HTML elements in document), browser object model (to access browser realated APIs),
  certain Web APIs (session storage, local storage, fetch API etc)

## How can JS help on server side?
- Database management
   - stores, manages and retrieves data efficiently through CRUD operations
- Authentication
   - verifies user identities to control access to the system.
- Authorization
   - manages permissions and access controls for authenticated users
- Input Validation
   - checks incoming data correctness, completeness and security to prevent malicious data entry and errors
- Session Management
   - Tracks user activity across various requests to maintain state and manage user specific settings
- API Management
   - Provides an interface for applications to interact and have smooth data exchange and integration.
- Error Handling
   - manages and responds to error effectively to maintain system stability and provide useful error messages.
- Security Measures
   - implements protocols to protect data from unauthorized access and attacks, such as SQL injection and cross site scripting (XSS).
- Data Encryption
   - secures sensitive information by encrypting data stored in databases and during transmission.
- Logging & Monitoring
   - keeps records of system activity to diagnose issues and monitor system health and security.
 
## How to execute JS file in node?
- command - ```node filename.js``` assuming that the path  in the terminal  is the current folder where file is located.
- require syntax - ```require('modulename')``` is written in the beginning of JS file in order to include any other JS file or built in or external modules. ```.js``` is added automatically after the module name in require syntax.
- In modern ES, import keyword is used.
- What are modules?
    - modules are packages/files (reusable block of code) that helps to organize code in a way that it can be reused again, separate concerns and improve maintainability.
    - When you require() a module, Node.js loads and executes it once, then caches the result.
	- If you require the same module again, Node doesn’t re-run the file, it just returns the cached version.
    - This improves performance, since modules aren’t repeatedly loaded.
- NodeJS searches for these modules in core, node_modules directory and file paths.
- For local file module, you need add the relative path in reequire syntax.

## What is REPL (Read, Evaluate, Print, Loop)?
- interactive shell for JS
- ideal for quick testing and debugging code snippets on fly
- offers help commands
- supports saving and loading code sessions
- provides direct access to nodeJS APIs for experimentation
- allows customization of prompt and behaviour settings
 

  
      

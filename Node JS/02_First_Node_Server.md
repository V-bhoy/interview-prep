## How DNS (Domain Name Service) works?
- It translates human-friendly domain names (e.g., www.google.com) into machine-friendly IP addresses (e.g., 142.250.182.100) so that computers can communicate with each other.
- Imagine you type www.google.com in your browser:
   - Browser Cache Check: Your browser first checks if it already knows the IP for www.google.com. If cached, it skips the lookup.
   - OS / Local DNS Cache: If not found in the browser, your OS checks its own local DNS cache.
   - DNS Resolver (ISP or Custom): If still not found, the request (DNS query) goes to a DNS resolver (usually provided by your ISP or a public DNS like Google 8.8.8.8 or Cloudflare 1.1.1.1).
     The resolver’s job = “Find me the IP of this domain.” To resolve the domain into an IP address.
   - The DNS server then provides the correct IP address for the domain, the resolver passes the IP to the browser
   - The browser then uses it to connect to Google’s web server.
   - Browser caches the IP for a short time. Next time you visit, it skips all these steps until the cache expires.
- There are three types of DNS servers
- **Root DNS** - acts as a starting point when resolving a DNS query. It directs queries to the correct TLD server (.com, .org etc)
- **TLD (Top Level Domain) DNS** - handles queries for specific top level domains (.com, .org etc.) and then directs them to its authoritative DNS server (ex: google in .com)
- **Authoritative DNS** - contains the actual IP of the domain and answers DNS queries with this information

## How web works? How is client-server connection established?
- The client(browser) initiates a network call by entering the URL.
- The browser contacts the DNS server to get the IP address of the domain
- The browser establishes a TCP connection with the server's IP address.
- The browser sends an HTTP request to the server
- The server processes the request and prepares a response
- The server sends an HTTP response back to the client
- The response travels back to the client over the network
- The browser reveives and interprets the response.
- The browser renders the response content and displays it to the user.

## What are protocols?
- A protocol is basically a set of rules and conventions that define how data is transmitted and understood between devices on a network.
- Think of it as a language that computers agree on so they can communicate correctly.
- **HTTP (HyperText Transfer Protocol)**
   - facilitates comunication between a web browser and a server to transfer web pages
   - sends data in plain text (no encryption)
   - used for basic website browsing with no security
- **HTTPS (HyperText Transfer Protocol Secure)**
   - secure version of HTTP, encrypts data for secure communication
   - uses SSL/TLS to encryt data
   - used in online banking, e commerce
- **TCP (Transmission Control Protocol)**
   - ensures reliable, ordered, error checked data delivery over the internet
   - establishes connection before the data is transferred

## How to create a node server?
- create an http server using built in http module
- below is the snippet of app.js
- http.createServer()
    - Creates the server
    - It takes a callback with arguments (req, res) which runs whenever a client makes a request.
    - In the snippet, the requestListener is the callback function
- server.listen()
    - Makes the server listen on a specific port, if not given, it wont listen to incoming requests on the server
    - It also takes a callback which is optional, that runs immediately after server starts listening on given port.
- Run the file using command - ```node app.js```
- as soon as you enter the server address in your browser, the browser sends a req object, which the server listens and is logged in the callback function as per the below code snippet
``` javascript
// import http module to use it in the app.js file
const http = require('http');

function requestListener(req, res){
   console.log(request);
}

const PORT = 3000;
const server = http.createServer(requestListener);
server.listen(PORT, ()=>{
  console.log(`Server running on address: http://localhost:${PORT}`);
});
```
## What is the req and res object in the create server callback?
### req (request object)
-  Instance of http.IncomingMessage
-  Contains info about the client’s request
-  Common properties:
  - req.url → the path requested (/, /about, etc.)
  - req.method → HTTP method (GET, POST, etc.)
  - req.headers → headers (user-agent, content-type, etc.)
  - req.on("data") → used to read request body (for POST/PUT)
### res (response object)
- Instance of http.ServerResponse
- Used to send data back to the client
- Common methods:
  - res.writeHead(statusCode, headers) → set response headers
  - res.write(data) → write body (can be called multiple times)
  - res.end([data]) → end response (must always be called)
``` javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.write("Hello, this is your server!\n");
  res.end("Goodbye!");
});

server.listen(3000);
```
## How do you route in nodejs?
- Routing means deciding what response to send based on the URL and method.
``` javascript
const http = require("http");

const server = http.createServer((req, res) => {
  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Welcome to Home Page!");
  } else if (req.url === "/about" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("This is About Page.");
  } else if (req.url === "/api/data" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.end(JSON.stringify({ message: "Hello from API" }));
  } else {
    res.writeHead(404, { "Content-Type": "text/plain" });
    res.end("404 Not Found");
  }
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000");
});
```
- req.url helps match path (like /about)
- req.method helps match HTTP method (GET, POST, etc.)
- Based on these, you implement simple if/else routing.

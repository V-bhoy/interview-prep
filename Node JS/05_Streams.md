## Stream
- Data exchange over the internet happens in the form of small packets
  that is 100MB of data is broken into small packets and sent to the destination in sequence.
- A stream is just a sequence of data that flows piece by piece instead of all at once.
- In Node.js, many things are streams:
    - req (Incoming HTTP request) → a Readable stream (data comes from client).
    - res (HTTP response) → a Writable stream (we send data back).
    - Files, sockets, stdin/stdout, etc.
- Benefit: You don’t have to load the entire data in memory. It would be a lot of memory consumption for thousands of incoming requests.
- Efficient handling of large data without blocking memory.
- 	With streams:
	•	Node reads/handles data piece by piece (flowing chunks).
	•	You can start processing before all data arrives.
	•	Great for files, video streaming, big JSON uploads, etc.
- Example: reading a 1GB file → instead of loading all 1GB, Node gives it in smaller pieces.

## Chunk
- A chunk is one piece of data from the stream.
- Benefit: Breaking down continuous data into manageable packets.
- When Node gets data (say request body, or a file being read), it splits it into chunks.
- Node emits a data event for each chunk → you collect them.
- This allows Node to work asynchronously and non-blocking, instead of waiting for all data and process data progressively.
- Each chunk is usually a Buffer object (binary data).
```
Stream = [Chunk1] → [Chunk2] → [Chunk3] → ... → End

req.on("data", (chunk) => {
  console.log("Got chunk:", chunk);
});

o/p
Got chunk: <Buffer 7b 22 6e 61 6d 65 22 3a 22 56 61 69 ... >

- further processing
const body = "";
req.on("data", (chunk) => {
  console.log("Got chunk:", chunk);
  body += chunk.toSring(); // Convert Buffer -> string and append
});
- once all the chunks are received
req.on("end", ()=>{
  const parsedBody = JSON.parse(body); // JSON string to JS object
  console.log(parsedBody);
}):
```
## Buffer
- A Buffer is Node’s way of handling binary data (raw bytes).
- In JavaScript normally you deal with strings and numbers, but HTTP, files, images, videos → all are actually bytes.
- Buffer provides a way to store and manipulate these raw bytes efficiently.

---
- Because Node is single-threaded and optimized for I/O → it cannot afford to block memory with huge files or wait for all data before starting work.
- Streams + Chunks + Buffers = make Node fast, memory-efficient, and non-blocking.

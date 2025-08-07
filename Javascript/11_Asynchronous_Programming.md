### Synchronous
- code runs in a particular sequence of instruction given in the program
- each instruction waits for the previous instruction to complete its execution

### Asynchronous
- Sometimes imp instructions get blocked due to massive time taken in the previous instruction.
- This causes delay in the UI
- Asynchronous code allows to execute the next instruction immediated without blocking the flow.

### Callback
- a function passed as an argument into another function
- a callback is used in synchronous programming as well as asynchronous programming (ex: setTimeout( cb, delay))
- In real time programming, we come accross an issue: Callback Hell when using callbacks

**CALLBACK HELL**
- arises when we have lot of nested callbacks in a function forming a pyramid like structure also called Pyramid of Doom
- it becomes difficult to understand, manage and debug the operations and functions.
``` javascript
function getData(id){
   setTimeout(()=>{
     console.log("Data"+ id);
   }, 2000);
}
getData(1); // Data1 --> after 2 sec
// if you want to get a particular data after the prev data is fetched
getData(1)
getData(2)
getData(3)
--> this is going to fetch data all at the same time because the timer starts and it executes the next instruction immediately
// can be achieved using callbacks
function getData(id, getNextData){
   setTimeout(()=>{
     console.log("Data"+ id);
     if(getNextData){
        getNextData();
     }
   }, 2000);
}
getData(1, ()=>{
   getData(2, ()=>{
     getData(3, ()=>{
       getData(4);
     })
   })
});
// this will fetch data one after the other after 2 sec, this code is difficult to understand and manage
// this is called callback hell
```

### Promises
- the issue of callback hell can be solved using promises
- Promise is an object in JS, which signifies an eventual completion of a task
- Promise object has a prototype that has state and result
- It has 3 states - PENDING, FULFILLED, REJECTED
- Pending is a state where the promise is waiting to be either fulfilled / resolved or get rejected, result is undefined
- Fulfilled is the state when the promise is resolved, result has fulfilled value
- Rejected is the state when the promise is rejected, result is an error object
``` javascript
// creation of promise
// we create using new keyword followed by the constructor of Promise class
//  we need to pass a callback that takes two arguments - handler functions which we call resolve & reject
// resolve handler - used to resolve a promise
// reject handler - used to reject a promise
let promise = new Promise((resolve, reject)=>{
  console.log("I am a promise");
  resolve("sucess");
  // reject("Something went wrong");
})
```
- In general, we don't create promises, the APIs where we request data returns us a promise and we handle those promises in our programming.
  
**How to handle promises ?**
- we use .then((res)=>{...}) to perform operations when a promise is fulfilled
- we use .catch((err)=>{...}) to perform operations when a promise is rejected
``` javascript
const getPromise = ()=>new Promise((resolve, reject)=>{
  console.log("I am a promise");
  resolve("sucess");
// reject("Something went wrong");
})
let promise = getPromise();
promise.then((res)=>{
  // res is fulfilled result value, here it's - success
  console.log("Promise fulfilled!", res);
})
promise.catch((err)=>{
     // err is rejected result value, here it's - Something went wrong
   console.log("Promise rejected!", err);
});
```

### Promise Chain
- A promise chain in JavaScript is a sequence of .then() calls that allow you to perform asynchronous operations one after another, with each operation waiting for the previous one to complete.
- Each .then() returns a new Promise, allowing the next .then() to wait for the previous one.
- Useful when tasks depend on each other
``` javascript
function getData(id){
   return new Promise((resolve)=>{
      setTimeout(()=>{
         console.log("Data"+ id);
          resolve("success");
      }, 2000);
  });
}
getData(1); // Data1 --> after 2 sec
// if you want to get a particular data after the prev data is fetched, use promise chain instead of callback to avpid callback hell
getData(1).then((res)=>{
   return getData(2);
}).then((res)=>{
   return getData(3);
}).then((res)=>{
   return getData(4);
}).then((res)=>{
   console.log(res);
})
// this will fetch data one after the other after 2 sec, this code is easier to understand and manage
```
### Using .catch() in promise chain
- **1. Using .catch() at the end (common pattern)**
    - Any error anywhere in the chain will be caught here.
	  - It’s like a global catch for the entire chain.
	  - Commonly used for centralized error handling.
``` javascript
doStep1()
  .then(result1 => doStep2(result1))
  .then(result2 => doStep3(result2))
  .then(result3 => console.log("All done:", result3))
  .catch(error => console.error("Error caught at the end:", error));
```
- **2. Using .catch() in the middle**
    - If an error occurs before the .catch(), it is caught there.
	  - If the .catch() recovers (i.e., returns something), the chain continues.
	  - If it rethrows the error, the chain breaks unless another .catch() is added later.
``` javascript
Promise.resolve("Step 1")
  .then(() => {
    throw new Error("Something went wrong in Step 2");
  })
  .catch(err => {
    console.log("Caught in middle:", err.message);
    return "Recovered value";
  })
  .then(result => {
    console.log("Continued with:", result);
  });
o/p -->
Caught in middle: Something went wrong in Step 2
Continued with: Recovered value

// rethrow error
Promise.resolve("Step 1")
  .then(() => {
    throw new Error("Step 2 failed");
  })
  .catch(err => {
    console.log("Caught in middle:", err.message);
    throw err; // rethrow the same error
  })
  .then(result => {
    console.log("This will not run");
  })
  .catch(err => {
    console.log("Caught at end:", err.message);
  });
o/p -->
Caught in middle: Step 2 failed
Caught at end: Step 2 failed
```
### Async Await
- more simple than promise chains
- we use async keyword with a function declaration to define it as an asynchronous function
- an async function always returns a promise
``` javascript
async function sayHello(){
  console.log("Hello");
}
console.log(sayHello()); // returns a promise which is immediately resolved with value undefined
```
- await keyword pauses the execution of its surrounding async function until the promise is settled.
- it can be used only inside an async function
- let's modify the previous getData example with async await
``` javascript
async function getData(id){
   return new Promise((resolve)=>{
      setTimeout(()=>{
         console.log("Data"+ id);
         resolve();
      }, 2000);
   }
    
}
// returning a promise here with async because setTimeout alone would immediately resolve the function after timer is set.
async function getAllData(){
  await getData(1);
  await getData(2);
  await getData(3);
  await getData(4);
}
getAllData();
// this will fetch data one after the other after 2 sec, this is more easy to understand than promise chains
```
- we can handle the errors for async await using try-catch block or using .catch with async function
``` javascript
async function fetchData() {
  try {
    const res = await fetch('https://api.example.com/data');
    const data = await res.json();
    console.log(data);
  } catch (error) {
    console.error('Something went wrong:', error);
  }
}

async function fail() {
  throw new Error("Oops!");
}
fail().catch(err => console.log("Caught outside:", err.message));

// Realistic example
async function getUser() {
  const response = await fetch("https://api.example.com/user");
  const data = await response.json();
  return data;
}
getUser()
  .then((user) => console.log("User:", user))
  .catch((err) => console.error("Failed to fetch user:", err));
```
- Here we have to make an extra function call, to await all the async functions, like getAllData() in the above example
- we can resolve that using IIFE, Immediately Invoked Function Expression
- these functions are immediately called as soon as it is defined
- this is useful when you want to use the function only once, it cannot be reused again and again.
``` javascript
// Above example using IIFE
(async function(){
  await getData(1);
  await getData(2);
  await getData(3);
  await getData(4);
})()
```


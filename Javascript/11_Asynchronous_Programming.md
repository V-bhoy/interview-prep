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
## Promise APIS
### Promise.all()
- takes an array of promises as arg
- return a promise
- resolves only when all promises are resolved or there are no promises in the array.
- immediately rejected when any of the promise is rejected
``` javascript
function f1(){
   return new Promise((resolve, reject)=>{
     setTimeout(()=>{ resolve(5000)}, 1000);
})
}
function f2(){
   return new Promise((resolve, reject)=>{
     setTimeout(()=>{ resolve(8000)}, 3000);
})
}
function f3(){
   return new Promise((resolve, reject)=>{
     setTimeout(()=>{ resolve(1000)}, 2000);
})
}
Promise.all([f1(), f2(), f3()]).then((values)=> console.log(values)).catch(err=>console.log(err));
values --> [5000, 8000, 1000]

scratch

function myPromiseAll(arrOfPromises){
   if(arrOfPromises.length == 0){
       return Promise.resolve([]);
   }
   const values = [];
   let counter = 0;
   return new Promise((resolve, reject)=>{
      arrOfPromises.forEach((p, i)=>{
             if(p instanceof Promise == false){
                p = Promise.resolve(p);
             }
             p.then((value)=>{
                counter += 1;
                values[i] = value;
                if(counter == arrOfPromises.length) {
                   resolve(values);
                }
             }).catch(err=>reject(err));
       }) 
   })
}

```
### Promise.allSettled()
- returns a fulfilled promise, with an array of promise results.
- it returns all the promise results even if any of the promise is fulfilled / rejected.
- the promise result is an object -> if fulfilled -> {status: fulfilled, value} , if rejected -> {status: rejected, reason}
- if an empty array, the value is an empy array
``` javascript
Promise.allSettled([f1(), f2(), f3()]).then((values)=> console.log(values))
values --> [
   {status: 'fulfilled', value: 5000},
   {status: 'fulfilled', value: 8000},
   {status: 'fulfilled', value: 1000}, 
]

// scratch
function myPromiseAllSettled(arrOfPromises){
   if(arrOfPromises.length == 0){
       return Promise.resolve([]);
   }
   const values = [];
   let counter = 0;
   return new Promise((resolve, reject)=>{
      arrOfPromises.forEach((p, i)=>{
             if(p instanceof Promise == false){
                p = Promise.resolve(p);
             }
             p.then((value)=>{
                counter += 1;
                values[i] = {
                   status: 'fulfilled',
                   value
                 };
                if(counter == arrOfPromises.length) {
                   resolve(values);
                }
             }).catch(err=>{
                 counter += 1;
                values[i] = {
                   status: 'rejected',
                   reason: err
                 };
                if(counter == arrOfPromises.length) {
                   resolve(values);
                }
 });
       }) 
   })         
}

```
### Promise.race()
- returns the first promise that is either resolved/ rejected
- doesn't wait for any other promises
- if you pass an empty array, the promise continues to be in a pending state
```
Promise.race([f1(), f2(), f3()]).then((value)=> console.log(value)).catch(err => console.log(err))
value --> 5000 since f1 is resolved in 1 second
the promise is rejected if the first promise settled is rejected
```
### Promise.any()
- returns the first fulfilled promise, it waits until any of the promise is resolved to be fulfilled.
- if the none of the promise is resolved, it returns an aggregate error object having all the errors of the rejected promises.
- even when you pass an empty array -> the promise is rejected
  
## Async Await
- syntactic feature that allows asynchronus function to be structured in a way similar to an ordinary synchronous function (synchronous looking async code)
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
- Internally, await works like a .then() — it pauses the async function until the Promise resolves, and resumes execution by placing the continuation in the microtask queue.
- It doesn’t block the main thread and can run Promises in sequence or in parallel using Promise.all().
---
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
## How Promises Work in Parallel with Async/Await
- By default, await executes sequentially:
```
async function sequential() {
  const p1 = await fetch("url1");
  const p2 = await fetch("url2");
  return [p1, p2];
}
Here:
	•	fetch("url1") completes → only then fetch("url2") starts.
	•	Total time = t1 + t2 (slow).
```
- ⚡ To run in parallel:
- Start the Promises first, then await them together:
```
async function parallel() {
  const p1 = fetch("url1");
  const p2 = fetch("url2");

  const [res1, res2] = await Promise.all([p1, p2]);
  return [res1, res2];
}
	•	Both requests start at once ✅
	•	You wait for both to finish ✅
	•	Total time = max(t1, t2) (faster)
```


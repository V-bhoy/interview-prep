### What is a function?
- block of code that performs a specific task & can be invoked whenever needed.
- it avoids repeated code, avoiding code redundancy.
- all the variables/ methods declared in the function are accessible within the function.
- the function parameters are treated as local variables - accessible only within the function

### Function Definition/ Function Declaration/ Function Statement:
- normal function that is defined with its body
- It is fully hoisted and can be called even before it is declared.
``` javascript
function funcName(){....}
```

### What is the use of return statement?
- it is used to return a single value from a function as o/p.

### What is the difference between parameters & arguments?
- Parameters --> placeholders defined in function declaration as i/p to the function
- Arguments --> actual values passed to the function when it is invoked.

### In how many ways can you pass the arguments?
1. Positional arguments: sum(a, b)
2. Named Arguments: passing a single value by creating an object of arguments
3. Arguments object: we can use arguments object inside the function which is an array
   sum(1, 2, 3);
   function(sum){
      console.log(arguments.length);
   }

### How do you use default parameters in a function?
In JavaScript, default parameters allow you to specify default values for function parameters.
ex: function greet(name = "Guest"){
    console.log("Hello ", name);
}

### Is JavaScript Pass-by-Value or Pass-by-Reference?
- JavaScript is always pass-by-value — but the behavior depends on the type of data you’re working with.
With respect to functions:
1. primitives are passed by value, Function gets a copy of the value, the original value is npt modified.
2. objects & arrays are also passed by value of the reference that is memory address
   and not the reference itself, so the function can mutate the object.
   Function has local reference to same memory.
   Function’s reassignment affects only its local reference copy.
``` javascript
ex: function replacePerson(person) {
      person = { name: "Someone else" }; // reassigning the local copy of the reference
    }
    let user = { name: "Original" };
    replacePerson(user);
    console.log(user.name); // "Original"
    The original object remains unchanged because the function only reassigns
    its local copy of the reference, not the actual object.
```

### What is function expression?
- A function assigned to a variable / property of an object is known as function expression.
- We cannot call these before it is declared as it is treated as variable
- The function expression is not hoisted as functions.
- These functions can be either named / anonymous.
Usage --> as argument in other function
          value to be returned
          encapsulate code within a specific scope.

### What is a named function?
- A function whose name is specified is known as a named function
- we usually use it for big and complex logics
- Usage: used for recursion calls within itself

### What is an anonymous function?
- A function whose name is not specified is known as anonymous function.
- You cannot use it standalone otherwise it gives you a syntax error
  since function statements cannot be nameless.
- generally used to define small functions to do a specific task.
- Usage: assigned to a variable as its value or used as an argument
         or returned directly from the function.

### What is the difference between function statement and function expressions?
- Function statements are fully hoisted and can be used before they are declared.
- Function expressions are not hoisted as functions and cannot be used before they are ddeclared
  because they are treated as variables.

### What are arrow functions?
- introduced in ES6
- concise syntax to define functions expressions
- implicit return feature if there is a single statement.
- Arrow functions can have zero or more parameters.
  When there is only one parameter, the parentheses around the parameter can be omitted.
  For multiple parameters, parentheses are required
``` javascript
ex: ()=>{....}
```

### What is the difference between pure and impure functions?
- PURE FUNCTION ==>
   - A pure function is a function that always produces the same output for the same input.
   - Pure functions cannot modify the state.
   - Pure functions cannot have side effects. (does not modify any external state)
``` javascript
ex: function add(a, b) {
  return a + b;
}
```
- IMPURE FUNCTION ==>
  - An impure function, can produce different outputs for the same input.
  - Impure functions can modify the state.
  - Impure functions can have side effects. (modifies external state)
``` javascript
ex: let counter = 0;
    function increment() {
      counter += 1; // modifies external state ❌
      return counter;
    }
```

### What is IIFE (Immediately invoked function expression)
- a JavaScript design pattern that allows you to execute a function immediately after its declaration.
``` javascript
(function() {
// Function body
})();
```
**Usage:**

- **Encapsulation:** IIFEs create a separate scope for variables and functions,
avoiding global scope pollution. This helps prevent naming conflicts and
provides a way to encapsulate code and data.
- **Privacy:** Variables and functions declared inside an IIFE are not accessible
outside the function, creating privacy and protecting them from external
interference.
- **Modularization:** IIFEs can be used to create self-contained modules,
allowing you to define and expose only specific properties or methods to the
outer world.
- **Isolation:** IIFEs provide a level of isolation, allowing you to define
temporary variables and execute code without affecting the global state or
interfering with other parts of the application.
``` javascript
** Real-world examples:
1. const mathModule = (function() {
  function add(a, b) {
    return a + b;
  }
  function subtract(a, b) {
    return a - b;
  }
  return {
    add,
    subtract,
  };
})();
console.log(mathModule.add(2, 3)); // 5
Before import/export, developers used IIFE to simulate modules.
2. Create private scopes, This keeps $ function encapsulated and exposes only what’s needed.
(function(global) {
  const $ = function(selector) {
    return document.querySelector(selector);
  };
  global.$ = $;
})(window);
// Now you can use $('h1') globally
3. Script setup/init - Run code immediately on load
(function setup() {
  console.log("App is initializing...");
  // set up config, listeners, analytics, etc.
})();
```

### What are first class functions -
- The functions that are defined  as values to a variable, passed as an argument or returned as a value
  from a function are first class functions. (Functions are treated as variables)

### What is a callback function? I.M.P
- it is a function that is passed as an argument to another function.
- This function is executed later after some operation completes/ in response to an event.
**Usage:**
1. Functions can be made flexible by passing different callbacks:
``` javascript
function greet(name, callback) {
  const message = `Hello, ${name}`;
  callback(message);
}
greet("Vaishali", (msg) => {
  console.log(msg.toUpperCase());
});
```
- You can pass different callbacks to reuse the same logic with different results.
- Example: map, filter, forEach etc takes callback function to perform a specific operation based on different logics.
2. To handle asynchronous behavior:
- JavaScript is single-threaded, so callbacks allow us to run code after a task completes,
  without blocking the main thread.
``` javascript  
 ex: setTimeout(() => {
       console.log("This runs after 2 seconds");
     }, 2000);
 Here, the arrow function is a callback that might run after 2 seconds
 after the whole program is executed.
```
3. To process results after an operation:
- Like handling API responses, file reads, or user actions:
``` javascript
ex: fetch("https://api.example.com/data")
      .then(response => response.json())
      .then(data => {
        // ✅ This is a callback function
        console.log(data);
      });
```
Common use cases:
1. Async operations - setTimeout, setInterval, fetch, custom APIs
2. Array methods - map(), filter(), forEach()
3. Event handling - element.addEventListener('click', callback)
4. Custom logic injection - Passing user-defined functions to APIs

### What are higher order functions ?
- it is a function that can accept other functions as arguments or return a function as its result
- promotes abstraction and code reusability by encapsulating common functionality in a
  higher-level function. This can reduce code duplication and
  make the codebase more modular and maintainable.
- Common examples of higher-order functions in JavaScript include map(),
  filter(), reduce(), and forEach(), which accept a callback function as an
  argument. These functions encapsulate common operations on arrays and
  can be customized by providing different callback functions.

### What is function currying?
- Function currying is a technique in JavaScript that involves transforming a
  function with multiple arguments into a sequence of functions, each taking a
  single argument.
- It helps create more flexible and specialized functions by partially applying arguments,
  leading to cleaner and more expressive code.
- promotes code reusability by providing fixed base value.
``` javascript
example 1: customizable logger
function log(level) {
  return function(message) {
    console.log(`[${level}] ${message}`);
  };
}
const infoLog = log("INFO");
const errorLog = log("ERROR");
const debugLog = log("DEBUG");
infoLog("Server started");
// [INFO] Server started
errorLog("Something went wrong!");
// [ERROR] Something went wrong!
example 2: URL Builder for API Calls
function createURL(base) {
  return function(endpoint) {
    return `${base}/${endpoint}`;
  };
}
const apiURL = createURL("https://api.example.com");
console.log(apiURL("users"));      // https://api.example.com/users
console.log(apiURL("products"));   // https://api.example.com/products
```






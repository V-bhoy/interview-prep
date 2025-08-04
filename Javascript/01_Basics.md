### What is JS?
- a programming language - used to convert static web pages into dynamic and interactive web pages.

### What is JS ENGINE ?
- a code/program that is used to execute javascript
- it is present in browsers
Example: Chrome = V8
         Safari = JS-Core
         Mozilla = Spider Monkey
         Edge = Chakra
  
- **Working:**
   - It is the heart of Javascript Runtime Environment.
   - It takes the JS code as the input and goes through 3 major steps --> Parsing, compilation and execution
   - PARSING: The code is converted to tokens.
   - The syntax parser takes these tokens and converts into AST (Abstract syntax tree).
   - This AST is converted by the interpreter line by line to the bytecode which is finally
     executed by the engine.
   - The JIT compiler works along with the interpreter to optimize the code which improves the
     performance of execution.

### What is JRE ?
- javascript runtime environment
- it provides all the resources that is necessary to execute a javascript program.
- It includes the JavaScript engine, call stack, heap, web APIs, callback queues and event loop.
1. JS ENGINE: interprets & executes JS code
2. HEAP: memory space used to store objects dynamically at runtime by JS engine
3. WEB APIs : interfaces provided by browser that allows JS to interact with browser features
   These APIs include the alert(), confirm(), prompt(), setTimeout(), setInterval() methods and many more.
4. CALLBACK QUEUES & EVENT LOOP: used to manage asynchronous code in program.
5. CALL STACK: keeps track of function calls & its execution context.

### How does the event loop function ?


### Is JS single threaded or multithreaded language? Why?
- JavaScript is single-threaded by design — meaning it has one call stack and one main thread of execution.
- JS Engine runs your code one line at a time in a synchronous manner.
- JavaScript was originally designed to run in the browser for tasks like DOM manipulation, event handling,
  and user interactions, which are best handled in a single thread to:
  	•	Avoid race conditions (unpredictable result when 2 operations execute concurrently on same shared data)
  	•	Ensure predictable behavior
  	•	Keep the UI responsive

### How JS code is executed?
- Everything in javascript runs in an execution context.
- **What is an execution context?**
   - a container - holds information about current state of code being executed
   - it has 2 components ==> variable environment & thread of execution
      - Variable Environment ==> holds all variables & methods accessible within a specific scope.
                                 reference to the variable environment of its parent scope.
      - Thread of Execution ==> sequence of code execution that is currently being executed for a specific scope.
- **How is execution context created?**
   - it is created in 2 phases - CREATION PHASE & EXECUTION PHASE
   - Creation Phase ==> 1. The variable environment is set up.
                       2. It allocates memory to all declared variables and functions.
                       3. In case of variables - it stores undefined
                          functions - it stores the code as it is along with a reference to
                          its parent variable environment else it is null
   - Execution Phase ==> 1. The javascript engine executes the code line by line within the specific scope.
                        2. The variables are assigned with their actual values in the order they are declared.
- **FLOW OF EXECUTION FOR JS SCRIPT:**
  - JS script is loaded
  - A global execution context is created. The call stack in browser will have a pointer to anonymous.
  - Creation Phase for global execution context:
      1. It creates a global object which is nothing but window object in case of browsers.
         In Scope tab, we have global scope, a script scope for let & const variables
         and local scope for function calls.
      2. This global object (global scope) has many inbuilt window methods,
       all the variables and functions that are defined globally within the program
       that means outside any kind of block.
      3. The "this" variable is created and assigned to the window object.
       It represents the context in which the current code is executing.
       "this" keyword is by default a reference to this global object.
      4. Hoisting takes place.
  - Execution Phase:
      1. Engine executes the program line by line and assigns values to the variables in
       the order it is declared.
      2. Whenever a function is invoked, a whole new execution context belonging to the function
       is created in the call stack, and it is destroyed after that function is completely executed.
       (You will find a local scope in the scope section on function call, and the pointer in the
        call stack is on the local execution context)
      3. The local execution context defines the "this" variable. The value of
       this is determined based on how the function is invoked. If the function is
       called in the global scope or without any specific context, this will be
       assigned the global `window` object. However, in strict mode, this will be
       undefined in such cases.
       Additionally, the local execution context includes the creation of the
       `arguments` object. This object is available within the function and contains a
       list of all the arguments passed to it
       memory allocation takes place similar to the global execution context.
       The function logic is executed in its thread of execution, once it is completed,
       the local execution context is removed from the memory.
 - After the program completely executed, the global execution context destroyed.
 - Call Stack becomes empty
 - The execution context are independent of each other, it occupies its own memory and maintains its own
  execution stack which keep track of the execution

### What is a scope?
- defines the area in which the declared functions/variables is accessible
- Global scope - the variables / methods are accessible everywhere in the program.
  Local scope - the variables / methods are accessible only in the defined scope (function / block).

### What is hoisting ?
- It is JavaScript’s behavior of moving variable and function declarations to the top
  of their scope (either global or function scope) before the code is executed.
  But only the declaration is hoisted, not the assignment.
  1.  var keyword variables are hoisted, and you can use it before declaration.
      console.log(a); // undefined,
      var a = 10;
      only the declaration is hoisted i.e var a, not the assignment.
  2. Function declarations are fully hoisted, including the function body.
       sayHi(); // ✅ Works!
       function sayHi() {
         console.log("Hello!");
       }
  3. function expressions are hoisted as a variable (declared), but not as a function (not assigned yet).
     greet(); // ❌ TypeError: greet is not a function, its value is undefined
     var greet = function() {
       console.log("Hi!");
     };
  4. let and const are also hoisted, but they stay in a “Temporal Dead Zone” (TDZ)
     ensuring that they are not accessible before their actual declaration in the code.
     console.log(b); // ❌ ReferenceError!
     let b = 20;

### What is a temporal dead zone?
- let and const are stored in a different memory space other than global.
- the time period from a variable declaration to its initialization with a value is called
  temporal dead zone.
- When you try to access the let & const variables in a temporal dead zone,
  it gives reference error.
- To avoid temporal dead zone, push the declared/initialized variables at the top of the scope
  before they are accessed, making the window shrink to zero.

### What is the difference between undefined & not defined?
- undefined -->
  - indicates the absence of a value.
  - It is a primitive type and is assigned to a variable when it is declared but not initialized with a
  value or when a function does not return anything
  - Assigning undefined to a variable is a bad practice because it has a specific purpose.
- not defined -->
  - is a state of a variable that has not been declared at all.
  - If you try to access such a variable, JavaScript throws a ReferenceError exception
  because it is not present in the memory.

### What is lexical environment ?
- It refers to the variable environment of execution context in which the code is being executed.
  It contains all the variables/functions declared in that scope and a reference to its parent environment
- A fresh lexical environment is generated whenever a function is invoked in JavaScript.

### What is a scope chain?
- it allows a function to access variables from its outer (enclosing) lexical
  environment as well as from the global scope.
- When JavaScript can’t find a variable in the current scope, it goes up the chain —
  from child to parent, — until it finds it or reaches global.
- scope chaining only works in one direction, from inner to outer, and not the other way around.
- variables defined in an inner scope cannot be accessed from an outer scope.

### What is shadowing ?
- Shadowing happens when a variable in an inner scope has the same name as a variable in an outer scope,
and the inner one “shadows” or hides the outer one.
``` javascript
ex. var a = 100;
    let b = 200;
    {
       var a = 10;
       let b = 20;
       console.log(a);
       console.log(b); // 20, the b value hides the value in outer scope
    }
    console.log(a) // 10, the value was modified because it pointed to the same memory address
    console.log(b); // 200 , the block scope gets destroyed and the variable b was declared in 2 different scopes
                          // the block scope, and a separate memory space when declared in global
                          // Same thing happens with const and when using functions instead of block
```

### What is illegal shadowing?
- it happens when you declare the variable with same name, but it conflicts with already declared
  variable due to overlapping scopes.
``` javascript
ex.let a = 10;
   {
     var a = 10; // var is crossing the boundaries and interfering with let, which violates shadowing
    // If we use function instead of block here, then it is valid
   }
```

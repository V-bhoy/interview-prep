### What is a data type?
- it describes the type of data stored in a variable.

### Describe the data types in JS.
- Primitive data types - number, string, boolean, undefined, null, bigint, symbol
- Non-primitives - objects, arrays, Date, functions, regExp etc.
``` javascript
let x = null;
typeof x; --> 'object'
internally it's an object, we treat it as a separate primitive
```

### What is the difference between primitives and non-primitives?
- PRIMITIVES -
  1. hold single value and are fixed for a specific language
  2. immutable in nature
``` javascript
  ex. let n = 10; n = 20;
10 & 20 will be stored in separate memory addresses, and n will point according to the assignment.
JS has 7 primitive data types.
```
- NON-PRIMITIVES -
  1. can hold multiple values & methods.
  2. mutable & complex in nature

### What is the difference between undefined & null ?
- undefined is assigned to value that is declared, but not assigned or when nothing is returned from a
  function. It has a purpose where it is unknown of that data type of value.
- null is intentionally assigned to signify that the variable does not contain any value.

### What is the typeof operator?
- used to determine the type of variable
- used to validate data received from external resources like API.

### What is type coercion in JS?
- It is the ability of JS to automatically/ implicitly convert the value from one data type to
another at runtime.
- That's why it is also called dynamically typed language, which can also lead to unpredictable bugs.
``` javascript
examples:
1. "5" + 2 --> 52 (implicitly converts 2 to string data type)
2. "5" - 2 --> 3 (implicitly converts 5 to number data type)
3. true + 1 --> 2 (implicitly converts true to 1 , number data type)
4. false + 10 --> 10 (implicitly converts false to 0 , number data type)
5. "10" * "2" --> 20
6. null + 1 --> 1 (implicitly converts null to 0)
7. undefined + 1 ---> NaN (implicitly converts undefined to NaN )
- Explicit type coercion is manually done by developers.
- We have in built functions for that like Number(), String(), Boolean() etc.
```
### What are variables?
- Variables are references to the data stored in memory
- it is defined using var, let and const keywords.
- By default, the variables are assigned value undefined in the creation phase.

### What are the rules for defining variables in JS?
- case-sensitive
- allowed - alphabets, digits, $ and _
- start with - alphabets, $ and _
- reserved words cannot be used
conventions to follow -->
- written in camelcase

### What is the difference between var, let and const variables?
- var variable -->
  1. it is function-scoped
  2. it is hoisted.
  3. it can be re-declared.
  4. it can be re-assigned
  5. var can lead to bugs in code if not used properly.
- let variable -->
  1. it is block-scoped
  2. it is stored in a separate memory space other than global scope
  3. it is hoisted but cannot be accessed before initialization due to temporal dead zone.
  4. it is stricter than var and helps to avoid bugs caused by var.
  5. it cannot be redeclared, but we can reassign.
- const variable -->
  1. it is block-scoped
  2. it is stored in a separate memory space other than global scope.
  3. needs to assign value when declared
  4. cannot redeclare and reassign.
**let & const variables gives reference errors if used before initialization.**

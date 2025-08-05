### What is an exception?
- used to handle runtime errors in javascript

### Error Types:
**1. Syntax Error**
- occurs when there is an invalid syntax in the code.
``` javascript
  const x = ( 2 + 3
```
**2. Reference Error**
- occurs when a variable/ function has a reference that does not exist / is out of scope.
``` javascript
console.log(a);
```
**1. Type Error**
- occurs when an operation/ method is applied to an incompatible type
``` javascript
let a = "hello"
let b = a*2 // cannot perform arithmetic on string
```
### Manually throw error
``` javascript
 throw new Error("Something went wrong!);
```
- this can be caught in try catch block otherwise it will result into an uncaught error

### Handling exceptions
**1. try-catch block**
``` javascript
try{
    throw new Error("Something went wrong!);
}catch(e){
    console.log(e);
}
```
**2. try-catch-finally block**
``` javascript
try{
    throw new Error("Something went wrong!);
}catch(e){
    console.log(e);
}finally{
  // code that gets executed anyway
}
```
- There are some errors that JS cannot catch
``` javascript
1. Syntax error - use eval() / new Function()
2. Stack-overflow error - avoid infinite recursion
3. Memory leaks - improve memory management
4. Async errors - use .catch() / try-catch inside async
5. event listener errors - use try-catch inside listener
6. network errors - use .catch() on promises
```

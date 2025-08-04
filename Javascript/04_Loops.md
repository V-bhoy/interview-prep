### LOOPS IN JS ==>
- used to execute a piece of code repeatedly until a specific condition is met

**1. for loop**
``` javascript
for(initialization; condition; updation){...}
```
- first values is initialized
- condition is checked --> true --> execution of block --> updation --> condition checl
- if condition is false, the loop is terminated.

**2. while loop**
``` javascript
while(condition){....}
```
- Generally, the initialization is done outside the loop and, updation is written inside the logic.
- the block is executed until the condition is true

**3. do-while loop**
``` javascript
do{...}while(condition);
```
- same as while loop, only difference is that the code is executed at least once before the
     condition is checked.

**4. for-of loop**
- used to iterate over string and arrays, there is no need of initialization, stopping and updating
    condition.
- It targets each character of string or each item of array.
``` javascript
    for(let s of "string"){
       console.log(s) // prints each character of string
    }
```

**5. for-in loop**
- same as above, used to iterate over objects and arrays
- for objects --> targets key
- for arrays --> targets item
``` javascript
     for(let key in obj){
           console.log(obj[key]) // prints each value of object
     }
```

### What is the difference between break and continue statements?
- break ==> used to terminate the loop
- continue ==> skips the current iteration of the loop

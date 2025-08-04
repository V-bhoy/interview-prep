### CONDITIONAL STATEMENTS -->
- used to implement some conditions in a code.

**1. if statement**
``` javascript
if(condition){....}
```
- The code in the block is executed only if the condition is true

**2. if else statement**
``` javascript
if(condition){...}
else{...}
```
- if condition is true, the code in the if block is executed else the code in the else block is executed

**3. else if statement**
- used to add multiple conditions
``` javascript
if(cond1){...}
else if(cond2){....}
else if(cond3){....}
else{...}
```
- if any of the condition is true, that block is executed otherwise the else block is executed.

**4. Ternary operator**
- concise way of if else statement
``` javascript
condition ? expression 1 : expression 2
```
- if condition is true expression 1 is evaluated and returned else expression 2 is evaluated

**5. switch statement**
``` javascript
switch(value){
  case A:
     {...}
     break;
  case B:
     {...}
     break;
  default:
     {...}
}
```
- it matches the value provided with the case value, and then the block is executed
- if break statement is not used, it executes all the following case blocks along with default

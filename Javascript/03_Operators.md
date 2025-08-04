### OPERATORS IN JS
- used to perform a specific operation.
``` javascript
Expression --> a + b
+ ---> operator
a, b ---> operands
```

### Types of operator ==>
1. Arithmetic - used to do mathematical operations between 2 operands
``` javascript
   | + ==> a + b
   | - ==> a - b
   | * ==> a * b
   | / ==> a / b
   | % ==> a % b --> gives remainder
   | ** ==> a ** b --> a to the power of b
```
2. unary operators - performs operation on single operand
``` javascript
   | ++ ==> a++ --> post - increment
        ==> ++a --> pre - increment
   | -- ==> a-- --> post - decrement
        ==> --a --> pre - decrement
   Example: let a = 5;
            console.log(++a) --> 6
            console.log(a++) --> 5
            console.log(a) --> 6
```
3. Assignment operators - used to assign values
``` javascript
   | = ==> a = b
   | += ==> a+=b --> a = a + b
   | -= ==> a-=b --> a = a - b
   | *= ==> a*=b --> a = a * b
   | /= ==> a/=b --> a = a / b
   | %= ==> a%=b --> a = a % b
   | **= ==> a**=b --> a = a ** b
```
4. Comparison operators - used to compare 2 operands and return a boolean value
``` javascript
   | == ==> a == b --> checks only values and gives result involving type coercion
   | === ==> a === b --> strictly checks the data type along with the value, does not involve type coercion
   | != ==> a != b --> gives result only on basis of values, involving type coercion
   | !== ==> a !== b --> strictly checks data type along with the value
   | > ==> a > b
   | < ==> a < b
   | >= ==> a >= b
   | <= ==> a <= b
```
5. Logical operators - used to compare expression and based on their boolean results, it will return
   a single value
``` javascript
   | && ==> a && b --> returns b only if a is true and b is true
   | || ==> a || b --> returns a if either a is true or b  if b is true
   | ! ==> !a --> negates the boolean value of a
```

### TRICKY EXAMPLES
``` javascript
1. [] + [] = "" --> empty string
2. [] + {} = '[object object]'
3. {} + [] = 0
4. true == 1 --> true
5. "0" == false --> true
6. null == undefined --> true
7. [] == false --> true
8. [1] == true --> true
"==" --> implicitly  does data type conversions and then compares values
```

### What is the difference between "==" and "===" operator?
- == --> implicitly  does data type conversions and then compares values which might lead to bugs
- === --> strictly checks data type without type coercion and compares values, gives accurate result.
``` javascript
ex : "5" == 5 --> true
     "5" === 5 --> false
```

### What is short circuit evaluation in JS ?
- it happens when the execution is stopped because result is determined already
  without evaluating further expression.
``` javascript
ex: let res = false && some expressions.
    let res = true || some expressions.
NOTE:
1. The && operator returns the value of last expression, if all expressions are true
2. The || operator returns the value of first expression it finds to be true
console.log(false && 5 || 2) --> 2
```

### What is operator precedence?
- operators with higher precedence is operated first according to BODMAS

### What is the difference between spread and rest operator?
- spread operator --> used to expand elements from an iterable into an individual element.
  1. used to copy array ==> [...arr]
  2. used to merge arrays ==> [...a1, ...a2]
  3. used to pass multiple arguments to a function = sum(...nums) where nums = [1,2,3] and sum(a,b,c)
- rest operator --> used in function parameter to collect all the remaining arguments into a single
  array
  ex. sum(a, b, ...args) --> args will be evaluated as an array.


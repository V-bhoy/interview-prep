### Time Complexity
- tells us about growth of time at runtime with respect to input
- meaning, if we increase input n for time t, how quickly will the time change.

### Space complexity
- algorithm either uses RAM during program computation
- second type is actual storage memory like hard disks, pen drive etc.
- we focus only on RAM here
- the maximum memory that can be taken with respect to input change at runtime.

### how to measure time complexity?
- count number of operations and converting it to big O notation

### how to measure space complexity?
- count data structure/variables created and convert it to big O notation

### What is Big O notation?
- represented by --> O(expression)
- TC = O(N) means runtime is directly proportional to input n
- time increases linearly with n operations
- 100million operations will take 100million time
- TC = O(1) - constant time complexity
- there is not much increase in time with input change
- TC=O(N^2) - quadratic time complexity
- TC=O(logN) - logarithmic time complexity

IMP ==>
### how to predict if the solution is acceptable?
1. if algorithm performs - 10^7 to 10^8 operations --> solution is mostly acceptable
2. if algorithm performs <= 10^7 operations --> solution is always acceptable
3. if algorithm performs greater than 10^8 operations - solution is not acceptable
``` javascript
example: if max value of n is 10^5 and your algorithm is taking O(n^2) time
         means 10^5^2 that is 10^10 operations will be performed which is bad.
         so you have to think of an approach for O(n) time complexity
- this is how to mentally check if your algorithm will be acceptable without wasting time.
let's say if max value of n is 20.
it means the expected T.C is exponential and there is high probability that the
concept of backtracking needs to be used in this.
let's say if max value of n is 10^12
it means if our solution is O(N) it will still not work because it's going to take 10^12
operations that's greater than 10^8, and we need something better than O(n) which is either
root n or log n, higher chances of using binary search or divide and conquer technique like
merge sort.
```

example 1:
- time complexity?
``` javascript
for(i=0; i<n; i++){print(i)}
- there is one operation --> print
- how many times it's going to be occurring --> number of time the loop runs that is n here.
- n * (1 print operation + increment operation + check condition)+declaration with 0
- 3n + 1 = O(3n+1)
- Rules ==> 1. Ignore constants to multiply / divide
            2. Ignore lower value terms
- We ignore 3 and 1 , so T.C becomes O(n)
```

### Whenever loops are used
1. number of times the loop runs?
2. number of operations performed per iteration

example 2:
``` javascript
for(int i=0; i%2==0; i++){
  print(i);
}
the loop runs --> 1 time when i = 0
when i=1, the condition fails and the loop breaks
so --> 1*(print+ condition check + increment)+ declaration
      = 4 operations --> O(4)
      = this is constant time complexity that is O(1)
```

example 3:
``` javascript
i=1;
while(i<n){
   print(i);
   i=2*i;
}
i--> 2 4 8 16 32 .... n
not clear how many times the loop runs
we assume the loop runs k times
when iteration  1 --> i = 2 = 2^1
                2 --> i = 4 = 2^2
                3 --> i = 8 = 2^3
                k --> i should be 2^k which is last iteration & has to be less than n
 hence 2^k < n
 taking log base 2 on both sides --> log(2^k) < log n --> k < log n (because log 2 to base 2 is 1)
 the max value of k can be upto log n
 the loop runs k + 1 times.
 since we exit the loop on k+1 iteration
 each time, i is doubled --> 2(k+1) --> O(2(logN+1)) --> O(logN)
```

example 4:
``` javascript
for(i=0; i<n; i++){
  for(j=0; j<m; j++){
     print(i+j);
  }
}
inner loop --> m times
outer loop --> n times
each iteration in outer loop iterates the inner loop m times
so, time complexity is O(n*m)
```

example 5:
``` javascript
A) for(i=0; i<n; i++){
  print(i)
}
B) for(i=0; i<n; i+=2){
  print(i)
}
which will take more time to run?
A will take more time because it will run n times
while B take n/2 times
A --> O(N)
B --> O(N)
time complexity is still same for both, because it doesn't tell the actual time
it tells the growth rate if time taken which is same for both algorithms.
if we increase 5times the input in both the algorithms,
 the time is going to increase linearly
```

## Time complexity in recursive cases:

### What is recursion?
- function calling itself until a base case is reached.
- the number of calls involved in it will estimate the time complexity
- the chain of the function calls recursively is the recursion tree
- number of operations = sum(time consumed in one function call) across the whole recursion tree

example1:
``` javascript
function f(n){
  if(n==1)
    return 1
  else
    return n * f(n-1)
}

f(5) --> 5 * f(4) --> 4 * f(3) --> 3 * f(2) --> 2 * f(1) --> 1
f(1) --> returns 1 --> O(1) // one operation
F(2) --> returns 2 * 1  --> O(1)
F(3) --> returns 3 * 2  --> O(1)
F(4) --> returns 4 * 6  --> O(1)
F(5) --> returns 5 * 24  --> O(1)
f(5) --> 5 nodes in tree
f(n) --> n nodes in tree --> O(1)+O(1)+O(1)+...+n times --> O(N)
```

example 2:
``` javascript
function fibonacci(n){
    if(n==1 || n==2)
      return 1
    else
      return fibonacci(n-1) + fibonacci(n-2)
}
Recursion tree --> fibo(6)
f(6) --->  calls f(5) first which is completely executes and then f(4) is called
f(6) --> f(5)
     ---> f(4)
f(5) -->f(4)    f(4)--> f(3)
    ---> f(3)       ---> f(2)
f(4) ---> f(3)  f(3)--> f(2)
    ---> f(2)       -> f(1)
f(3) --> f(2)
    ---> f(1)
f(3) ---> f(2) from branch f(5)
      --> f(1)
```

### the recursion tree pattern is - 
- maximum depth of tree for f(6) is 5 that is the levels = n-1
- total function calls --> total nodes
``` javascript
0th level --> 1 node --> 2^0 node
1 level --> 2 nodes --> 2^1 node
2 level --> 4 nodes --> 2^2 node
.....(n-2)th level --> 2^(n-2) nodes approx
The sum of this series is a geometric progression = 2^n-1
so total nodes = 2^n-1 - k where k is some fixed value in this algorithm because every node doesn't lead to 2 branches
we can ignore k, because it is some small number
total function calls = 2^n-1
each function call takes O(1) operation
so O(1) + O(1) + ....2^n-1 times
= O(1) * 2^n-1 = O(2^n-1) = O(2^n/2) = O(2^n)
Time complexity here is exponential O(2^n) which is worst
```

## CALCULATING SPACE COMPLEXITY
- contributed by --> variables, data structure, recursion

example: input array is given
- need to print each double of each element in array
``` javascript
1. recursion used --> no
2. data structure used --> array --> coming as i/p to algorithm --> ignore
3. variables --> int n --> array length --> constant
                 int num --> each iteration creates num and is destroyed after calculating
                             double of each element and the iteration is executed
                         --> at any point of time it is constant since its destroyed before the
                             creation of next
    = it is taking constant space
so the overall space complexity is O(1) which is not dependent on array size
space is not increasing on increase in input size
```

### space complexity for factorial recursion -->
- In recursive functions, the call stack stores the function calls in the recursion
tree, until the base call is made.
- This is an implicit memory consumed in the program
here the call stack stores n function calls for f(n)
- so space complexity is O(n)

### space complexity for fibonacci recursion -->
- calculate using recursion depth
- number of function calls in call stack = maximum depth in recursion tree
- here maximum depth is n - 1
- SC ==> O(n-1) --> O(n)

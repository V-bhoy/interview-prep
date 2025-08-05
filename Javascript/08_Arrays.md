### What is an array?
- collection of items stored in a contiguous manner (linearly) in memory
- index-based data structure
- used to store multiple items related to each other into a single variable
- it can store items of different data types
- good practice -- to store items of same data type.
- Arrays are mutable in nature - we can change an item at a particular index.
- Array is an object internally
``` javascript
Creation :
1. let arr = [1, 2, 3];
2. let arr = new Array(5); --> array of size 5 is created  with undefined value.
3. let arr = new Array(1, 2, 3, 4) --> [1, 2, 3, 4]

Length of array : arr.length
Retrieve items at index: arr[0], arr[1] etc.
```

### How to iterate over an array using loops?
- for-of loop, for-in loop

### What is array destructuring in an array?
- introduced in ES6
- allows to extract elements from an array and assign them to an individual variable in a single
  statement
``` javascript
  ex: const [f1, f2, f3] = fruits;
      where fruits = [apple, mango, banana];
```

### ARRAY METHODS
- built-in methods of array
``` javascript
1. push() --> add items to end of the array
2. pop() --> removes the lest element from an array
3. shift() --> removes the first element from an array
4. unshift() --> adds items at the start of an array
5. toString() --> converts array to string
6. concat() -> joins 2 array and returns a new array
7. slice() --> returns a part of array, does not modify original array
8. splice() --> modifies original array, used to add, remove or replace items
   ex: splice(starting index, number of items to delete, ...items to add)
       const arr = [1, 2, 3, 4] ;
       arr.splice(2, 0, 5, 6]
       arr --> [1, 2, 5, 6, 3, 4] --> add items from index 2
       if only starting index is passed, it will by default remove all the elements from
       the starting index.
```
### Higher Order Functions in Arrays:

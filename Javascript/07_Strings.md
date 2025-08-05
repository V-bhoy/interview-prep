### What is a string?
- string is a sequence of characters represented as a text
- each character in a string has its individual index starting from 0.
- strings are immutable in nature
- you cannot change a character in a string at a particular index, you need to modify and reassign again
```javacript
  ex: let str = "hello" --> Memory address: 88888x
      str = str.replace("h", "y") ---> this will create a new string with memory address 99999x
      and str will point to 99999x

CREATION --> let str = "hello"; let str = 'hello'
LENGTH --> str.length
RETRIEVE CHARACTER ---> str[0], str[1] etc.
```

### What is a string literal/ template literals?
- It is a way to define multiline string and have embedded expressions in a string.
- It is defined using backticks and does not ignore any white spaces if given.
```javacript
ex: `This is James.
     Can we talk?`
```

### What is string interpolation?
- when a string is created by embedding expression / substitution of placeholders, it is knows as
  string interpolation.
```javacript
  ex: `Sum of 1 and 2 is ${1+2}`;
```

### STRING METHODS:
- built-in functions to manipulate string
```javacript
1. str.toUpperCase()
2. str.toLowerCase()
3. str.trim() --> remove whitespaces from start & end
4. str.slice(start, ?end) --> returns a part of string from the given index
5. str.concat(str2) --> joins str2 to str and returns a new string
6. str.replace(searchVal, newVal) --> replaces only first matching value
7. str.replaceAll(searchVal, newVal) --> replaces all matching values
8. str.charAt(index) --> gives character at particular index.
9. str.split(",") --> converts string into array by distinguishing elements based on the value
Other methods --> includes(), substring() etc.
```

### In how many ways can you concatenate a string?
```javacript
1. + operator
2. concat()
3. template literals
4. join() --> [s1, s2].join(" ");
```

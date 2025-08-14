## WHERE CLAUSE
- used to filter rows from a table based on a condition.
- It is used with SELECT, UPDATE, and DELETE statements to return or modify only the rows that meet the specified condition.
- WHERE is applied before grouping (GROUP BY) and aggregation (HAVING).
- multiple conditions can be grouped together using provided operators.
``` sql
-- syntax
SELECT column1, column2
FROM table_name
WHERE condition;

SELECT name, salary
FROM employees
WHERE department = 'IT';

UPDATE employees
SET salary = salary + 5000
WHERE department = 'HR';

DELETE FROM employees
WHERE salary < 55000;
```
### Using Comparison Operators
- <, >, <=, >=, =
``` sql
SELECT * 
FROM employees
WHERE salary >= 55000;
```
### Using Logical Operators
- **AND** => WHERE cond1 AND cond2 (filters rows where all conditions are true)
- **OR** => WHERE cond1 OR cond2 (filters rows where either of the condition is true)
- **NOT** => WHERE col NOT IN (val1, val2, val3) (filters rows where value does not belong to given set)
``` sql
SELECT * 
FROM employees
WHERE department = 'IT' AND salary > 55000;
```
### BETWEEN Operator
- filter between a given range which is inclusive
``` sql
SELECT * 
FROM employees
WHERE salary BETWEEN 50000 AND 60000;
```
### IN Operator
- reduces multiple OR conditions;
``` sql
SELECT * 
FROM employees
WHERE department IN ('IT', 'HR');
```
### IS NULL, IS NOT NULL Operator
- filter rows having column with null value / not null values
``` sql
-- prime_status = null
SELECT *
FROM customer
WHERE prime_status IS NULL;

-- prime_status is not null
SELECT *
FROM customer
WHERE prime_status IS NOT NULL;
```
### Wildcards (Pattern Searching)
- **%** => any number of character from 0 to n
- **_** => single character
- we use LIKE operator with WHERE clause for pattern matching
``` sql
SELECT * FROM customer WHERE name LIKE '%p_';
-- it can be anything like abcpn where abc --> % and n --> _ , so it matches %p_
```
---
## ORDER BY Clause
- used to sort the fetched result set for single/multiple columns in ascending or descending order.
- ascending order is default when using ORDER BY 
``` sql
-- syntax
-- ASC means ascending and DESC means descending
ORDER BY column-name [ASC/DESC];

-- fetch employee with highest salary being on top
SELECT * FROM employee ORDER BY salary DESC;

-- it will sort by last name in descending first and for similar last_name it will sort first_name in ascending order 
SELECT * FROM customer ORDER BY last_name DESC, first_name ASC;
```

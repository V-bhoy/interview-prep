# Sub Queries
- A subquery (also called a nested query or inner query) is a query inside another query.
The inner query executes first, and its result is passed to the outer query.

## Key Points
- alternative to joins
- Outer query depends on inner query’s result.
- Can return a single value, a list of values, or a table.
- Mostly used for filtering, comparisons, or complex calculations.
- it mainly exists in 3 clauses
    - WHERE clause
    - FROM clause
    - SELECT clause

## WHERE Clause 
- filtering based on inner query.
``` sql
SELECT name
FROM Employees
WHERE dept_id = (SELECT dept_id FROM Departments WHERE dept_name = 'HR');
--  Here, the inner query finds dept_id of HR, and the outer query fetches employees in HR.
```
## FROM Clause 
- treat inner query result as a temporary table (a.k.a. derived table).
``` sql
SELECT dept, COUNT(*) as emp_count
FROM (SELECT dept_id as dept FROM Employees WHERE salary > 50000) sub
GROUP BY dept;
```
## SELECT Clause
- inner query provides a computed value.
``` sql
SELECT name,
       (SELECT AVG(salary) FROM Employees) AS avg_salary
FROM Employees;
--  Each row will show the employee name + the company-wide average salary.
```
## Types of Sub Queries
### Single-row subquery
- returns one value (used with =, <, >).
``` sql
-- Finds employees whose salary is greater than the overall average salary.
SELECT name, salary
FROM Employees
WHERE salary > (SELECT AVG(salary) FROM Employees);
-- Here the inner query returns a single value (average salary).
```
### Multi-row subquery 
- returns multiple values (used with IN, ANY, ALL).
``` sql
-- Gets employees who work in any department located in Pune.
SELECT name
FROM Employees
WHERE dept_id IN (SELECT dept_id FROM Departments WHERE location = 'Pune');
```
### Correlated subquery 
- inner query depends on outer query’s row, runs repeatedly.
``` sql
-- Finds employees earning more than the average salary in their department.
SELECT name
FROM Employees e
WHERE salary > (SELECT AVG(salary) FROM Employees WHERE dept_id = e.dept_id);
-- for each row of table e , the inner query will be executed
```
## Difference Between Joins And SubQuery
- Joins
   - faster
   - increase calaculation burden on DBMS
   - complex, difficult to understand and implement
   - choosing optimal join for optimal use case is difficult
- Sub Queries
   - slower
   - keeps responsibility of calculation on user
   - easy to understand and implement
   - optimal for different use cases

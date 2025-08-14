## GROUP BY clause
- used to collect data from multiple records and group the result by one or more column.
- generally used in a SELECT statement
- groups into category based on column given having same values in it
- the columns mentioned after select command should be repeated after GROUP BY clause in order to successfully execute the query
- used with aggregation functions otherwise it behaves like DISTINCT
- The main difference between GROUP BY and DISTINCT is that GROUP BY groups rows to perform aggreagate functions on the group while DISTINCT just removes duplicates and gives unique values.
- GROUP BY on multiple columns will consider the pair of column values as unique, same as DISTINCT
``` sql
-- count of rows in each distinct department
SELECT department, count(*)
FROM company
GROUP BY department;

SELECT department, location, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM company
GROUP BY department, location;
-- 	1.	Find all unique department-location combinations.
--	2.	For each group:
--     	•	COUNT(*) → count rows in that group.
--     	•	AVG(salary) → calculate average salary in that group.
```
- can be used with WHERE clause to give condition but GROUP BY is always written after WHERE clause
``` sql
-- this query will not include HR department in the result set
SELECT department, count(*)
WHERE department NOT IN ('HR')
GROUP BY department; 
```
## Aggregate Functions
- used to perform calculations on the groups/ category by the GROUP BY clause
- these are are built-in functions
- Without GROUP BY, they work on the entire result set as one group.
### COUNT()
- used to give the count, total number of rows in a group
- COUNT(*) counts all rows, including those with NULL values.
- COUNT(column) counts only rows where the column is not NULL.
``` sql
SELECT department, count(*) as count
FROM company
GROUP BY department;
```
### AVG()
- Returns the average value of a numeric column.
- Ignores NULL values.
``` sql
-- Find average salary per department
SELECT department, AVG(salary) AS avg_salary
FROM company
GROUP BY department;
```
### SUM()
- Returns the total sum of a numeric column.
- Ignores NULL values.
``` sql
-- Find total sales per location
SELECT location, SUM(sales) AS total_sales
FROM company
GROUP BY location;
```
### MIN()
- Returns the minimum value in a group.
``` sql
-- Find the lowest salary in each department
SELECT department, MIN(salary) AS min_salary
FROM company
GROUP BY department;
```
### MAX()
- Returns the maximum value in a group.
``` sql
-- Find the highest salary in each department
SELECT department, MAX(salary) AS max_salary
FROM company
GROUP BY department;
```
## Using ORDER BY With GROUP BY
- When you use GROUP BY, SQL collapses rows into groups first.
- After that, ORDER BY sorts that reduced result set of groups, not the original raw rows.
- You can sort by:
    - The grouped column(s) (department)
	  - Aggregate results (COUNT(*), SUM(salary))
	  - Even expressions.
``` sql
SELECT department, COUNT(*) AS total
FROM employees
GROUP BY department
ORDER BY total DESC;

-- After GROUP BY department:
-- department total
-- IT          2
-- HR          1
-- Sales       3

-- After ORDER BY total DESC:
-- department total
-- Sales       3
-- IT          2
-- HR          1

```
## HAVING Keyword
- Purpose: Filters groups after they are formed by the GROUP BY clause.
- Works like WHERE, but instead of filtering individual rows before grouping, it filters entire groups after aggregation.
- Commonly used with aggregate functions (e.g., COUNT(), SUM(), AVG()), because WHERE cannot use aggregate functions directly.
- **Difference between WHERE and HAVING**
   - WHERE → filters individual rows before grouping.
   - HAVING → checks each group’s aggregated results, and either keeps the whole group or removes it.
``` sql
SELECT department, COUNT(*) AS emp_count
FROM company
GROUP BY department
HAVING COUNT(*) > 5;
-- HAVING COUNT(*) > 5 → keeps only departments with more than 5 employees.

-- Syntax with WHERE clause
SELECT <column-name>
FROM <table-name>
WHERE <condition>
GROUP BY <column-name>
HAVING <condition>
ORDER BY <column-name> 
```




## VIEWS
- A view is a virtual table based on the result of a SQL query.
- It does not store data itself (by default) — it just stores the SQL query.
- When you query a view, the underlying SQL runs and fetches results.

## Why use views?
- Simplify queries → write complex queries once, then just use the view.
- Security → hide sensitive columns (like salary) and expose only selected ones.
- Abstraction → underlying table structure can change, but the view remains the same.
- Reusability → multiple users/programs can reuse the same view.

## Creating View
``` sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;

CREATE VIEW IT_Employees AS
SELECT EmpID, EmpName, Salary
FROM Employee
WHERE Dept = 'IT';

-- query it like table
SELECT * FROM IT_Employees;
```
## Updating Data Through A View
- If the view is simple (based on one table, no aggregations), you can INSERT, UPDATE, DELETE through it.
- If it is complex (joins, group by, distinct, etc.), usually you cannot update directly.
``` sql
UPDATE IT_Employees
SET Salary = Salary + 5000
WHERE EmpID = 101;
-- This updates the base Employee table as well.
```

## Dropping a View
``` sql
DROP VIEW IT_Employees;
```
## Types Of Views
### Simple View 
- created from one table, no functions/aggregations.
### Complex View
-  created using multiple tables, joins, or functions.
### Materialized View (in Oracle/Postgres, not MySQL by default)
-  actually stores data (snapshot), improves performance for large queries.

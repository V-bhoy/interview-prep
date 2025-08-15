## JOINS
- A JOIN in SQL is used to combine rows from two or more tables based on a related column between them.
- This related column is usually a primary key in one table and a foreign key in another.

## INNER JOIN
- Returns only rows where there is a match in both tables.
- Use Case: Find matching records.
``` sql
SELECT Orders.order_id, Customers.customer_name
FROM Orders
INNER JOIN Customers
ON Orders.customer_id = Customers.customer_id;

-- only the matching records are in the result set
-- inner join is also written as JOIN

SELECT o.order_id, c.customer_name
FROM Orders as o
INNER JOIN Customers as c
ON o.customer_id = c.customer_id;
-- using alias for table names

SELECT s.*, sp.*, p.*
FROM Supplier s
INNER JOIN SP sp 
ON s.Sno = sp.Sno
INNER JOIN Product p 
ON sp.Pno = p.Pno;
-- join on 3 tables

-- Table A ●●●●●
-- Table B ●●●●●
-- Result  ●● (only intersection)
```
## LEFT JOIN (LEFT OUTER JOIN)
-  Returns all rows from the left table and matched rows from the right table.
-  If no match, NULLs are returned for right table columns.
-  Use Case: Get all records from Table A, even if they don’t have matches in Table B.
``` sql
-- syntax
SELECT Customers.customer_name, Orders.order_id
FROM Customers
LEFT JOIN Orders
ON Customers.customer_id = Orders.customer_id;

-- Table A ●●●●●
-- Table B   ●●
-- Result  ●●●●● (all from left, NULLs for no match)
```
## RIGHT JOIN (RIGHT OUTER JOIN)
-  Returns all rows from the right table and matched rows from the left table.
-  If no match, NULLs are returned for left table columns.
-  Use Case: Get all records from Table B, even if they don’t have matches in Table A.
``` sql
-- syntax
SELECT Orders.order_id, Customers.customer_name
FROM Orders
RIGHT JOIN Customers
ON Orders.customer_id = Customers.customer_id;

-- Table A   ●●
-- Table B ●●●●●
-- Result  ●●●●● (all from right, NULLs for no match)
```
## FULL JOIN (FULL OUTER JOIN)
- Returns all rows from both tables. NULLs where there is no match.
- Use Case: Get a complete dataset from both sides.
``` sql
-- syntax
SELECT Customers.customer_name, Orders.order_id
FROM Customers
FULL JOIN Orders
ON Customers.customer_id = Orders.customer_id;

-- IN MY SQL, we dont have full join keyword so we use UNION
SELECT p.ProjectID, p.ProjectName, e.EmpFname, E.EmpLname, e.EmailID
FROM Project p LEFT JOIN Employee e ON p.EmpID = e.EmpID;
UNION
SELECT p.ProjectID, p.ProjectName, e.EmpFname, E.EmpLname, e.EmailID
FROM Project p RIGHT JOIN Employee e ON p.EmpID = e.EmpID;

-- Table A ●●●●
-- Table B   ●●●●
-- Result  ●●●●●● (everything)
```
## CROSS JOIN
-  Returns the Cartesian product of two tables (every row of A with every row of B).
-  Use Case: Useful for generating combinations.
``` sql
SELECT Customers.customer_name, Products.product_name
FROM Customers
CROSS JOIN Products;
-- If A has 3 rows, B has 4 rows → result = 3×4 = 12 rows
```
## SELF JOIN
- Join a table with itself.
- Use Case: Find relationships within the same table (e.g., employee-manager hierarchy).
``` sql
SELECT E1.name AS Employee, E2.name AS Manager
FROM Employees E1
LEFT JOIN Employees E2
ON E1.manager_id = E2.employee_id;
```

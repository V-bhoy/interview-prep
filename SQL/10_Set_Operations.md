## SET OPERATIONS
- In SQL, set operations are used to combine the results of two or more SELECT queries into a single result set.
- hey work on rows (sets), not columns, and each query must have the same number of columns with compatible data types.
## Why do we need set operations?
- distinct rows
- no duplicates in the result set

## Difference Between Joins And Sets
- Joins
   - combines tables based on matching condition
   - combines result via columns in horizontal way
   - number of columns and data types can be different for both tables
   - can generate distinct & duplicate rows
- Sets
   - combines select queries result sets
   - combines result via rows in verical way
   - number of columns and data types must be same for both tables
   - generates distinct rows

## Rules for Set Operations
- All set operators have equal precedence.
- Both queries must have the same number of columns.
- Columns must have compatible data types.
- Column names in the result come from the first query.
- ORDER BY applies to the final combined result.

## UNION
- Combines results from two queries and removes duplicate rows.
``` sql
SELECT city FROM customers
UNION
SELECT city FROM suppliers;
-- A list of unique cities from both customers and suppliers.

-- using WHERE
SELECT item_name, price FROM shop_1 WHERE price > 25
UNION
SELECT item_name, price FROM shop_2 WHERE price > 25;

SELECT item_name, item_type, price FROM shop_1
UNION
SELECT item_name, item_type, price FROM shop_2
ORDER BY price DESC;
-- items present in both shops
```
## UNION ALL
- Combines results but keeps duplicates.
``` sql
SELECT city FROM customers
UNION ALL
SELECT city FROM suppliers;
-- All cities from both tables, including duplicates.

SELECT EmpFName, EmpLName, EmpCode FROM Empdept1
UNION ALL
SELECT EmpFName, EmpLName, EmpCode FROM Empdept2
ORDER BY EmpCode;
-- employees in both departments, including duplicates.
```
## INTERSECT
- Returns only rows that are common to both queries.
``` sql
SELECT city FROM customers
INTERSECT
SELECT city FROM suppliers;
-- Cities that exist in both customers and suppliers.

In MYSQL, we do not have INTERSECT keyword, we enumerate using INNER JOIN
SELECT DISTINCT e1.*
FROM Empdept1 e1
INNER JOIN Empdept2 e2
ON e1.EmpCode = e2.EmpCode;
-- DISTINCT removes duplocates in case of mupltiple copies in tables.

-- same can be written as
SELECT DISTINCT e1.*
FROM Empdept1 e1
INNER JOIN Empdept2 e2
USING(EmpCode);
```
## MINUS 
- Returns rows from the first query that do not appear in the second query.
``` sql
SELECT city FROM customers
EXCEPT
SELECT city FROM suppliers;
-- Cities that are in customers but not in suppliers.

-- MySQL doesn’t support MINUS or EXCEPT directly.
-- Using LEFT JOIN … IS NULL
SELECT e1.id, e1.name
FROM Empdept1 e1
LEFT JOIN Empdept2 e2 ON e1.id = e2.id
WHERE e2.id IS NULL;

-- same can be written as
SELECT e1.id, e1.name
FROM Empdept1 e1
LEFT JOIN Empdept2 e2 USING(id)
WHERE e2.id IS NULL;
```


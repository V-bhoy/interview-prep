## Indexing
- Indexing is a data structure technique used to speed up retrieval of records from a database table.
- Without an index: DBMS performs a full table scan (checks every row).
- With an index: DBMS can jump directly to the required row(s).

## How Index Works?
- An index is an additional data structure (usually a B-Tree or Hash Table) that stores sorted values of one or more columns and pointers to the actual rows in the table.
- An index is created on one or more columns of a table.
- DBMS maintains an index file separate from the actual data file.
- Index file contains search keys + pointers to the data rows.
``` sql
-- Suppose we have a table:
CREATE TABLE Students (
  StudentID INT PRIMARY KEY,
  Name VARCHAR(50),
  Age INT,
  City VARCHAR(50)
);

SELECT * FROM Students WHERE Name = 'Vaishali';
-- Queries Without Index
-- DBMS scans all rows.

CREATE INDEX idx_name ON Students(Name);
-- Queries With Index
-- DBMS jumps directly to ‘Vaishali’ using B+ Tree.

-- For every row in the index table:
-- 	1.	The value of the indexed column(s).
--	2.	A pointer (ROWID or address) to the actual row in the table.
Index (B-Tree):
+---------+----------+
| StudentName | ROWID    |
+---------+----------+
| Alice   | → Row#1  |
| Bob     | → Row#2  |
| Charlie | → Row#3  |
| David   | → Row#4  |
-- so the index file contains a sorted list and a pointer to where that row lives in the table.
-- If you create index on one column → It stores that column’s values for all rows.
-- 	If you create composite index (multiple columns) → It stores combinations of those column values.
CREATE INDEX idx_emp_dept_salary
ON Employee(Department, Salary);
-- Then the index will store (Department, Salary) pairs in sorted order + row pointers.
```
##  Data Structures Used in Indexing
	•	B+ Tree (most common) → balanced, supports range queries.
	•	Hash Index → best for equality searches (=).
	•	Bitmap Index → used in data warehouses for low-cardinality columns (e.g., Gender = M/F).

## NOTE
- By default, DBMS only creates:
	•	A primary key index (automatically, since primary keys must be unique).
	•	Any unique constraints also get indexes automatically.
- For anything else, you manually decide which columns to index based on your query patterns.

## Advantages of Indexing

- ✅ Faster SELECT queries.
- ✅ Efficient range queries and sorting.
- ✅ Reduces I/O operations.

## Disadvantages of Indexing

- ❌ Extra space needed for index file.
- ❌ Slows down INSERT, UPDATE, DELETE because index must be updated.
- ❌ Too many indexes = overhead.

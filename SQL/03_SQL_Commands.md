## Types of SQL Commands
- DDL (Data Definition Language)
- DQL/DRL (Data Query Language)
- DML (Data Manipulation Language)
- DCL (Data Control Language)
- TCL (Transaction Control Language)

## DDL (Data Definition Language)
- define, modify, and manage the structure of database objects
- generally auto-committed — meaning changes are permanent and cannot be rolled back once executed.
### CREATE
- used to create new database objects like table, database, view, indexes or stored procedures.
- constraints like PRIMARY KEY, FOREIGN KEY, UNIQUE, and CHECK can be defined while creating the table.
``` sql
-- create database
CREATE DATABASE CompanyDB;

-- create table
CREATE TABLE Employees (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50) NOT NULL,
    DeptID INT,
    Salary DECIMAL(10,2)
);
```
### ALTER
- Used to modify the structure of an existing database object (mostly tables).
- we can change data type of column or add/remove columns
- can add or drop constraints
- rename column
``` sql
-- Add a new column
ALTER TABLE Employees ADD Email VARCHAR(100);

-- Modify data type
ALTER TABLE Employees MODIFY Salary DECIMAL(12,2);

-- Rename column
ALTER TABLE Employees RENAME COLUMN EmpName TO EmployeeName;

-- Drop a column
ALTER TABLE Employees DROP COLUMN Email;
```
### DROP
- Used to permanently delete a database object along with all its data and structure.
``` sql
-- Drop a table
DROP TABLE Employees;

-- Drop a database
DROP DATABASE CompanyDB;

-- This is irreversible — all stored data will be lost.
```
### TRUNCATE
- Used to remove all rows from a table but keep its structure intact.
- Faster than DELETE because it does not log individual row deletions and cannot have a WHERE clause.
- Auto-increment counters reset to initial values.
- Cannot be rolled back in many DB systems (auto-commit).
``` sql
TRUNCATE TABLE Employees;
```
### RENAME
- Used to rename tables, databases, or columns (depending on DB system).
``` sql
-- Rename a table
RENAME TABLE Employees TO Staff;

-- Rename a database (MySQL does not support directly; must create and move objects)
ALTER DATABASE old_db_name MODIFY NAME = new_db_name; -- Works in some DBMS
```
## DQL/DRL (Data Query Language / Data Retrieval Language)
- used to retrieve data from tables without modifying it.
### SELECT
``` sql
SELECT column1, column2, ...
FROM table_name
[WHERE condition]
[GROUP BY column_name(s)]
[HAVING condition]
[ORDER BY column_name(s) ASC|DESC]
[LIMIT number];
```
1.	SELECT → Specifies the columns to be retrieved.
2.	FROM → Specifies the table from which data will be fetched.
3.	WHERE → Filters rows based on a condition.
4.	GROUP BY → Groups rows that have the same values in specified columns.
5.	HAVING → Filters groups after grouping is applied (similar to WHERE but used with aggregate functions).
6.	ORDER BY → Sorts the results in ascending (ASC) or descending (DESC) order.
7.	LIMIT → Restricts the number of rows returned (in MySQL, PostgreSQL).

**Examples**

``` sql
-- fetch all data from table
SELECT * FROM employees;

-- fetch data of specific columns
SELECT first_name, last_name, salary FROM employees;

-- using where clause
SELECT first_name, last_name, salary 
FROM employees
WHERE department = 'IT';

-- fetch data and sort by highest salary first
SELECT first_name, last_name, salary 
FROM employees
ORDER BY salary DESC;

-- find avg salary for each department
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;

-- show departments having more than 5 employees
SELECT department, COUNT(*) AS total_employees
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;

-- limit results
SELECT first_name, last_name
FROM employees
LIMIT 3;
```
## DML (Data Manipulation Language)
- DML commands are used to manipulate data stored in database tables.
- They allow you to insert new records, update existing records, and delete unwanted records.
- These operations modify the actual data but not the database structure.
### INSERT
- Used to add new records (rows) into a table.
``` sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

-- Insert a new employee record into the Employees table
INSERT INTO Employees (EmployeeID, Name, Department, Salary)
VALUES (101, 'Amit Sharma', 'IT', 55000);
```
### UPDATE
- Used to modify existing records in a table.
- Always use a WHERE clause when updating, to avoid changing all rows.
``` sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

-- Increase the salary of employee with EmployeeID 101
UPDATE Employees
SET Salary = 60000
WHERE EmployeeID = 101;
```
### DELETE
- Used to remove existing records from a table.
``` sql
DELETE FROM table_name
WHERE condition;

-- Remove employee record with EmployeeID 101
DELETE FROM Employees
WHERE EmployeeID = 101;
```
## DCL (Data Control Language)
- used to control access and permissions to the database.
- They define who can access the data and what actions they are allowed to perform.
### GRANT
- Gives specific privileges to a user or role on database objects (like tables, views, schemas).
``` sql
-- syntax
GRANT privilege_type ON object_name TO user_name;

-- Give SELECT and INSERT permission on Employees table to user 'vaishali'
GRANT SELECT, INSERT ON Employees TO 'vaishali';
```
### REVOKE
- Removes previously granted privileges from a user or role.
``` sql
-- syntax
REVOKE privilege_type ON object_name TO user_name;

-- Remove INSERT permission from user 'vaishali'
REVOKE INSERT ON Employees FROM 'vaishali';
```
### Common Privileges in DCL:
	•	SELECT – Read data from a table/view.
	•	INSERT – Add data into a table.
	•	UPDATE – Modify existing data in a table.
	•	DELETE – Remove data from a table.
	•	ALL PRIVILEGES – Gives all possible permissions.

## TCL (Transaction Control Language)
- used to manage transactions in a database.
- A transaction is a group of SQL statements that are executed as a single unit.
- TCL ensures data consistency and allows rolling back changes if something goes wrong.
### COMMIT
- Saves all the changes made by the current transaction permanently in the database.
``` sql
INSERT INTO Employees (id, name, salary) VALUES (1, 'Vaishali', 50000);
COMMIT; -- Changes are saved permanently
```
### ROLLBACK
- Undoes all changes made by the current transaction, restoring the database to its previous state.
``` sql
INSERT INTO Employees (id, name, salary) VALUES (2, 'Amit', 60000);
ROLLBACK; -- Changes are undone
```
### SAVEPOINT
- Creates a point inside a transaction to which you can later roll back, without affecting earlier changes.
``` sql
INSERT INTO Employees VALUES (3, 'John', 70000);
SAVEPOINT sp1;

INSERT INTO Employees VALUES (4, 'Sara', 80000);
ROLLBACK TO sp1; -- Undo only Sara's insert, John's insert remains
```
### SET TRANSACTION
- Configures the transaction properties such as read/write mode or isolation level.
``` sql
-- syntax
SET TRANSACTION [READ WRITE | READ ONLY];

-- example
SET TRANSACTION READ ONLY;
```
### TCL Workflow Example
``` sql
START TRANSACTION;

INSERT INTO Orders VALUES (101, 'Laptop', 55000);
SAVEPOINT before_discount;

UPDATE Orders SET price = price - 5000 WHERE id = 101;

ROLLBACK TO before_discount; -- undo discount
COMMIT; -- save only the insert
```
## NOTE
- whether autocommit mode is enabled depends on the database system.
### Autocommit ON (Default in MySQL, SQL Server, etc.)
- Every individual SQL statement is automatically committed right after it executes successfully.
- You don’t have to explicitly type COMMIT.
- Once committed, the changes cannot be rolled back.
``` sql
-- check autocommit
SELECT @@autocommit; -- 1 means ON, 0 means OFF
-- Turn off autocommit in MySQL
SET autocommit = 0; -- now you must explicitly COMMIT or ROLLBACK
```
### Autocommit OFF (Default in Oracle, PostgreSQL)
- Changes are not saved permanently until you explicitly run COMMIT.
- If you exit the session or run ROLLBACK, the uncommitted changes are lost.
- For transaction control (TCL) to make sense, autocommit must be OFF.
---
### Concept of dual tables
- allows to use SELECT command without using FROM clause or having table
- these are dummy tables that are already created by MySQL itself.
- The significance of dual tables is that we can make temporary changes without disturbing the user-defined tables.
- You can find the current time of the system, can perform mathematical
calculations using dual tables, convert the string from lower-case to
upper-case and vice-versa, etc
``` sql
-- syntax
SELECT <STATEMENT_TO_EXECUTE>;

SELECT 1000 + 100;
-- o/p = 1100

SELECT ucase(“coding ninjas”);
-- o/p = CODING NINJAS
-- Other keywords - NOW(), current_timestamp(); will display time.
```

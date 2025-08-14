## ADD
- used to add new column in existing table
``` sql
ALTER TABLE employees 
ADD department VARCHAR(50);

-- adds column before salary
ALTER TABLE employees 
ADD department VARCHAR(50)
FIRST salary;

-- adds column after salary
ALTER TABLE employees 
ADD department VARCHAR(50)
AFTER salary;

ALTER TABLE employees
ADD department   VARCHAR(50) AFTER salary,
ADD join_date    DATE AFTER department,
ADD bonus        DECIMAL(10,2) FIRST;
-- MySQL adds the column at the end by default
```
## CHANGE
- used to change the column name and optionally its data type at the same time
``` sql
ALTER TABLE employees 
CHANGE COLUMN emp_name full_name VARCHAR(100);
```
## MODIFY 
- used to change the column data type (or attributes) without changing its name.
``` sql
ALTER TABLE employees 
MODIFY salary DECIMAL(10,2);
```
## DROP
- used to drop column / remove column from a table
``` sql
ALTER TABLE employees 
DROP COLUMN department;
```
### NOTE:
- DELETE - DML command
    - Removes one, some or all the records in the table.
    - can be rolled back to prev state
    - Is a slow operation
- DROP - DDL command
    -  Removes the entire table structure. 
    -  cannot be rolled back
    -   Relatively faster
- TRUNCATE - DDL command
    -  Removes all the records from the table, not the structure
    -  cannot be rolled back
    -   Fastest of all.
      
## RENAME
- used to rename table / column
``` sql
ALTER TABLE employees 
RENAME TO staff;

ALTER TABLE employees 
RENAME COLUMN fname TO first_name;
```
## Information Schema 
- We have an in-built view in MySQL called information_schema
-  which holds all details about the constraints on a particular table
- INFORMATION_SCHEMA provides access to information about the MySQL server, such as database
metadata, database or table names, column data types, and permissions.
``` sql
-- General form:
SELECT COLUMN_NAME, CONSTRAINT_NAME, REFERENCED_COLUMN_NAME,
REFERENCED_TABLE_NAME
FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_NAME = 'table_name';
```

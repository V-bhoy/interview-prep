## INSERT
- used to insert records in a table
``` sql
-- syntax
INSERT INTO table_name (col1, col2, col3, ...)
VALUES (val1, val2, val3, ...),
       (val4, val5, val6, ...); -- Multiple rows at once

-- Column list is optional if you’re inserting into all columns in order:
INSERT INTO employees
VALUES (1, 'John Doe', 50000);

-- Multiple rows insert saves time and improves performance
INSERT INTO employees (id, name, salary)
VALUES (1, 'John Doe', 50000),
       (2, 'Jane Smith', 60000);

-- Default values can be used:
INSERT INTO employees (id, name)
VALUES (3, 'Mike Ross'); -- salary will be default if defined

-- Can also insert using SELECT:
-- copies records from employees to archive_employees
INSERT INTO archive_employees (id, name, salary)
SELECT id, name, salary FROM employees WHERE active = 0;
```
## UPDATE 
- Used to modify existing data in one or more records in a table.
- Generally used with WHERE clause otherwise all rows will be updated
- UPDATE only allows one SET clause per statement 
``` sql
-- Syntax
UPDATE <table-name>
SET col1 = new_val1,
    col2 = new_val2
WHERE <condition>;

-- update single column
UPDATE employees
SET salary = 55000
WHERE id = 3;

-- update multiple columns
UPDATE employees
SET salary = 60000,
    department = 'HR'
WHERE id = 5;

-- update multiple rows
-- Marks all Sales employees as inactive.
UPDATE employees
SET active = 0
WHERE department = 'Sales';

-- Without WHERE condition
-- This will set active = 0 for all employees which is risky
UPDATE employees
SET active = 0;

-- update the age of all students by 1 
UPDATE University SET Age = Age + 1;
```
## DELETE

## RENAME

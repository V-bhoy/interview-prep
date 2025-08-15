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
- used to delete records from existing table
- does not reset auto increment on deletion
- can be rolled back to the prev state if inside a transaction.
- Safe Updates Mode is a setting in some database clients (like MySQL Workbench) that prevents you from running UPDATE or DELETE without a WHERE clause or a key filter. You can easily enable or disable it.
- It’s a safety mechanism to avoid accidentally modifying or deleting all rows in a table.
``` sql
-- syntax
DELETE FROM table_name
WHERE condition;
-- if you omit the WHERE clause, all rows in the table will be deleted (be careful!).

DELETE FROM BankAccount
WHERE Id = 2;
-- This deletes the row where Id is 2.

DELETE FROM BankAccount;
-- Deletes every record in the table but keeps the table structure.

START TRANSACTION;
DELETE FROM BankAccount WHERE Id = 2;
COMMIT;       -- permanent
ROLLBACK;     -- ❌ does nothing now

SET autocommit = 1; -- default
START TRANSACTION;  -- overrides autocommit until commit/rollback
DELETE FROM BankAccount WHERE Id = 2;
ROLLBACK;           -- ✅ works here
```
## REPLACE
- used as combination of INSERT and UPDATE
- If the row does not exist (based on a primary key or unique key), it inserts it.
- If the row already exists (same primary key/unique key), it deletes the existing row and then inserts the new row.
``` sql
REPLACE INTO table_name (col1, col2, col3)
VALUES (val1, val2, val3);

CREATE TABLE Users (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);

INSERT INTO Users VALUES (1, 'Vaishali', 25);

-- If we do REPLACE
REPLACE INTO Users (id, name, age)
VALUES (1, 'Vaishali Bhoyar', 26);
-- It inserts the new row with updated values.

REPLACE INTO Users SET id = 1, name = 'Alice', age = 26;
-- works same

REPLACE INTO Users (id, name, age)
SELECT id, name, age FROM customer WHERE id = 1;
-- works same
```
- it is not same as ON DUPLICATE KEY UPDATE
``` sql
INSERT INTO Users (id, name, age)
VALUES (1, 'Vaishali Bhoyar', 26)
ON DUPLICATE KEY UPDATE
name = VALUES(name), age = VALUES(age);
-- this will directly update the existing row
-- it does not delete the old row first and then insert a new row
```

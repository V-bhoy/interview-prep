## Constraints
- Constraints in SQL are rules applied to table columns to enforce data integrity, meaning they control the type, format, and relationships of the data stored.
- They prevent invalid data entry, maintain consistency, and ensure accuracy.
- In SQL, constraints can be applied to both tables and columns, but how and where you define them depends on the type of constraint.
## Column-level Constraints
- Defined right after a column’s definition in the CREATE TABLE or ALTER TABLE statement.
- Apply only to that column.
``` sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,        -- Primary Key constraint on emp_id column
    emp_name VARCHAR(100) NOT NULL, -- NOT NULL constraint only on emp_name column
    salary DECIMAL(10,2) CHECK (salary > 0) -- CHECK constraint for salary column
);
```
## Table-level Constraints
- Defined at the end of the column definitions.
- Can apply to one or more columns together.
- Useful for multi-column constraints like composite keys or foreign keys.
``` sql
CREATE TABLE orders (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id), -- Table-level composite primary key
    FOREIGN KEY (product_id) REFERENCES products(id) -- Table-level foreign key
);
```
## PRIMARY KEY
- unique and not null
- used to uniquely identify each row
- each table must have only one primary key,  but it can consist of multiple columns (called a composite primary key).
- Automatically creates a unique index for fast lookups.
``` sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100) NOT NULL,
    salary DECIMAL(10,2)
);

CREATE TABLE orders (
    order_id INT,
    product_id INT,
    quantity INT,
    PRIMARY KEY (order_id, product_id)
);
-- Uniqueness is enforced on the combination of (order_id, product_id).
```
## FOREIGN KEY
- used to establish relationship between two tables
- Refers to the PRIMARY KEY (or UNIQUE key) of another table.
- Ensures referential integrity — meaning you cannot insert a value in the child table that doesn’t exist in the parent table.
- You can have multiple foreign keys in a table.
- Can be defined at column level or table level.
``` sql
-- parent table
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL
);

-- child table
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);

-- parent table
CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);

-- child table
CREATE TABLE grades (
    student_id INT,
    course_id INT,
    grade CHAR(2),
    FOREIGN KEY (student_id, course_id)
        REFERENCES enrollment(student_id, course_id)
);
-- the foreign key must include both columns.
-- You cannot reference only one part of the composite key unless that part is also unique in the parent table.
-- if UNIQUE(student_id) was mentioned in the parent table, then it could be used for referencing.
```
## NOT NULL
- restricts the values to be not null
- Applied at column level.
- ensures data correctness
``` sql
CREATE TABLE employee (
    id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,  -- must always have a name
    department VARCHAR(50)
);
```
## UNIQUE
- Ensures all values in a column (or a combination of columns) are different.
- Can be applied to a single column or multiple columns (composite unique key).
- Allows NULL values, but the rule is:
   - Each UNIQUE column can have only one NULL (per table) —
     because NULL is treated as an “unknown” value, and SQL considers all unknowns different,
     but most RDBMS still restrict to one in a UNIQUE column.
``` sql
CREATE TABLE employee (
    id INT PRIMARY KEY,
    email VARCHAR(100) UNIQUE  -- No two employees can have the same email
);

CREATE TABLE enrollment (
    student_id INT,
    course_id INT,
    UNIQUE (student_id, course_id) -- No student can enroll in the same course twice
);
```
## CHECK
- Ensures that values in a column meet a specific condition before they are inserted or updated.
- If the condition evaluates to FALSE, the INSERT or UPDATE fails.
- Can be applied to a single column or multiple columns.
- Multiple CHECK constraints can be applied on the same table.
``` sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    age INT CHECK (age >= 18) -- Employees must be at least 18
);

CREATE TABLE products (
    id INT PRIMARY KEY,
    price DECIMAL(10,2),
    discount DECIMAL(10,2),
    CHECK (discount <= price) -- Discount cannot be greater than price
);
-- named check constraint
CREATE TABLE students (
    id INT PRIMARY KEY,
    marks INT,
    CONSTRAINT chk_marks CHECK (marks BETWEEN 0 AND 100)
);

```
- CHECK is evaluated per row, not across rows.
- If you need to enforce conditions involving multiple rows (e.g., sum of salaries in a department), you cannot use CHECK — you would need a trigger or business logic in your application.
- CHECK can be combined with other constraints like NOT NULL, UNIQUE, DEFAULT.

## DEFAULT
- Used to assign a default value to a column when no value is explicitly provided during an INSERT.
- Helps avoid NULL values for optional columns.
- Can be applied to any data type (string, number, date, boolean, etc.).
- Works well with NOT NULL to ensure a column always has some value.
``` sql
CREATE TABLE logs (
    id INT PRIMARY KEY,
    log_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
## AUTO_INCREMENT / SERIAL
- database-specific constraint/feature
- used to automatically generate a unique sequential value for a column (usually for primary keys).
``` sql
CREATE TABLE students (
    student_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL
);

CREATE TABLE users (
    user_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    username TEXT
);

CREATE TABLE users (
    user_id INT GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
    username TEXT
);
```















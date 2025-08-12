## SQL Data Types
- represents the type and space allocated to the value stored in attribute columns
---
### String Data Types
-	Non-binary → stored as characters (text)
- Binary → stored as raw bytes (no character set conversion)
- It can be of fixed or variable length.
---
### CHAR
- string (0-255) --> size is 0-255
- fixed size of memory is allocated (pads with spaces if shorter)
- non-binary string (stored in form of character)
### VARCHAR
- string (0-255) --> size is 0-255
- variable size of memory is allocated
- non-binary string
### TEXT
- Stores large non-binary text strings.
- Variants:
  - TINYTEXT: 0–255 characters
  - TEXT: 0–65,535 characters
  - MEDIUMTEXT: 0–16,777,215 characters
  - LONGTEXT: 0–4,294,967,295 characters
- Variable length (despite “fixed” wording sometimes used — storage depends on content length).
### BLOB
- binary large object
- Stores binary data (images, audio, video, files, etc.).
- Variants:
  - TINYBLOB: 0–255 bytes
  - BLOB: 0–65,535 bytes
  - MEDIUMBLOB: 0–16,777,215 bytes
  - LONGBLOB: 0–4,294,967,295 bytes
- Variable length (no text collation, raw bytes stored).
### BINARY (0-255)
- Range: n = 0–255 bytes
- Fixed-length binary data (pads with \0 if shorter).
### VARBINARY
- Range: n = 0–65535 bytes (depends on storage limits)
- Variable-length binary data (stores only required bytes + length byte).
---
### Numeric Data Types
- Whole numbers (integers) or decimal numbers
- Signed (positive + negative) or Unsigned (only positive)
---
### INT
- By default, it stores signed numbers
- Range (Signed): -2,147,483,648 to 2,147,483,647
- Range (Unsigned): 0 to 4,294,967,295
- Storage: 4 bytes
- Used for whole numbers (IDs, counts, etc.)
- Variants
   - TINYINT
       - Storage: 1 byte
       - Range (Signed): -128 to 127
       - Range (Unsigned): 0 to 255
   - SMALLINT
       - Storage: 2 bytes
       - Range (Signed): -32,768 to 32,767
       - Range (Unsigned): 0 to 65,535
   - MEDIUMINT
       - Storage: 3 bytes
       - Range (Signed): -8,388,608 to 8,388,607
       - Range (Unsigned): 0 to 16,777,215
   - BIGINT
       - Storage: 8 bytes
       - Range (Signed): -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
       - Range (Unsigned): 0 to 18,446,744,073,709,551,615
### DECIMAL / NUMERIC
- Exact fixed-point number.
- Syntax: DECIMAL(p, s)
   - p = precision (total digits)
   - s = scale (digits after decimal point)
- Example: DECIMAL(10, 2) → max 10 digits, with 2 after decimal (e.g., 12345678.90)
- Stored as string of digits internally → no rounding errors → best for money.
### FLOAT
- Approximate floating-point number (single precision, ~7 digits )
- Storage: 4 bytes
- Can store very large/small numbers but may cause rounding errors
- Range: ~ -3.402823466E+38 to 3.402823466E+38
- Signed range: Same positive range
### DOUBLE
- Approximate floating-point number (double precision, ~15 digits )
- Storage: 8 bytes
- More precision than FLOAT
- Range: ~ -1.7976931348623157E+308 to 1.7976931348623157E+308
- Signed range: Same positive range
### BIT
- Stores bit-field values (1 to 64 bits)
- Example: BIT(1) → true/false (1 or 0), BIT(8) → can store values from 0 to 255
- BIT(n) --> ranges from 0 to 2^n-1
---
### Date & Time Data Types
- used to represent date and time values
---
### DATE
- format: yyyy-mm-dd
- storage: 3 bytes
- range: 1000-01-01 to 9999-12-31
- Use case: Birth dates, due dates, event dates where time of day is irrelevant.
### TIME
- format: hh:mm:ss
- storage: 3 bytes
- Range: -838:59:59 to 838:59:59 (can represent durations longer than 24 hours)
- Use case: Store opening hours, durations, time intervals.
### DATETIME
- format: yyyy-mm-dd hh:mm:ss[.fraction]
- storage: 8 bytes (MySQL 5.6+; earlier versions used 5 bytes)
- Range: 1000-01-01 00:00:00 to 9999-12-31 23:59:59
- Can include fractional seconds up to microseconds (DATETIME(6)).
- Use case: Storing full timestamp values for events, transactions, or logs without timezone conversion.
### TIMESTAMP
- format: yyyy-mm-dd hh:mm:ss[.fraction]
- Storage: 4 bytes (MySQL 5.6+ allows fractional seconds, increasing size slightly)
- Range: 1970-01-01 00:00:01 UTC to 2038-01-19 03:14:07 UTC (affected by Year 2038 problem)
- Stored in UTC internally; automatically converted to the session’s time zone for display.
- Special feature: Can auto-update when a row changes (DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP).
- Use case: Track record creation and update times across time zones.
### YEAR
- format: yyyy
- Storage: 1 byte
- Range: 1901 to 2155 (or 0000 for “zero” year)
- Use case: Store only the year part (e.g., manufacturing year, graduation year).
---
### Boolean Data Type
- used to represent boolean values
---
### BOOLEAN
- In MySQL, BOOLEAN is a synonym for TINYINT(1).
- Stored as an integer where 0 = FALSE and 1 = TRUE.
- Can be constrained with CHECK constraints for stricter enforcement.
- Use case: Flags, status indicators, yes/no answers.
---
## Advanced Data Types
### SPATIAL Data Types
	•	Used to store geometric and geographic data such as points, lines, and polygons.
	•	Examples: POINT, LINESTRING, POLYGON, MULTIPOINT, MULTIPOLYGON, GEOMETRY.
	•	Supports spatial indexing for faster queries (when using MyISAM or InnoDB with SPATIAL INDEX).
	•	Use case: Mapping applications, GIS systems, location-based services.
### JSON
	•	Stores JSON documents in an optimized binary format (from MySQL 5.7+).
	•	Allows validation to ensure only valid JSON is stored.
	•	Supports functions for querying and manipulating JSON (JSON_EXTRACT, JSON_SET).
	•	Use case: Store semi-structured or flexible schema data (e.g., user preferences, metadata).
 ### ENUM (Advanced String Data Type)
	•	Stores one value from a predefined list of strings.
	•	Stored internally as integers mapping to string values.
	•	Use case: Fixed categories like ('Small', 'Medium', 'Large').
 ### SET (Advanced String Data Type)
	•	Stores zero or more values from a predefined list of strings.
	•	Useful for representing multiple boolean flags in a single field.

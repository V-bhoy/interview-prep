### What is a schema?
- structure or blueprint of database that defines how the data is organized, stored, and rekated.
- It tells
    - what tables exist
    - what columns are in each table
    - what are the data types
    - what are the relationships between tables
    - what are the constraints
 
### Difference betweeen data model and schema
- data model designs the logic and rules of how data should be stored and accessed
- schema defines the design of the actual database as per the chosen data model
- data model design is abstract and focuses on how data shoould be represented and related
- schema design is concrete and focuses on what the database should contain used to actually build it.

### Types of schema
- **Physical Schema**
   - The physical database schema represents how the actual data is stored on disk storage.
   - That is the actual code that will be used to create the structure of your database.
- **Logical schema**
   - A logical database schema represents how the data is organized in tables.
   - It explains how attributes from tables are linked to each other.
   - For creating a logical schema, we use ER Model technique.
- **View Schema**
   - the view schema describes the database design at view level which describes how the user interacts with the database
   - describes virtual tables created by queries (views)

 ### Advantages
 - A database schema can be easily transferred to another user.
 - It enables the transfer of database objects between schemas.
 - Data can be managed independent of physical storage.

### Difference between database and database schema
- The database contains interrelated data
- Database schema is a structural view of data
- DB contains the data while DB schema does not contain any data of its own
- Data Changes while schema does not change

### 3 Schema Architecture
- framework for database systems that separates the database into 3 levels to provide data abstraction, independence and security
- changes in schema of any one layer doesn't affect others
- **External Level (View level)**
   - contains multiple user views
   - each view only shows the relevant data for that user
   - hides the rest of the database
   - example: a student sees only their marks and courses, while the admin can see all student records.
- **Conceptual Level (Logical Level)**
   - describes entire database structure
   - includes entities, data types, constraints and relationships
   - independent of physical storage
   - example: tables like students, courses and their relationships.
- **Internal Level (Physical Level)**
   - deal with how the data is actually stored in memory/disks
   - includes file formats, indexing, compression, access paths.
   - example: a table is stored in B-tree indexed file in blocks of 4KB on SSD.

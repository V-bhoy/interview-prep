### What is abstraction?
- To expose only what is needed. The rest of the part is hidden.
- example: the car mechanisms are hidden and only the parts to operate are exposed.

### NOTE
- The major purpose of DBMS is to provide users an abastract view of the data.
- To simplify user interaction with the system, abstraction is applied through several levels of abstraction.
- This is achieved via 3-schema architecture

### 3 Schema Architecture
- The main objective of three-level architecture is to enable multiple users to access the same data with a personalized view while storing the underlying data only once.
- it also ensures physical data independence --> any change at physical level does not affect data represented at logical level.
- **Internal Level (Physical Level)**
   - lowest level of abstraction
   - deal with how the data is actually stored in memory/disks
   - low-level data structures are used.
   - has physical schema that describes physical structure of DB.
   - we must define algorithms that allow efficient access to data.
   - example: a table is stored in B-tree indexed file in blocks of 4KB on SSD.
- **Conceptual Level (Logical Level)**
   - describes what kind of data is stored and the existing relationships among them.
   - it doesn't care about how the data will be stored at physical level.
   - the conceptual schema (logical schema) describes the design of the database at a logical level. (mapping physically stored data and represent it in form of tables)
   - example: tables like students, courses and their relationships.
- **External Level (View level)**
   - highest level of abstraction
   - simplifies user interaction with the system by providing different view to different end-user.
   - Each view schema describes the database part relevant to particular users and hides the remaining database.
   - a security mechanism is also provided to prevent users from accessing certain parts of DB
 
### What is DB instance?
- The collection of information stored in the database at a particular time is know as DB instance.

### What is a schema?
- structure or blueprint of database that defines how the data is organized, stored, and related.
- It tells
    - what tables exist
    - what columns are in each table
    - what are the data types
    - what are the relationships between tables
    - what are the constraints

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

- Logical schema is the most important as programmers use this design to implement the database and applications

### Data Model
- way to describe the design of DB at logical level.
- underlying structure of DB is the data model.
- ex: ER model, relational model etc.

 
### Difference betweeen data model and schema
- data model designs the logic and rules of how data should be stored and accessed
- schema defines the design of the actual database as per the chosen data model
- data model design is abstract and focuses on how data shoould be represented and related
- schema design is concrete and focuses on what the database should contain used to actually build it.

### Difference between database and database schema
- The database contains interrelated data
- Database schema is a structural view of data
- DB contains the data while DB schema does not contain any data of its own
- Data Changes while schema does not change


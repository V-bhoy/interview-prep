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

### Database Languages
- You need a language to interact with the databases.
- **Data Definition Language (DDL)**
    - used to specify the database schema
    - involves consistency constraints to be checked every time DB is updated
- **Data Manipulation Language (DML)**
    - used to specify the database queries and updates.
    - Involves
        - retrieval of data
        - insertion of new data
        - deletion of data
        - updating existing data
- Practically, both the languages are part of single DB language like SQL.

### How does the application access database?
- through APIs
- through an interface that allows communication between two entities
- example: JDBC in java, allows Java application to interact with database.

### Database Administrator (DBA)
- has control of both data and the programs that access those data
- functions:
     - schema definition
     - storage structire and access methods
     - schema modifications
     - authorization control
     - routine maintenance
          - periodic backups
          - security pathes
          - upgrades

### DBMS Application Architecture
- **T1 tier architecture**
   - client, server and database exist in the same machine
- **T2 tier architecture**
   - partitioned into 2 components
   - client and DB interacts over an interface like JDBC
   - client sends direct queries to the database and fetches data
- **T3 tier architecture**
   - partitioned into 3 logical components
   - client is just frontend and doesn't contain direct DB calls.
   - client communicates to the app server and app server communicates with the DB system to access data.
   - Advantages:
       - stability due to distributed applicaton server
       - minimal chances of data corruption since app server acts as a middle layer between client and DB
       - increased security since client does not have direct access to DB
  




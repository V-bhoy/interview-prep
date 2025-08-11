## Relational Model
- organizes data in the form of relation (table)
- consists of collection of tables each having a unique name.
- row represents releationship among set of values and table is a collection of such relationships
- tuple -> single row of table / a unique record
- columns -> represents attributes of relation, having permitted value, also called domain of the attribute.
- relation schema -> defines the design and structure of relations
- RM based DBMS --> RDBMS --> IBM, MySQL, PostgreSQL etc.
- Degree of table --> number of attributed/columns in a relation (table).
- Cardinality --> number of tuples in a relation
- Relational key --> set of attributes that uniquely define each tuple

## Properties of Relation (Table)
- name of relation is distinct among all other relations
- values have to be atomic, cannot be broken down further
- name of each attribute must be unique
- each tuple must be unique
- sequence of row and column has no significance
- tables must follow integrity cinstraints, helps to maintain data consistencu across all tables.

## Relational Model Keys
### Super Key
- Any combination of attributes that can uniquely identify each tuple.
### Candidate Key
- minimum subset of super key, which can uniquely identify each tuple.
- It conatins no redundant attribute.
- Value shouldn't be null
### Primary Key
- selected out of candidate key, it has least number of attributes.
- unique and not null
### Alternate Key
- All candidate key except candidate key
### Foreign Key
- creates relationship between 2 tables
- R1 relation includes primary key of relation R2 which is called the foreign key of R1 referencing R2.
- Relation R1 is called referencing (child) relation while R2 is called referenced (parent) relation.
- can have null values indicating that its referenced tuple does not exist
### Composite Key
- primary key with at least 2 attributes
### Compound Key
- primary key formed using 2 foreign key
### Surrogate Key
- synthetic primary key
- generated automatically by DB, usually an integer value
- may be used as primary key

## Integrity Constraints
- CRUD operations must be done with some integrity policy so that DB is always consistent
- introduced so that we do not accidently corrupt the DB
- the operation is not performed if the constraint fails
### Domain Constraints
- restricts the value in the attribute by specifying the domain
- restricts data type of every attribute
- example: enrollment should happen for candidate birth year < 2002
### Entity Constraints
- every relation should have primary key thst is not null.
### Referential Contraints
- **Insert Constraint**
  - an insert operation cannot be performed in the child if the reference value is not present in the parent table.
- **aDelete Constraint**
  - a delete operation cannot be performed in the child if the reference value is present in the parent table or vice versa.
  - we can delete a parent key tuple without violating the delete constraint by using
     - ON DELETE CASCADE where the child tuple is automatically deleted when the parent tuple is deleted.
     - ON DELETE NULL where the child tuple foreign key is set to null when the parent tuple is deleted.
### Key Constraints
- **NOT NULL**
   - restricts the attribute value to be null
- **UNIQUE**
   - ensures all values in a column/attribute are unique
- **DEFAULT**
   - sets default value if no value is specified
- **CHECK**
   - checks condition before an insert/update operation else throws error
- **PRIMARY KEY**
   - checks if the value is unique and not null
   - a realtion can only have one primary key
- **FOREIGN KEY**
   - creates relationship between 2 tables
   - prevents every actions which can result in loss of connection between tables
 
  ## Converting ER Diagran to Realtional Model

  ### Strong Entity
  - becomes individual table with entity name, and attributes as its columns
  - The primary key in an entity becomes the relation's PK
  - FK is added to establish realtionship with other relations

  ### Weak Entity
  - becomes individual table with entity name, and attributes as its columns
  - The primary key in its corresponding strong entity becomes the relation's foregin key
  - PK is composite - (FK + partail discrimination key)

  ### Single Valued Attribute
  - represented as column directly

  ### Composite Attribute
  - handled by creating a separate attribute for each part of the composite attribute 
  - example: Address -> define separate columns fort street, house , city etc.

  ### Multivalued attribute
  - new table is created with attribute name
  - The primary key of the original table is used as foreign key in the new table
  - PK is composite - (FK + partail discrimination key)

  ### Derived Attribute
  - not considered in the table
 
  ### Generalisation
  - **METHOD 1**
     - create table for higher level as well as lower level entities
     - The foreign key of lower level entities will be the primary key of higher level entity.
  - **METHOD 2**
     - create table for lower level entities
     - Add columns for higher entity into lower entities.
     - Drawbacks --> duplicate data stored in relations and if there is some data which doesn't belong
       to lower level entities but a part of it belongs to higher level entity, such data could not be
       represented by second method

  ### Aggregation
  - Table of the relationship set is made.
  - Attributes includes primary keys of entity set and aggregation set’s entities.
  - Also, add descriptive attribute if any on the relationship.
  - example: table --> emp_id job_id branch_id
  - 
  ### Unary Relationship
  - Add an extra column for foreign key referencing the same table.


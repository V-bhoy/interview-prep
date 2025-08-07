### ER Model (Entity Relationship Model)
- it is the graphical representation of database design.
- a high level data model that describes data in terms of entities, attributes and
relationships

### Entity
- Entity is a real world object,class, person or place.
-  Entities can be uniquely identified. It has a physical existence.
- It is represented by a rectangle.
- Example – any customer who has taken a Loan from the bank could be an entity

### Entity Set
- Set of entities of the same type at a particular point of time is known as the entity set.
- Example – customer and loan are the entity sets.
- **Strong Entity Set**
   - An entity set which is not dependent on any other entity set in the schema is known as a strong entity set i.e. a strong entity set will always have a primary key.
   - It is represented with a rectangle.
- **Weak Entity Set**
   - A weak entity set is usually dependent on a strong entity set to ensure its existence and it does not have any primary key
   - contains a discriminator or a partial key to differentiate between the records present in the weak entity set table.
   - It is represented with a double rectangle.
   - It needs to have participation.
- Example:  customer is strong entity set and Loan is weak entity set because without a customer there is no existence of loan
- loan entity set has total participation i.e. every loan must have at least one customer.

### Attributes
- Properties of the entity are known as attributes.
- Each attribute has some value.
- An entity can contain multiple attributes.
- They are represented by eclipse.
- example: cust_id, cust_name, cust_city, cust_acc, dob, phone_no, loan_id and income are attributes of customer entity set.

### Types of attributes
- Based on composition
- **Simple Attributes**
    - an attribute that cannot be divided further
    - example: cust_acc is a simple attribute.
- **Composite Attributes**
    - an attribute that can be divided into further parts
    - example: cust_name is a composite attribute because it is further divided into Fist_name, Middle_name and Last_name.
- Based on count of values that can be stored
- **Single Valued Attributes**
    - attribute has only one value
    - example: cust_id is a single valued attribute
- **Multi Valued Attributes**
    - attribute has more than one value
    - It is represented by a double oval
    - example: cust_email can be multi valued attribute
- Based on how attribute value can be stored
- **Stored Attributes**
    - The initial information which we save in our database
    - example:  DOB is a stored attribute.
- **Derived Attributes**
    - The value which we can derive from stored attributes 
    - example: Age is a derived attribute because it can be derived from DOB.
- **Complex Attributes**
    - an attribute has multivalued and composite components
    - example: address is a complex attribute
- **Null Values** - It represents something which is unknown.

### Keys in ER Diagram
- An attribute or set of attributes which can uniquely identify a record is known as keys.
### Types of keys
- **Primary Key**
    - uniquely identifies each entity in the entity set.
- **Foreign Key**
    - Whenever there is some relationship between two entities there must be some common attribute between them.
    - the primary key of an entity set and will become foreign key of another entity set
    - represented  with a dashed underlining.
    - example: loan_id is foreign key in the customer entity set and the
    discriminator or Partial key(won’t call it a Primary key) in the loan entity set.

### Relationships
- It defines how two or more entities are connected with each other.
- It is an association among two or more entities.
- It is represented by a diamond operator in the ER diagram.
- It is of two types:
   - Strong Relationship - The relationship between two independent entities is a strong
relationship.
   - Weak Relationship - When a relationship exists between a weak entity and its owner entity, represented by double diamond.

### Degree of Relationships
- Number of entities participating in a single relationship.
- **Unary Relationship**
    -  only one entity participates in a relationship
    -  example: an employee could be a manager also, so the
       manager manages other employees, and all types of employees are in a
       single entity. Therefore the relationship here is unary relationship.
- **Binary Relationship**
    - two entities participate in a relationship
    - example: student enrolls in a course
- **Ternary Relationship**
    - there is an association among three entities.
    - example: an employee and a project are alotted to a department

### Cardinality Ratio
- It refers to the number of entities to which another entity can be
associated through a relationship set.
- For Binary Relationship, four types: –
- **One To One**
    - If only one instance of an entity is associated with only one instance of
another entity.
    - example: A person has aadhaar card and vice-versa
- **One To Many**
    - a single instance of an entity is associated with more than one instance of
another entity.
    - example: A customer can have multiple bank accounts.
    - An entity in Consumer is associated with zero or more entities in
Account. An entity in Account is associated with at most one entity in
Consumer
- **Many To One**
    - more than one instance of an entity is associated with a single instance
of another entity.
    - example: one product could have multiple orders.
    - An entity in Order is associated with at most one entity in Product. An
entity in Product is associated with one or more entities in Order.
- **Many To Many**
    - more than one instance of an entity is associated with more than one instance
of another entity.
    - example: customer nuys products.
    - An entity in Customer is associated with many entities in Product. An
entity in Product is associated with many entities in Customer.

### Participation Constraints
-  also called minimum cardinality constraint
-  **Partial Participation**
     - It specifies that not all entities are involved in the relationship
instance.
     - shown by using a single line
-  **Total Participation**
     - It specifies that each entity must be involved in at least one
relationship instance, therefore it is also called as mandatory
participation
     - shown by using a double line
     - example: every loan must be associated with a customer

### Enhancements for increase in complexity
- SPECIALIZATION
- it is the procedure to splitting up the entities into further sub entities on the basis of their
functionalities, specialities and features.
- In Specialisation, schema size increases.
- GENERALIZATION
- the sub entities are combined together resulting in the
formation of a parent entity set on the basis of some common features
- example: e entities like guitar, piano, violin, drums, flute are
generalized into a single parent entity, named Instrument
- It optimizes the database, by making it simpler.
- Data repetition is also avoided, as now there won’t be no need to
mention the same attributes or data in different tables/relation.
- In Generalization, schema size shrinks.
- AGGREGATION
- used when we need to express a relationship among relationships.

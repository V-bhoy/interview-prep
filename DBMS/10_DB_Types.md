## Relational DB (RDBMS)
	•	Model: Based on relational model (tables, rows, columns).
	•	Storage: Data stored in tables with relationships.

	•	Features:
	•	SQL for queries.
	•	Strong ACID compliance.
	•	Well-suited for structured data.
	•	High consistency & reliability.

	•	Advantages:
	•	Optimized for structured data.
	•	Mature ecosystem & community.

	•	Disadvantages:
	•	Horizontal scalability is difficult.
	•	Becomes complex with huge datasets.

	•	Examples: MySQL, PostgreSQL, Oracle, SQL Server.

⸻
## Object-Oriented DB (OODBMS)
	•	Model: Based on OOP (Objects, Classes, Inheritance).
	•	Storage: Data stored as objects (like in programming).

	•	Features:
	•	Objects interact via methods.
	•	Can model complex data directly.
	•	Good for multimedia, CAD, simulations.

	•	Advantages:
	•	Easy mapping between real-world entities and database.
	•	Efficient for applications needing object persistence.

	•	Disadvantages:
	•	Not widely used (less community support).
	•	Slower CRUD with very complex structures.

	•	Examples: db4o, ObjectDB, Versant.

⸻

## NoSQL DB
	•	Model: Non-relational (Document, Key-Value, Column, Graph).
	•	Storage: Schema-free, flexible.

	•	Features:
	•	Great for big data, real-time applications.
	•	Scales horizontally.
	•	Supports semi-structured/unstructured data.

	•	Advantages:
	•	Flexible schemas.
	•	Can handle huge volumes of data.
	•	Faster writes, high scalability.

	•	Disadvantages:
	•	May sacrifice consistency (CAP theorem trade-off).
	•	Redundant data (denormalization).

	•	Examples: MongoDB (document), Cassandra (column), Redis (key-value), Neo4j (graph).

⸻
## Hierarchical DB
	•	Model: Tree-like structure (Parent → Child).
	•	Storage: Each record has one parent, but can have multiple children.

	•	Features:
	•	Navigation through hierarchy (like file system).
	•	Data retrieval is fast for hierarchical queries.

	•	Advantages:
	•	Good for one-to-many relationships.
	•	Efficient for hierarchical data (e.g., org charts, file systems).

	•	Disadvantages:
	•	Rigid structure → difficult to modify schema.
	•	Poor flexibility for complex relationships.
	•	Examples: IBM IMS, Windows Registry.

⸻
## Network DB
	•	Model: Graph-like with records and set-based relationships.
	•	Storage: Each record can have multiple parent and child relationships.

	•	Features:
	•	Uses pointers/links to represent relationships.
	•	More flexible than hierarchical model.

	•	Advantages:
	•	Good for many-to-many relationships.
	•	Efficient for traversing complex networks.

	•	Disadvantages:
	•	Complex implementation & navigation.
	•	Hard to scale compared to relational & NoSQL.

	•	Examples: IDMS, Raima Database Manager.

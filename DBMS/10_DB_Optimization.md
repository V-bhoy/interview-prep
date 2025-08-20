- Huge data
   - Storage full
   - increased response time due to high incoming requests
   - maybe system crash due to heavy work load
- Solution:
- Scale up --> increase hardware but costly.
- Clustering & Replication
- Partitioning (scale out - horizontal scaling)
- Sharding

## Clustering/Replication
- having multiple servers (nodes) working together as a single database system.
- The goal is usually high availability and load balancing.
- high availability --> if one server is shut down, the other server is still available.
- load balancing --> Distributing incoming requests across multiple servers so that no single server is overloaded.
### 🔹 Load Balancing in Databases
	•	Reads: Often load-balanced → requests are spread across replicas.
	•	Writes: Usually go to a single master (to maintain consistency).
	•	With clustering, all nodes might be active, so LB distributes both reads & writes.

### Active-Active Clustering
	•	All DB nodes are active and can process read/write queries.
	•	Load is distributed among them.
	•	Needs careful handling of concurrency & consistency.
	•	Example: Oracle RAC (Real Application Clusters).
### Active-Passive Clustering
	•	One DB node is active (handles requests), others are standby (idle, waiting).
	•	If the active node fails → passive node takes over (failover).
	•	Simpler, but doesn’t scale reads/writes as much.
### ✅ Use Case:
	•	Mission-critical systems where zero downtime is required.
	•	Banking, healthcare, large-scale enterprise apps.

## Replication
 -  copying database data from one server (primary) to another (secondary) in real-time or near real-time.
 -  Goal: data redundancy, disaster recovery, performance optimization.
### Master-Slave Replication
	•	Master node handles writes.
	•	Slave nodes handle reads (read scaling).
	•	Data changes are replicated from master → slaves.

### Master-Master Replication
	•	Both nodes can accept read & write.
	•	Each one replicates changes to the other.
	•	Needs conflict resolution.

### Log-Based / Incremental Replication
	•	Changes in DB logs are streamed to replicas.
	•	Example: MySQL binlog replication, PostgreSQL WAL shipping.

### ✅ Use Case:
	•	Read-heavy apps (social media, analytics, e-commerce).
	•	Disaster recovery (backup in another region).
	•	Geographical distribution (users closer to nearest replica).

## Partitioning
- splitting a single large table (or index) into smaller, more manageable pieces (partitions).
- The DBMS still sees it as one table, but data is stored in chunks.
- Improves query performance, especially when you only need a subset of data.
### Horizontal Partitioning (most common)
- Rows are divided based on a rule (e.g., users with id 1–1M in Partition A, 1M–2M in Partition B).
- Each partition has the same columns but different rows.
- Example: A users table split by geographic region.
### Vertical Partitioning
- Columns are divided.
- Example: In a users table →
  - Partition A = frequently used columns (id, name, email)
	-	Partition B = rarely used columns (profile_pic, bio, settings)
### Range Partitioning
- Based on a range of values.
- Example: Orders from Jan–Mar in one partition, Apr–Jun in another.
### Hash Partitioning
- Use a hash function on a key.
- Example: user_id % 4 → puts data in 4 partitions.

## Sharding
-  a special form of horizontal partitioning where partitions (shards) are stored on different servers.
-  Each shard is a self-contained DB.
-  Together, all shards represent the full dataset.
-  Used for scalability across multiple machines.
```
📌 Example of Sharding:
	•	You have 1 billion users.
	•	If all are in one DB server, it becomes slow.
	•	Shard by region:
	•	Shard 1 → Users from Asia
	•	Shard 2 → Users from Europe
	•	Shard 3 → Users from America

Now, queries for Asian users hit only Shard 1 → faster, scalable.
```
### How They Improve Performance
- Partitioning: Queries scan less data (only relevant partition).
- Sharding: Distributes load across multiple servers → avoids bottlenecks.
### In Short:
- Partitioning = split data within a single database.
- Sharding = split data across multiple databases/servers.

## When to use partitioning & sharding?
🔹 Use Partitioning (inside 1 DB server) when:
	1.	Data is large, but still fits on one server
	•	Example: A few hundred million rows in one table.
	•	Partitioning keeps queries efficient by scanning only a subset.
	2.	Queries usually target a subset of data
	•	Example: Orders table → queries are usually “last 3 months only.”
	•	Range partitioning by date speeds this up.
	3.	You want better maintenance & performance
	•	Easier to archive/drop old partitions.
	•	Backups and indexing become faster.

📌 Example:
	•	E-commerce orders table with 5 years of data.
	•	Most queries look at recent 6 months → use range partitioning by date.

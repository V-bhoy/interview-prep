## CAP Theorem
- C --> Consistency
- A --> Availability
- P --> Partition Tolerance

## Consistency
- data across all node machines should be same
- a read operation on any node should return the value of most recent write operation
- all users should see the same data at same time regardless the node they are connected
- a write operation on a single node, should be replicated across other nodes in the system

## Availability
- system remains operational all the time
- every req will get a response regardless of the individual status of the node
- there is no guarantee that the reponse is the most recent write operation

## Partition Tolerance
- partition --> break in communication between nodes
- the system does not fail even if msgs are dropped or delayed between nodes.
- To have partition tolerance - the system ust replicate records across combination of nodes and networks.

## CAP Theorem Definition 
- it states that, a distributed system can only provide two of three properties simultaneously. T
  The theorem formalises the tradeoff between consistency and availability when there's a partition.
  Meaning, if there is a communication break, either consistency is lost / availability is lost.
- all three properties are established if a single node is present in the system.
- a distributed system with consistency and availability is a hypothetical thought, since there are high chances of partition.
- CP database --> enables partition and consistency but no availability. When a partition occurs, the system has to turn off all the
  inconsistent nodes until the partition can be fixed. Example: MongoDB. The system is structured such that there is only one primary
  node for write operations in a replica set. The secondary nodes replicate the data from the primary node, so if the primary node fails
  teh secondary node can stand-in. Availability is not as important as consistency.
- AP database: enables availability and partition tolerance but not consistency. If partition occurs, all nodes are available but thet are
  not all updated.When the partition is eventually resolved, teh nodes are in sync to ensure consistency. ex: Apache Cassandra (nosql DB)


## BASE Properties
- 👉 Definition: BASE stands for:
  - Basically Available
	- Soft state
  - Eventual consistency
- It’s used in distributed, NoSQL databases (like Cassandra, DynamoDB, MongoDB) where high availability and scalability are prioritized over strict consistency (CAP theorem).
### Basically Available
	- The system guarantees availability even in case of failures.
	- It may return a stale or partial response instead of failing.
	- Example: In Amazon DynamoDB, even if one replica is down, the system still serves data from another replica.
### Soft State
	- The system’s state may change over time, even without new input.
	- Because replicas sync asynchronously, data may temporarily differ across nodes.
	- Example: A write request in Cassandra might take time to propagate to all nodes → during this time, the state is “soft”.
### Eventual Consistency
	- The system does not guarantee immediate consistency.
	- Instead, it guarantees that if no new updates are made, all replicas will eventually converge to the same state.
	- Example: In a social media feed, your post might not immediately appear to all friends, but eventually everyone sees it.
 - ACID → reliability, strict rules (banking, finance).
 - BASE → flexibility, availability, scale (social networks, large-scale apps).

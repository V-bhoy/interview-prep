- A master–slave architecture is a replication model where:
- Master (Primary) → handles writes (and sometimes reads).
- Slave(s) (Replica/Secondary) → handle reads (and get updates from master asynchronously or synchronously).

- ## How it works?
- Write request → goes to Master DB.
- Replication → Master pushes changes to Slaves.
- Synchronous replication → Slaves must confirm before write is committed. (Strong consistency but slower).
- Asynchronous replication → Master writes immediately, slaves catch up later. (High availability but eventual consistency).
- Read request → can go to Slaves to reduce load on Master.

## ✅ Advantages
- Scalability → read-heavy workloads distributed across slaves.
- High Availability → if master fails, one slave can be promoted as new master.
- Backup & Reporting → slaves can be used for backups or analytics without affecting master performance.

## Disadvantages
- Replication Lag (in async mode) → slaves may serve stale data.
- Single point of failure → if master crashes and no failover is set, writes stop.
- Complexity → managing failover, consistency, and promotion is tricky.

## Use Cases
- MySQL / PostgreSQL Replication → master handles writes, slaves handle reads.
- Redis Sentinel → manages failover in master–slave setups.
- Kafka → leader (master) and follower (slave) partitions.

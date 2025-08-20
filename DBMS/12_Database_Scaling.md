## When to scale?
- huge data
- huge incoming requests

## Issue
- slow app performance
### API Latency
- time taken for an API request to travel from the client to the server,
  get processed, and return the response back to the client.
- It’s usually measured in milliseconds (ms).
- It includes: 
- Network Latency
    - Time taken for the request to travel across the internet.
	  - Influenced by distance (client ↔️ server), routing, congestion.
- Processing Time
    - Time taken by the backend/server to execute the request.
	  - Includes DB queries, business logic, authentication, caching.
- Serialization/Deserialization
    - Converting request/response between formats (e.g., JSON ⇄ Object).
- Load Balancer / Middleware Delay
    - If request goes through API gateways, proxies, or middlewares, they add extra milliseconds.
- Low latency = fast, smooth user experience
- High latency = slow apps, timeouts, poor UX
- For most APIs:
    - <100 ms = Excellent
	  - 100–500 ms = Acceptable
	  - >1s = Noticeable lag
### How to Reduce API Latency
### Query Optimization & Connection Pool
- cache frequently used non dynamic data like booking history, payment history, user profile etc on client side.
- join queries take more time due to heavily normalized database, so, introduce data redundancy (or maybe use noSql)
- everytime creating a new connection to DB is costly, and time consuming, so create a connection pool, to reuse the old connections again. Use connection pool libraries like Cache DB connections.
### Vertical Scaling
- upgrade hardware server machine
- RAM by 2x, SSD by 3x etc.
- More you scale up, cost increases exponentially.
### Command Query Responsibility Segregation (CQRS)
- used when the upgraded machine is not able to handle read/write requests.
- add 2 more machines as replica to the primary machine
- All read requests read from replicas while write requests are done on primary
- The replicas replicate the data from ptimary time to time
- Now what if primary is not able to handle all write requests?
  This increases the lag between data replication and results into poor performance impacting user experience.
### Multi Primary Replication
- all machines can work as primary/replica.
- we had 3 machines (1 peimary and 2 replicas), now we treat all three as primary/replica
- The multi primary configuration is a logical circular ring.(server 2 replicates server 1, server 3 replicates server 2, server 1 replicates server 3)
- we write data to any node
- we broadcast read request among 3 nodes and read data from node that replies first
- Now number of requests/sec increases? Now how to scale?
### Partition Data By Functionality
- separate the data by location in diffferent database/ different machines with primary-replica or multi primary replication configuration
- it can be categorized based on the functionality as well
- Con: Backend / Application layer has to take the responsibility to join the results
- the business is scaled across india?
### Horizontal Scaling
- Sharding - multiple shards
- Allocate 50 machines- all have same DB schema, but each machine holds just a part of data
- the local data should be there in the machine.
- each machine can have its own replica for failure recovery
- sharding is generally hard to apply.
- the business is scaled across world?
### Data Center Wise Partition
- Requests travelling across continents has high latency
- Distribute traffic across data centers
- Establish data centers across continents
- Partition data based on the region across those data center
- Enable cross data replication for disaster recivery and maintain high availability

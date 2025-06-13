---
created: 2023-08-25 19:26 
modified: Friday 25th August 2023 19:26:36
alias: 
---
up::  [[system-design]]
tags:: 
related: 

## Design Key Value Store

### What is it?
- Key value database, non-relational (no SQL) like Amazon DynamoDB. Each unique identifier is stored as a key with its associated value. This data pairing is known as a “key-value” pair.

### Functional Requirements
1. put(key, value) insert value with associated key
2. get(key) get value with associated key\

### Non-Functional Requirements:
1. The size of key value pair must be small
2. Ability to store big data
3. High available, system to responds to every request even when there are errors
4. Highly scalable, the system can support a large data set
5. Automatic scaling, the addition/deletion of servers should be automatic based on traffic
6. Tunable consistency
7. Low latency: time for a request to receive a response 
## Single Server
1. Store the key-value pairs in a hash table, keeping everything in memory
2. Although memory access will be fast, it will be impossible to fit all the data into a single machine. This solution is not scalable and if we want to support big data we need a distributed key value store with many machines. 

### Distributed Key Value Store
[[CAP Theorem]]
**Consistency:** All clients see the same data at the same time no mater which node they read from
**Availability:** Every request gets response without errors even in the presence of failures 
**Partition Tolerance:** when a node goes down, the system can continue to operate
### Data Partitioning
1. For large applications we cannot store all the system in a single server, therefore we must split the data into partitions and then distribute them across multiple servers.
2. We can use **consistent hashing** to partition the data.
	**Automatic scaling:** servers can be added and removed automatically depending on the load
	**Heterogeneity:** the number of virtual nodes for a server is proportional to the server capacity. For example, servers with higher capacity are assigned with more virtual nodes.

### Data Replication
To achieve high availability and reliability, data must be replicated over N servers.  
After a key is mapped to a position in the hash ring, walk clockwise from the position and choose the first unique N servers on the ring to store data copies. The replicas should be placed in different data center for better reliability![[Screenshot 2023-08-26 at 12.10.04 PM.png]]
### Consistency
Quorum reads and writes can guarantee consistency for both read and write operations 
N = The number of replicas  
W = A write quorum of size W. For a write operation to be considered as successful, write operation must be acknowledged from W replicas.  
R = A read quorum of size R. For a read operation to be considered as successful, the read operation must wait for responses from at least R replicas.
![[Screenshot 2023-08-26 at 12.22.33 PM.png]]
The configuration of W, R and N is a typical tradeoff between latency and consistency.
**If W or R > 1,** the system offers **better consistency**; however, the query will be slower **because** the coordinator must wait for the response from the slowest replica.
**If R = 1 and W = N,** the system is optimized for a fast read.
**If W = 1 and R = N,** the system is optimized for fast write.
**If W + R > N,** strong consistency is guaranteed (Usually N = 3, W = R = 2). because there must be at least one overlapping node that has the latest data to ensure consistency.
**If W + R <= N,** strong consistency is not guaranteed.
### Consistency Models:
• Strong consistency: any read operation returns a value corresponding to the result of the most updated write data item. A client never sees out-of-date data.
	Strong consistency is usually achieved by forcing a replica not to accept new reads/writes until every replica has agreed on current write. This approach is not ideal for highly available systems because it could block new operations.

• Weak consistency: subsequent read operations may not see the most updated value.

• Eventual consistency: this is a specific form of weak consistency. Given enough time, all updates are propagated, and all replicas are consistent.
### How does inconsistency resolution versioning work?
Versioning and vector locks are used to solve inconsistency problems. 
  
1. Versioning: Versioning involves assigning a unique identifier or timestamp to each update or modification made to a piece of data. When a replica or node modifies the data, it creates a new version with an updated identifier or timestamp. 2.2.
2. Conflict Detection: With versioning, it becomes possible to detect conflicts when multiple replicas attempt to modify the same data concurrently. Conflicts occur when two or more replicas have different versions of the same data and need to be resolved to maintain consistency.
### Failure Detection
**Gossip Protocol:**
• Each node maintains a node membership list, which contains member IDs and heartbeat counters.
• Each node periodically increments its heartbeat counter.
• Each node periodically sends heartbeats to a set of random nodes, which in turn propagate to another set of nodes.
• Once nodes receive heartbeats, membership list is updated to the latest info.
• If the heartbeat has not increased for more than predefined periods, the member is considered as offline.
![[Screenshot 2023-08-26 at 12.31.13 PM.png]]
- Node s0 maintains a node membership list shown on the left side.  
• Node s0 notices that node s2’s (member ID = 2) heartbeat counter has not increased for a long time.
• Node s0 sends heartbeats that include s2’s info to a set of random nodes. Once other nodes confirm that s2’s heartbeat counter has not been updated for a long time, node s2 is marked down, and this information is propagated to other nodes.
### How to handle temporary failures?
A technique called “sloppy quorum” [4] is used to improve availability. Instead of enforcing the quorum requirement, the system chooses the **first W healthy servers for writes** and **first R healthy servers for reads** on the hash ring. Offline servers are ignored
If a server is unavailable due to network or server failures, another server will process requests temporarily. When the down server is up, changes will be pushed back to achieve data consistency. This process is called **hinted handoff.**
### Handling Permanent Failures 
Anti-entropy protocol to keep replicas in sync. Anti-entropy involves comparing each piece of data on replicas and updating each replica to the newest version. A Merkle tree is used for inconsistency detection and minimizing the amount of data transferred.,
### System Architecture
![[Screenshot 2023-08-26 at 2.54.33 PM.png]]
Main features of the architecture are listed as follows:  
• Clients communicate with the key-value store through simple APIs: get(key) and put(key, value).  
• A coordinator is a node that acts as a proxy between the client and the key-value store. • Nodes are distributed on a ring using consistent hashing.  
• The system is completely decentralized so adding and moving nodes can be automatic. • Data is replicated at multiple nodes.  
• There is no single point of failure as every node has the same set of responsibilities.

As the design is decentralized, each node performs many tasks as presented in Figure 6-18.
![[Screenshot 2023-08-26 at 2.54.57 PM.png]]
### Write Path
![[Screenshot 2023-08-26 at 2.55.23 PM.png]]

1. The write request is persisted on a commit log file. 
2. Data is saved in the memory cache.
3. When the memory cache is full or reaches a predefined threshold, data is flushed to SSTable [9] on disk. Note: A sorted-string table (SSTable) is a sorted list of <key, value> pairs. For readers interested in learning more about SStable, refer to the reference material [9].
### Read Path
![[Screenshot 2023-08-26 at 2.55.54 PM.png]]
1. The system first checks if data is in memory. If it is in memory the data is returned to the client,t,If not, go to step 2. 
2. If data is not in memory, the system checks the bloom filter.
3. The bloom filter is used to figure out which SSTables might contain the key. 
4. SSTables return the result of the data set. 
5. The result of the data set is returned to the client.\

[System Design : Distributed Database System Key Value Store - YouTube](https://www.youtube.com/watch?v=rnZmdmlR-2M)
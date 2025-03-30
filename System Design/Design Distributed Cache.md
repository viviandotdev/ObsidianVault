---
created: 2023-07-21 09:57
modified: Sunday 23rd July 2023 17:04:50
alias:
---
up::  [[System Design MOC]]
tags:: #system-design
source:: [System Design Interview - Distributed Cache - YouTube](https://www.youtube.com/watch?v=iuqZvajTOyA)

# Design Distributed Cache


### What is a Distributed Cache?

![[distributed-cache-2023-07-21.excalidraw]]
A **distributed cache** improves application performance and scalability by **reducing the backend and server loads**. We can s**tore frequently accessed data** in the cache,  this allows for **faster retrieval** and reduces the need to fetch from slower data sources.
### Functional Requirements
`put (key, value)`
`get(key)`

### Non-Functional Requirements
**Scalable** (scales out easily together with increasing number of requests and data)
	Consistent hashing
**Available** (every request receives a response despite failures)
**Fault tolerant** (survives hardware / network failures)
**Performance** (fasts puts and gets)
	LRU Cache is highly performant and uses constant time operations
	Cache client picks a server in log(n) time
	Connection between cache client and cache server is done with TCP or UDP which is fast
**Accurate** (accurate data)


### Local Cache
1. Data is stored in memory on a hash table in a single server
    ![[Screenshot 2023-07-21 at 10.11.24 AM.png|700]]
2. What is a method for evicting old data when the storage is full?

   [[LRU cache Algorithm]]

### Distributed Cache

![[Screenshot 2023-07-21 at 10.18.59 AM.png]]

| Co-located Cache                        | Dedicated Cache Cluter                           |
| --------------------------------------- | ------------------------------------------------ |
| No extra hardware and operational costs | Flexibility in hardware                          |
| Scales together with service            | Isolation of resources between service and cache |
|                                         | Cache can be used by multiple services           |


### How does a service decide which cache hosts to call?

Consistent hashing
![[Screenshot 2023-07-21 at 10.20.08 AM.png|200]]
Hash ring is used to map keys and nodes

1. Hash function is applied to each key to generate a hash value
2. The hash ring is divided into a fixed function of equally sized partitions
3. Each node in the system in assigned to a position based on some criteria
4. To map each key to a node the key’s hash value is used to find the the next node in the a clockwise direction of the hash ring. This node is responsible for storing and serving the key.

Pros:
	When the number of nodes changes only a fraction on the keys need to be remapped
	This feature makes consistent hashing highly scalable and fault-tolerant, as it minimizes the need for redistributing a large amount of data across the system.

Caching Efficiency: Consistent hashing is beneficial for caching systems because it **reduces cache invalidation and the need to update large portions of the cache when nodes are added or removed**

[[Modular Hashing]]
### Who is actually making the selection?

The cache client is small libary that is integrated with the service and it is responsible for the cache hosts selection![[Screenshot 2023-07-21 at 10.22.45 AM.png|700]]

how do clients get the list of servers?

**Option 1 (Not Flexible)**
![[Screenshot 2023-07-21 at 10.25.22 AM.png|200]]

**We store a list of cache hosts in a file and deploy this file to service hosts using some continuous deployment pipeline. We can use configuration management tools such as chef and puppet to deploy file to every service host**

This is the simplest option. But not very flexible.
How is this list updated when a server dies or a new one is updated
Every time list changes, we need to make a code change and deploy it out to every service host.
The file is maintained manually

**Option 2 (Not Flexible)**
![[Screenshot 2023-07-21 at 10.25.42 AM.png|200]]
Specifically, we may put the file to the shared storage and make service hosts poll for the file periodically.
All service hosts try to retrieve the file from some common location, for example S3 storage service.
To implement this option, we may introduce a daemon process that runs on each service host and polls data from the storage once a minute or several minutes.

How is this list updated when a server dies or a new one is updated?

The drawback of this approach is that we still need to maintain the file manually. We need to make changes and deploy it to the shared storage every time cache host dies, or a new host is added.
**Option 3 (Configuration Service)**
![[Screenshot 2023-07-21 at 12.57.52 PM.png|200]]
Option 3 (Configuration Service)
Use a configuration service to monitor cache server health and if something bad happens to the cache server, all service hosts are notified and stop sending any requests to the unavailable cache server. And if a new cache server is added, all service hosts are also notified and start sending

Each cache server registers itself with the configuration service and sends heartbeats to the configuration service periodically. As long as heartbeats come, server is keep registered in the system. If heartbeats stop coming, the configuration service unregisters a cache server that is no longer alive or inaccessible.

Every cache client grabs the list of registered cache servers from the configuration service. The third option is the hardest from implementation standpoint and its operational cost is higher. But it helps to **fully automate the list maintenance**. And in a couple of minutes you will see one other benefit of using configuration service for a distributed cache.

### Improve availability and hot shard problem
![[Screenshot 2023-07-21 at 10.24.09 AM.png|700]]

**For each shard we will designate a master cache server and several read replicas.**

Replicase try to be the exact replica of the leader.

**Every time the connection between master and replica breaks, the replica attempts to automatically reconnect to the master. And replicas live in different data centers, so that cache data is still available when one data center is down. All put calls go through the master node, while get calls are handled by both the master node and all the replicas. And because calls to a cache shard are now spread across several nodes, it is much easier to deal with hot shards**

- Ho**w these leaders are elected.**

    C**onfiguration service**

    Configuration service is responsible for monitoring of both leaders and followers and failover, if some leader is not working as expected, configuration service can promote follower to leader. And as we discussed before, configuration service is a source of authority for clients. Cache clients use configuration service to discover all cache servers.

    Configuration service is a distributed service by its nature. It usually consists of an odd number of nodes (to achieve quorum easier), nodes are located on machines that fail independently (so that configuration service remains available in case for example network partitions) and all nodes talk to each other using TCP protocol. Zookeeper is a good candidate for a configuration service, we can use it here. Redis also implemented Redis Sentinel for this purpose.


### Additional Topics of Discussion

- Why do we favor performance and availability over consistency in a distributed cache?

    Caches should be designed to have low latency access. The purpose of the cache is to retrieve data quickly while compromising some accuracy.

    Since data is replicated asynchronously a get call from master may return different result from a get call processed for the same key be the replica.

    **Least recently used algorithm evicts data from cache when cache is full. But if cache is not full, some items may sit there for a long time.**

    And such items may become stale. To address this issue, we may introduce some metadata for a cache entry and include time-to-live attribute

    Passive vs Active Expiring

    **We can passively expire an item, when some client tries to access it, and the item is found to be expired. Or we can actively expire, when we create a maintenance thread that runs at regular intervals and remove them.**

    Use a probabilistic algorithm to test some random items on every run
- Local vs remote cache

    **If data is not found in the local cache, call to the distributed cache is initiated. To make life of service teams easier, so they do not need to deal with both caches, we can implement the support for a local cache in the cache client**
- Security

    Use firewall to restrict access to cache server ports.
- monitory and logging

    **What metrics we may want to emit: number of faults while calling the cache, latency, number of hits and misses, CPU and memory utilization on cache hosts, network I/O. With regards to logging we may capture the details of every request to the cache.**
- how can we simplify the cache client?

    client software should be simple.

    To simplify the cache client we can use a proxy that sites between cache clients and cache servers that will be responsible for picking a cache shard

    Another idea is to make the cache servers responsible for picking a shard, the client sends a request to a random cache server and the cache server applies consistent hashing and redirects requires to the shard that stores that data
- problems with consistent hashing

    Domino effect, cache servers do not split the circle evenly. when a server dies **And all of its load is transferred to the next server. This transfer might overload the next server, and then that server would fail, causing a chain reaction of failures.**

    **And to understand the second problem, remember how we placed cache servers on the circle. Some servers may reside close to each other and some may be far apart. Causing uneven distribution of keys among the cache servers. To deal with these problems, several modifications of the consistent hashing algorithm have been introduced.  One simple idea is to add each server on the circle multiple times.*

![[Screenshot 2023-07-21 at 10.23.46 AM.png]]

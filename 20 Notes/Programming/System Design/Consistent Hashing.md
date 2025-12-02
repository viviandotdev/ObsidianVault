---
created: 2023-12-07 17:00
modified: 2025-06-15T13:19:27-04:00

---
tags:: [[system-design]]

**What is consistent hashing?**
Consistent hashing, is a useful strategy for a [[Design Distributed Cache |distributed caching system]]. It allows us to distribute data across a cluster is such a way that we **minimize the amount of data that needs to be moved or remapped when nodes are added or removed.**
**Use case**
Consistent hash is a common method used by load balancers to balance the load across multiple servers.
**Use Case**
Distributed caching system. Given 'n' cache servers an simple hash function we can use is the [[Modular Hashing]]
1. However this is not scalable, because if a new cache host is added, all existing mappings are broken,

### Consistent Hashing Algorithm
A hash function maps a key to an integer. Suppose the output of the hash function is in the range 0 to 256.
	The choice of the hash function and the range of it outputs depends on performance, security and collision resistance.
	High ranges means lower collision, improved security however has high memory consumption and computational overhead
	Lower ranges means higher probability of collisions, load imbalance, but has lower computations costs
1. **Assign each node/server in the system to a position on the ring.**
	- Nodes should be evenly spaced in the ring to minimize data movement during node additions or removals. Evenly spaced nodes on the hash ring ensure a balanced distribution of keys across nodes, so that each node is responsible for approximately an equal portion of the hash space.
	![[Screenshot 2023-12-07 at 5.53.43 PM.png]]
1. To assign a key to node
	1. Map the key's value to it position on the ring.
	2. The node responsible for storing and serving the key is determined by finding the next node on the ring in the clockwise direction from the key's hash value.

![[Screenshot 2023-12-07 at 5.54.30 PM.png]]
**Node addition and removal**
1.  When a new node is added or a node is deleted only 'k/n' keys will need to be remapped, where 'k' is the total number of keys and 'n' is the total number of node. In a modular hashing system all keys would need to be remapped
2. When a **new host is added**, it takes its share from a few hosts without touching other’s shares.
	![[Screenshot 2023-12-07 at 6.07.47 PM.png]]
3. When a **host is deleted**, the keys that were previously mapped to the removed node are remapped to the closest next node on the ring in a clockwise direction.
	![[Screenshot 2023-12-07 at 5.55.07 PM.png]]

### Domino Effect Problem

The "Domino Effect Problem" in consistent hashing arises due to unevenly spaced nodes on the ring, leading to potential overload when nodes fail. This cascading failure happens as the load shifts to adjacent nodes, potentially causing a chain reaction of failures until all nodes shut down.

### Virtual nodes
Virtual nodes resolve this issue by replicating or hashing nodes multiple times in the ring. Each physical node now has several virtual nodes, expanding the number of hash slots for each node. This increased granularity balances key distribution, preventing excessive load on a single node and reducing the impact of node failures.
![[Screenshot 2023-12-07 at 6.08.16 PM.png]]

### Related
[[Modular Hashing]]

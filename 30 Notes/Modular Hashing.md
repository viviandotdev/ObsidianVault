---
created: 2023-12-07 17:05
modified: 2025-06-16T07:09:36-04:00

---
tags:: [[system-design]]
related:: [[Consistent Hashing]]
![[Screenshot 2023-07-21 at 10.22.11 AM.png|700]]

Modulo hashing, also known as simple hashing or standard hashing, uses a modulo operation to assign keys to nodes. Here's how it works:

1. Each node in the system is assigned an identifier or index, typically represented as a numeric value.
2. When a key needs to be mapped to a node, a hash function is applied to the key to generate a hash value.
3. The hash value is then divided by the total number of nodes in the system.
4. The remainder of the division (modulo operation) determines the index or identifier of the node responsible for storing and serving the key.

Scalability Challenges: When nodes are added or removed in a modulo hashing scheme, a significant portion of the keys will result in hash misses because the hash will produce entirely different cash hosts from before

Load Imbalance: Modulo hashing can result in uneven distribution of keys, especially when the distribution of keys is not uniform. If the keys are not evenly distributed, some nodes may receive a significantly higher load than others, leading to performance issues.

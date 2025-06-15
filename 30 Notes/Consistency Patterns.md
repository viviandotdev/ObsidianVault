---
created: 2023-10-15 10:55
modified: Sunday 15th October 2023 13:31:17
alias:
Category: system-design
Status: hold
tags: "[[system-design]]"
---
up::  [[system-design]]

## Consistency Patterns

**Consistency:**
	Discuss the appropriate consistency model for your distributed system.
		**Strong consistency**: Strong consistency ensures that all read and write operations reflect the most recent write.
			**Linearizability** is like having a guarantee that every operation (like money transfers) in the app feels as if it happens instantly at some specific moment between starting and finishing. It ensures you always see a consistent view of your data, as if every action occurred instantly and in a specific order.
		**Eventual consistency**:
			**Gossip Protocols:** Nodes periodically exchange state information with a few other nodes in the system. Over time, all nodes converge to a consistent view of the cluster, ensuring eventual consistency.
	**Quorum-Based Consistency:** Requiring a certain number of nodes to agree on a read or write before it is considered successful.
		It balances the trade-off between consistency, availability, and partition tolerance, making it a practical choice for many distributed applications where immediate and absolute consistency is not strictly required but a strong level of consistency is necessary for the system to function correctly.
	**Versioning**: Assign versions to data items, allowing clients to reconcile conflicting updates based on version numbers. Helps ensure outdated data does not overwrite more recent updates.



[Consistency Patterns. Consistency patterns are approaches or… | by Aayush Agarwal | Medium](https://medium.com/@crazy_nuclei/consistency-patterns-e5e720476d57)
https://medium.com/@crazy_nuclei/consistency-patterns-e5e720476d57

[Idea of Consistency patterns in System Design](https://iq.opengenus.org/consistency-patterns-in-system-design/)

[Consistency Patterns - System Design](https://systemdesign.one/consistency-patterns/)


[System Design Interview Concepts – Eventual Consistency](https://www.acodersjourney.com/eventual-consistency/)

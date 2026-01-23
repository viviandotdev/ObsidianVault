---
created: 2023-10-15 13:18
modified: 2025-06-22T19:18:52-04:00
---
type:: #note/concept 
tags:: [[system-design]]

What are system design patterns that improve **availability** and **fault tolerance**?
**Availability** =  System up time the percentage time the system has been working and available.

**Redundancy**: Eliminate single points of failure
	- Regions
	- Availability Zones
	- High availability pair
	- Data Replication
		- [[Master Slave Replication]]
**Switch from one server to another without losing data**
	- DNS
	- Load Balancing
	- Reverse Proxy
	- API Gateway
	- Peer Discovery
	- Service Discovery
**Protect System from Atypical client behavior**
	- Rate limiting
	- Cell-based architecture
	- Shuffle Sharding
**Protect System from Failures and Bad Performance when Certain Parts Fail**
	- Time outs
	- Circuit Breaker
	- Retires
**Failure Detection**
	- Monitoring
**Data Backup and Recovery**: Regular backup data have a robust recovery mechanism in place to minimize data loss in case of failures.

[Architecting for Reliability Part 2 — Resiliency and Availability Design Patterns for the Cloud | by Sathiya Shunmugasundaram | becloudy | Medium](https://medium.com/becloudy/architecting-for-reliability-part-2-resiliency-and-availability-design-patterns-for-the-cloud-cf7aaaed0df2)

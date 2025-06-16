---
created: 2023-10-15 13:09
modified: Sunday 15th October 2023 13:30:32

Status: idea
Category: system-design
tags: "[[system-design]]"
---
up::  [[system-design]]


## Design Patterns that Improve Scalability

### Scalability Patterns

**Scalability:**
	How will you handle anticipated growth rate in terms of users, data volume and transactions?
	How does your system ensure rapid response times for users?
		**Horizontal vs vertical scaling**
		**Load balancing**: As users grow, it prevents a single server from becoming overwhelmed, ensuring even distribution of requests
		**Database sharding**: Partition database to smaller shards distributed across multiple servers. Allows horizontal scaling as the dataset crows.
		**Caching**: Reduces the need to fetch data from slower data source, improving response time.
		**Microservices and serverless**- cold starts
		**Replication**:Creating copies of data and distributing them amount different data centers. Increase read scalability because multiple servers can handle read requests
		**[[MapReduce]]** -  targets batch jobs where disk I/O is the major bottleneck. It use a distributed file system so that disk I/O can be done in parallel.

[Scalability Patterns and Anti-Patterns for Technical Design](https://www.linkedin.com/advice/0/what-some-common-scalability-patterns-anti-patterns)
[8 Commonly Used Scalable System Design Patterns - High Scalability -](http://highscalability.com/blog/2010/12/1/8-commonly-used-scalable-system-design-patterns.html)![[Screenshot 2023-10-15 at 2.51.19 PM.png]]

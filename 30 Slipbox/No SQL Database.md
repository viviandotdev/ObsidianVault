---
created: 2023-07-16 15:26
modified: Sunday 16th July 2023 15:26:13
alias:
---
up::
tags:: [[system-design]]
related: [[SQL Database]]

## No SQL Database

**Examples:** Cassandra: column, MongoDB: document based
Preferred for application dealing with large amounts of unstructured or rapidly changing data, like user generated social media posts, text documents

**Advantages**:
1. flexibility, data is more free form
2. scalability, can be scaled horizontally to increase performance

**Disadvantages**:
Don’t support ACID transactions across multiple documents

**Scaling:**
Designed for scale out horizontal scaling: handles increased traffic by distributing workload across multiple servers

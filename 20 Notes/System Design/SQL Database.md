---
created: 2023-07-16 15:26
modified: 2025-06-15T18:58:58-04:00

---
tags:: [[system-design]]
related: [[No SQL Database]]

**Examples:** SQL, PostgresSQL
**Data Model:**
	Relational data model, data in stored in tables which relationships between tables defined using keys

**Use Case:**
	Handling large amounts of structured data such as customer data such as names, addresses, phone numbers and email addresses, each customer data would be represented as a row in a table

**Benefits:**
	Supports multiple record ACID transactions ACID (Atomicity, Consistency, Isolation, Durability)

**Disadvantages:**
1. Less flexible, because the structure of the data is more rigid.
2. More difficult to scale out because they are optimized for complex querying and relational operations which often involve joins that require the data to be located on a single. database instance. Distributing this data across multiple node can make these queries much more complex and slower to execute.

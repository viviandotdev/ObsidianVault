---
created: <% tp.file.creation_date() %>
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
alias:
---
up::
tags:: #system-design
related:[[Load Balancer]]

## Database Sharding

What is database sharding?
Spliting a single dataset into partitions of shards. This allows larger datasets to be split into smaller chunks to be storead across multiple data-nodes

Database sharding is a form of horizontal scaling, rather than making the database bigger when we need more storage we can split the data into multiple chunks and store it across multiple database instances.

**Advantages of Sharding**
- Increase read/write throughout
  - By distributing the dataset across multiple shards, both read and write operation capacity is increased.
- High Availability of the system
  - By creating additional copies of the databse, read performance can be increased using [[Load Balancer]]s.

**Disadvantages of Sharding**
- Increased infrastructure costs.
  - By nature sharding will require more machines where each additional database / shard means mosts costs
- Increased complexity
  - With every sharded database, on top of managing the shards themselves, there are additional service nodes to maintain.

### Links to this page
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```

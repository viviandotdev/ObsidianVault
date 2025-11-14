---
created: 2023-12-13 06:57
modified: 2025-06-15T13:21:18-04:00

---
up:: [[01 System Design Problems]]
tags:: [[system-design]]

What is UUID Generator?
Generates unique Ids,

• IDs must be unique.
• IDs are numerical values only.
• IDs fit into 64-bit.
• IDs are ordered by date.
• Ability to generate over 10,000 unique IDs per second.

### Multi Master Replication
Auto-increment feature in databases

However instead of incrementing by 1 we can increment by k where k is the number of database in the system.
**Pros**
Easy to implement
**Cons**
It does not scale well when a server is added or removed.
### UUID
UUID is a randomly generated 128 bit number. The UUID algorithm has a very low probability of getting collisions.
**Pros**
Easy to implement
Scales well when web servers need to be added or removed because each server is independently responsible for generating the ids they use
**Cons**
IDs don't increase with time
128 bits is very long
### Ticket Server
Use a centralized auto_increment feature on a single data base server
**Pros**
Easy to implement
**Cons**
Single point of failure, if the ticket server goes down all the servers that use it to generate id's will have issues.

### Twitter Snowflake
Instead of generating IDs we can divide the ID into different sections
- **Timestamp**- 41 bits, the timestamps grow with time making the IDs sortable by time. The timestamp represents the number of milliseconds since a custom epoch
- **Datacenter ID**-  chosen at the start up time of the machine.
	- Node ID remains constant for the specific node or worker throughout its lifetime in the distributed system. The combination of Timestamp, Node ID, and Sequence Number allows for the generation of unique Snowflake IDs in a distributed and scalable manner.
- **Sequence number**- this sequences id's that are generated within 1 millisecond from each other on the same server.
	- In case multiple IDs are generated at the same timestamp by the same node, a sequence number is used to ensure uniqueness within that timestamp/node combination.

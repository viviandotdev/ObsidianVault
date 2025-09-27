---
created: 2023-09-01 14:53
modified: 2025-06-15T18:27:13-04:00

---
tags:: [[system-design]]
### Functional Requirements

- `generateId()` return a 64 bit unit ID
- IDs must be unique and sortable by time
### Multi-master replication
auto_increment ID. However, in a distributed system with many databases we cannot just increment the ID by one there will be duplicate IDs instead we can increment by k where k is the number of database servers in use. Therefore, the IDs from each database will not overlap.
**Pros**
- Simple
**Drawbacks**
• Hard to scale with multiple data centers
• IDs do not go up with time across multiple servers.
• **It does not scale well when a server is added or removed.**
![[Screenshot 2023-09-01 at 2.59.08 PM.png]]

### UUID
In this design, each web server contains an ID generator, and a web server is responsible for generating IDs independently.
Pros:
• Generating UUID is simple. No coordination between servers is needed so there will not be any synchronization issues.
• The system is easy to scale because each web server is responsible for generating IDs they consume. ID generator can easily scale with web servers.
Cons:
• IDs are 128 bits long, but our requirement is 64 bits.
- IDs do not go up with time.
• IDs could be non-numeric.


## Ticket
![[Screenshot 2023-09-01 at 3.00.49 PM.png]]
The idea is to use a centralized auto_increment feature in a single database server (Ticket Server).
Pros:
• Numeric IDs.
• It is easy to implement, and it works for small to medium-scale applications.
Cons:
• Single point of failure. Single ticket server means if the ticket server goes down, all systems that depend on it will face issues. To avoid a single point of failure, we can set up multiple ticket servers. However, this will introduce new challenges such as data synchronization.

### Twitter Snowflake
Instead of generating an ID directly, we divide an ID into different sections
![[Screenshot 2023-09-01 at 3.02.45 PM.png]]
Datacenter IDs and machine IDs are chosen at the startup time, generally fixed once the system is up running.

Timestamp: As timestamps grow with time, IDs are sortable by time.

Sequence number: This field is 0 unless more than one ID is **generated in a millisecond** on the same server.

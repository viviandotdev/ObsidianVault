---
created: 2024-02-29 16:26
modified: 2025-06-15T13:20:32-04:00
alias: 
---
tags:: [[system-design]]
links::
## Design a Chat System
- finish the API list
- show the path for the direct and then the group message flow visually
-
**Functional Requirements**
1. Users can send and receive chat messages from other clients in real time
2. Users can send the status of message of status, delivered or read
3. Users receive notifications
4. Users can chat one on one with another user
5. Users can create and chat in group chats.

**Non-functional requirements**
- Scalable
- Available
- Fault Tolerant

#### Database Schema (NoSQL vs SQL)
Two types of data
**Generic data-** SQL Database
	- user profile
	- settings
	- friends lists
**Chat History data**- No SQL Database
	- About 1 to 1 read to write ratio.
	- A lot of data
	- Recent chats are accessed frequently
	- A key value store is a good way to store this data

| Message      |           |
| ------------ | --------- |
| messag_id    | bigint    |
| message_from | bigint    |
| message_to   | bigint    |
| content      | text      |
| created_at   | timestamp |

| group message |                         |
| ------------- | ----------------------- |
| channel_id    | channel_id              |
| message_id    | message_id              |
| user_id       | bigint (fk)             |
| content       | text                    |
| created_at    | timestamp               |
| id (pk)       | channel_id + message_id |
#### Communication
- **Web Socket**- Stateful **bidirectional communication channel that stays open, allowing real-time data exchange without continuous requests**. The connection is established with an initial HTTP handshake, the connection will persist until explicitly closed
	- List having a direct phone line open when a friend. You can talk back and forth without asking for anything new.
	![[2024-03-13.excalidraw|400]]
	![[websocket-chat-system|500]]
- **HTTP Polling**- Stateless Protocol that follows a request response model, the client sends a request to the server and the server responds each new request establishes a new connection but the connections are short. **The client repeatedly asks the server if there are any updates available.**
	- High overhead, there will be a lot of requests with empty responses.
#### System Components
- Chat Service
	- stores and relay the message to queue
	- What are web sockets
- Cassandra, database
	- Generic data, user profile, settings
- S3 (Key Value Store)
	- Chat message history
- Message sync Queue
	- a inbox for a user
- Zookeeper (service discovery)
	- Finds the best chat server for the user that logs on based on location, server capacity and other.
	- Then the user connects to that server through web sockets.

#### High Level Design
![[chat-system-high-level-design|500]]

#### One To One Message Flow
1. Bob sends a message to Alice
2. Bob sends a chat message to Chat server 1
3. **Chat server** 1 sends the message to a **message sync queue**
4. The message is stored in a **key value store** (S3)
5. If User B is online the message is forwarded to Chat server 2 where user B is connected
6. If a push notification is sent from push notification servers
7. Chat server 2 forwards the message to User B. There is a persistent **Web Socket** connection between User B and Chat server 2.
![[2024-03-13_0.excalidraw|400]]
#### Group Chat Message Flow
1. User A sends a message to a group chat.
2. User A senses message to chat server 1
3. The Chat server 1 sends the message to the message sync queue for all users in the group.

**Benefits**
- Simplifies message sync flow, the message just needs to check it’s inbox to sync up the group messages
- When the group number is small it is not too expensive to store a copy
![[2024-03-13_1.excalidraw|400]]

#### Summary
**Scalable**- Shard and replicate the key value store
	Load balancer -  create multiple instances of each service and then place a load balancer in front to distribute the requests among the service evenly.
**Availability**-  Master slave replication
	[[Master Slave Replication]]
**Latency**- We can add a cache on the client side to store frequently accessed messages. (Such as the chats users open often)

### Resources

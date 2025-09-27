---
created: 2023-08-10 17:23
modified: Thursday 10th August 2023 17:23:34

---
up::  [[system-design]]
tags:: [[system-design]]
sources::
**Benefits of message queue**
	**Decoupled**- The sender and receiver of message operate independently. This flexibility haves it easier to scale individual components and add new ones without. affecting the overall system.
	**Increased Availability**: If a system fails the other parts can continue to interact with the queue
	**Increased Scalability**: Producers and Consumers can be scaled independently.
	**Performance:** Allows asynchronous communication, the consumers and producers don't need to wait for each other.
**Functional Requirements**
 - Producers send messages to a queue
 - Consumers consume messages from a message queue
 - Consume message in the order they are added to the queue
**Non-Functional Requirements**
- Scalable - Distributed should be able to handle sudden surges in message volume
- Low latency- fast response times to requests


**Message Models: What is point to point and pub/sub messaging?**
	1. Point to Point a message is processed only once by one consumer. There can be multiple consumers waiting to consume messages but each message can be only consumed by a single consumer.
		![[2023-08-25.excalidraw]]
	2. Pub/Sub a message can be processed by multiple consumers that have subscribed to the topic. Same message can be processed by multiple consumers. Consumers subscribe to a topic and a message sent to that topic will be received by all consumers subscribed to that topic.
		![[2023-08-25_0.excalidraw]]
### System Components
1. **Producer**- generates the message containing data.
2. **Consumer**
	Within a consumer group, each consumer pulls from a different partition.
4. **Topic**: Topics are categories used to organize messages. Each topic is unique name and consumers subscribe to a topic.
5. **Partition**: If the data volume of a topic os too large for a single. server we can divide a topic into partitions
6. **Offset**
	Keeps the **order of messages** inside the partition. The position of message in the partition is the off set. This offset is important because if a consumer fails, the next consumer will be able to pick up exactly where the failed consumer left off by reading this offset.
7. **Consumer Group** is a set of consumers working together to consumer messages from topics. Each consumer group can subscribe to multiple topics.
8. **Broker**
	A broker is a Kafka server, it is a single machine. When the queue size limit is exceeded, we can add additional brokers. Machines have a max storage limit, therefore if we want our system to be scalable we need the ability to add additional brokers. Brokers are servers that hold partitions.
8. **Cluster**
	A cluster is a group of brokers. Each brokers stores replicas of topics. Therefore, if a leader topic is down a replica can take over. This process is coordinated by the zookeeper.
9. **Dead letter queue**
	When a message is buggy and fails all the set retries. The consumer will send it to the dead letter queue and move on to the next message. A separate process will deal with the messaging in the dead letter queue

 **System Architecture **
	![[2023-08-23.excalidraw]]
**Data Storage**
- Read and write heavy
- No update and delete operations
- Sequential read and write access
Database is a common option
- Relational: Create a topic table and write messages to the table as rows
- NoSQL: Create a collection as a topic and write messages as documents.
They are not ideal because it is hard to design a database that supports heavy read and writes
Write ahead log (WAL)
WAL - simple plain file where new entries are added to an append only log. We can persist message as WAL long files on disk. WAL have purely sequential read and write access pattern.

### Message Schema
**key**: used to determine the partition of the message. The partition is chosen by hash(key) % numPartition
**value**: the payload of the message
**topic**:  the name of the topic the message belongs to.
**partition**: the id of the partition the message belongs
**offset**: the position of the message in the partition
**timestamp**: the timestamp of when the message is stored
**size**: size of this message
![[Screenshot 2024-02-28 at 11.39.53 AM.png|200]]
```d
Table message {
	key integer
	value json
	topic string
	partition long
	offset long
	timestamp datetime
}

```

**Push Model**
In a push model the producers control the consumptions rate, the brokers push data to consumers
**Advantages:**
	Low latency- the broker push messages to the consumer immediately upon receiving them
**Disadvantages**
	The rate of consumption falls below the rate of production, consumers could be overwhelmed. The producer will try to push more than the consumer can handle.
	 Difficult to deal with consumers with different processing power because the broker control the rate which data is transferred.

**Pull Model**
Consumers pull data from the brokers therefore they control the consumption rate.
**Advantages**
The Consumers control the consumption rate.
If the rate of consumption fall below the rate of production we can simply scale out the consumers. The consumers can choose how much they can handle and if they production rate is too much can scale out
This model is good for **batch processing**. In the push model the broker has no idea if the consumer will be able to process the message immediately. If the broker sends messages but the consumer is backed up the new message will stay in a temporary storage buffer. When the consumer is ready it will pull all the available message after the consumer's current position in the log.
**Disadvantages**:
When there is not message in the broker the consumer may still pull data wasting resources.
**Based on the tradeoffs most. message queues choose the pull model**

### Configuration Service
9. **Zookeeper**:
	Configuration service that knows about the consumers and brokers and coordinates them. All the services are registered in zookeeper and sends heart beats to zookeeper to indicate that it is alive. If a consumer stops sending heart beats, then the zookeeper will know that the service has died. Then zookeeper will be able to choose a consumer from the same consumer group to pick up processing from where the failed consumer left off



### Resources
[16. System Design - Distributed Messaging Queue | Design Messaging Queue like Kafka, RabbitMQ - YouTube](https://www.youtube.com/watch?v=oVZtzZVe9Dg)

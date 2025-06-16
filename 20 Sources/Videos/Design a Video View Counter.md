---
created: 2023-07-16 13:26
modified: 2025-06-16T07:15:18-04:00

---
tags:: [[system-design]]
type:: #source/video
source: [System Design Interview – Step By Step Guide - YouTube](https://www.youtube.com/watch?v=bUHFg8CZFws)

# Design a Video View Counter

### Table of Contents
- [[#Requirements Classification|Requirements Classification]]
	Functional Requirements
	Non-Functional Requirements
- [[#Draw out the high level architecture|Draw out the high level architecture]]
- [[#Database (Apache Cassandra, Apache HBases)|Database (Apache Cassandra, Apache HBases)]]
	- what we store
		- raw vs aggregate
	- where we store
		- SQL vs NoSQL
- [[#Database (Apache Cassandra, Apache HBases)|Data Processing Service (Apache Spark, Apache Flink)]]
	- data aggregation
		aggregator
		in memory store
		state store
	- how to not lose data during processing, **consistency and fault toleran**t
		- checkpoint, and pulling data
	- how to achieve **high throughput**?
		- partitioning
		- partition consumer
		- dead letter queue
		- embede database
- [[#Data ingestion path|Data ingestion path]]
	- APi gateway
		- partitioner service client
		- batching / buffering
		- timeouts
		- retries
		- circuit breaker
	- load balancer
		- algorithms
		- DNS
		- how to load balancers help achieve high availability?
	- partitioner service
		- partition strategies
			- hash based
			- how to handle hot partitions
		- service discovery
		- message format
- [[#How to identify bottle necks|Bottlenecks]]
	- how to identify bottlenecks?
		- performance testing
		- health monitoring
- [[#How to make sure the system produces accurate results?]]
		lambda architecture
		stream and batch processing
- [[#Architecture Summary]]


### Requirements Classification
What we may want to ask the interviewer about?

| User                            | Scale                                          | Performance                                    | Cost                                                |
| ------------------------------- | ---------------------------------------------- | ---------------------------------------------- | --------------------------------------------------- |
| who will be using this service? | how many read and write queries per second?    | what is expected write to read delay?          | Should the design minimize the cost of development? |
| how will they use this service  | can there be spikes in traffic?                | what is expected p99 latency for read queries? | should the design minimize the cost of maintenance  |
|                                 | how many video views are processed per second? |                                                |                                                     |

**Clarifying Questions:**
1. what is p99 latency (amount of time it takes for data to travel from source to destination) ? The P99 latency is the 99th latency percentile, **This means that 99% of requests will be faster than the given latency numbe**r. It helps identify outliers or situations where the system's performance degrades significantly for a small fraction of requests.

### Define the function requirements API

- API requirements for what we want the system to do
- What data does the user need to request?

**The system has to count video view events**
countViewEvent(videoId)
countEvent(videoId, eventType) where eventType can be “view”, “like”, “share”
processEvent(videoId, eventType, function) where function can be “count”, “sum”, “average”
processEvents(listOfEvents)

The system has to return video views count for a time period
getViewCount(videoId, startTime, endTime)
getCount(videoId, eventType, startTime, endTime)
getStats(videoId, eventType, function, startTime, endTime)

### Define non-functional requirements API

**Scalability**: how well the system performs to a large number of users and requests
**Consistency**: all nodes in a distributed system observe the same data at the same time.
**Availability**: every request receives a response without any errors, even in the presence of failures.
**Partition** **tolerance**: The system continues to operate and make progress despite network failures. no single point of failure

### Draw out the high level architecture
![[Screenshot_2023-06-21_at_2.58.54_PM.png]]
### Database (Apache Cassandra, Apache HBases)

Raw Events: (Apache Hadoop, AWS Redshift)
AWS S3: (Rolled up and archived data)
Cache: Redis,

### What we Store
| Raw Data                                 | Aggregate Data                                 |
| ---------------------------------------- | ---------------------------------------------- |
| individual events (every click)          | clicks per minute                              |
| fast writes                              | fast reads                                     |
| can slice and dice data however we need  | date is ready for decision making              |
| we can recalculate the numbers if needed | can query only the way the data was aggregated |
| slow reads                               | requires data aggregation pipeline             |
| costly for a large scale (many events)   | hard or even impossible to fix errors          |

### Where we store: List of non-functional requirements

- How to scale writes and reads?
    **[[Database Sharding]]:** Splitting the data into smaller chunks and storing this across several database servers. Sharding helps scales writes in the database system by **distributing** the read and write **loads** across multiple shards.
- How to make both reads and writes fast?
    **[[Database Sharding]]** increases database read and write throughput (read and write operations per second)
- How not to lose data in case of hardware faults and network partitions? (Replication)
    Replication, create multiple copies of your database, read operations can be. directed to the replica servers, to help offload the read load on the primary server improving read performance.
    Place the data in two different data centers
- how to achieve strong consistency? what are the tradeoff?
    **Quorum reads and write** help achieve strong consistency. This technique uses a quorum which represents the minimum number of nodes required to reach consensus of a successful operation.
    - Quorum reads:
        the system reads data from a subset of replicas/nodes and considers the read successful which a certain amount of nodes respond with the some data. **This ensures strong consistency because the read operation will always return the the latest committed data that has. been replicated to a majority of replicas.** However the tradeoff is that they can be slower than eventual consistency approaches because a consensus must be reached. among a subset of replicas before a result is returned.
    - Quorum writes:
        quorum writes ensures durability and availability, by requiring a write to be acknowledged by a quorum of replicas, the system guarantees that the data will be reliably stored and available for subsequent reads, even if some replicas are temporarily unavailable or fail.

How to recover data is case of an outage?
How to ensure data security
How to make it extensible for data model changes in the future?
Where to run (cloud vs on premise data centers)?

### Where we store: How SQL database handle these requirements
![[sql-database.excalidraw]]
### **Where to store: About NoSql: Cassandra**

Group Protocol: Instead of using a **configurations service that knows that status and availability** of each database and a proxy to route requests,  in a NoSQL databases each database knows about each other and route the requests to the correct database

1. Processing service makes request to coordinator node %
2. Coordinator node decides which nodes stores the data for the requested video, we can use **consisting hashing** algorithm to chose the node or nodes
3. Quorom reads and Writes
![[Screenshot_2023-06-21_at_4.31.54_PM.png|800]]
- How we Store
    ![[Screenshot_2023-06-22_at_6.40.36_AM.png]]

- what is the difference between[[ No SQL Database]] and [[SQL Database]]

### Data Processing Service (Apache Spark, Apache Flink)

### Summary
- how to scale?
    **pre-aggregating data** in the processing service allows to scale of system better because it reduces database load and increase performance optimization.
- how to achieve high throughput? (number of operations per second)?
    partitioning the input data, therefore each partition can be processed in parallel, increasing performance
- how to not lose data when processing node crashes?
    using checkpoints, processing nodes will pull input data sequentially from a temp storage, after a certain interval a checkpoint is created and the intermediary data will put in persistent storage. Therefore if the processing node fails we can reprocess that data from the checkpoint instead of starting over and reprocessing the entire data set

### Data aggregation
why is **pre-aggregating** data in the processing service better for large **scale** systems?
![[Screenshot_2023-06-23_at_6.36.35_AM.png]]
1. Performance optimization- calculating and storing aggregated in advance is better because it reduces computational overhead, during query execution, this leads to faster response times.
2. Reduced database load- offload some processing workload from the database
3. Decoupling from data-source:  allows you to aggregate data from multiple sources regardless of the underlying data structure or format, this means we can design a processing service that efficiently handle data from various sources

### **Push vs Pull**
![[Screenshot_2023-06-23_at_6.37.31_AM.png]]
what is the advantages of pulling the data from a temp storage?
- if the processing service crashes the events are still in the temp storage therefore we can re process them, however without a temp storage if a process service crashes all the data that was being processed if deleted

### **[[Checkpointing]]**
![[Screenshot_2023-06-23_at_6.37.47_AM.png]]
- As events arrive we store in the temp storage and the processing service will pull these events from the storage sequentially.
- checkpointing is a technique used to periodically save intermediate results of the data aggregation process. checkpoints are created at predefined intervals.  After a predefined number of events are processed and successfully stored in the database we will create checkpoint to write the intermediate data to some persistent storage.

How do checkpoints ensure **consistency?**
- By periodically saving intermediate results, all data is not lost when the processing service. crashes. Helps prevent data inconsistencies than can results from processing failures.

How do checkpoints ensure **fault tolerance?**
- if failure occurs during aggregation process we can recover from the last saved checkpoint, avoids processing entire dataset from the beginning saving time and computational resources.

### **Partitioning (Multi threaded. data aggregation)**
![[Screenshot_2023-06-23_at_6.38.34_AM.png]]

- Partition input data into smaller subsets. Once the data is partitioned each partition can be processed in **parallel.**
    - Multiple threads can be created to process each of the partitions concurrently

### Partitioning Service
![[Screenshot_2023-06-23_at_7.28.05_AM.png]]
- **Partition consumer:**
    1. establishes TCP connection with the partition to pull data from.
    2. Consumer reads the events and deserializes.
    3. Usually this is a **single threaded component**, reads events from the partition sequentially one by one. However we can implement a **multi-threaded** consumer that reads multiple events from the partition in parallel, however this makes it **difficult to preserve the order of the events.**
1. Deduplication cache: store the unique event identifiers, let’s say for the last 10 minutes, if multiple identical messages arrive within 10 minute interval only one of them will be processed.
3. Aggregator: After the partition consumer reads, deserialize and deduplicates the events the events goes into the aggregator for in-memory counting, Combines the individual events into an aggregated form using an in-memory store such as a hash table.
4. **State Store:** Events stored **in-memory will be lost when the machine fails**. The solution to this is **checkpointing**: is a technique used to periodically store the entire in-memory data data to persistent storage.
5. Internal Queue: Temporary storage for incoming data that needs to be written to the database.
    1. **Asynchronous Processing**: With an internal queue, the producer and consumer components operate independently. The **producer can enqueue tasks or data without waiting for their immediate processing**, allowing it to continue with its own operations. The c**onsumer component can then process the tasks at its own pace,** optimizing resource utilization and potentially improving overall system throughput.Order preservation
    2. Order Preservation: An internal queue can help preserve the order by processing tasks in the same order they were enqueued.
    3. Fault Tolerance and Resilience: If a processing component fails or experiences issues, the tasks or data in the queue remain intact. This allows for graceful recovery or the ability to switch to alternate processing components without losing any work.
6. Database Writer: Can also be either a single or multi threaded component, each thread takes a message from the internal queue and stores the pre-aggregated views count in the data base.
    Single threaded makes checkpointing easier, multi threaded increase throughput (operations per second)
6. Dead letter queue: Store messages that could not be routed to the correct destination, if a database becomes slow for we cannot reach the database due to network issues. messages are pushed to this dead-letter queue and a separate process is used to read messages from this queue and send them to the database. (AWS SQS or Rabbit MQ)
7. Embedded Database (RocksDB): Attributes such as channel name, video title does not come in the processing service with every video view event. The video view event will. only have a video identifier and a time. stamp, We can store the extra attributes in a embedded database in the same machine as the processing service. This eliminates the need from multiple remote calls
### Data ingestion path
![[Screenshot_2023-06-23_at_7.32.32_AM.png]]

API Gateway: When a user opens a video a request goes through the API Gateway which is the entry to various backend services, the video view counter system is one of those backend services. It receives incoming data from clients or other systems via API calls. It performs initial authentication, authorization, and request validation.

Partitioner Service Client

Load Balancer: **Evenly distributes events across partitioner service machines.** The load balancer receives the data from the API Gateway and distributes it across multiple instances of the partitioner service. The load balancer ensures that the incoming data is evenly distributed to maintain a balanced workload across the partitioner service instances.

Partitioner Service: he partitioner service is responsible for analyzing the incoming data and determining the appropriate partition(s) to handle it. A partition represents a logical subset or shard of the data. The partitioner service uses various techniques (such as hashing, key-based routing, or predefined rules) to assign the incoming data to the relevant partitions.

**Partitions Service Client**
Blocking Systems (Synchronous): When a request a is made a **thread** is dedicated to handling the request, therefore if the request takes too long to complete the thread stays occupied and prevents it from being used for other tasks. Request arrival and processing are not decoupled. (Used in situations were it is acceptable to wait for a task’s completion such as I/O operations)

Non-Blocking Systems (Asynchronous): Messages can be **queued** up and processed concurrently without blocking the execution flow. The queue is a buffer that holds requests until they can be processed. This decouples the request arrival from request processing, allowing a more efficient use of system resources. (Better for scalability, responsiveness)

Technology (Neety)
Buffering and Batching:
1. Request batching: combining multiple individual request into a single batch for processing. (Reduces the overhead of individual request handling)
2. Request buffering: Temporarily storing incoming requests to a queue before processing. Decouples the arrival of requests and processing allow for the more efficient use of system resources.

Timeouts
Connection timeout: how long the client is willing to wait for a connection to be established,
Response timeout: after the connection is established how long is the client willing to wait for a response before it considers the request as failed.

Retries
When a request fails the system will handle these failures by retrying again. A common retry strategy is exponential back off and jitter which increases the time between each retry exponentially. Jitter is a randomization applied to the relay between retry times to prevent synchronization between retries across systems

Circuit breaker:
Prevents clients from continuously executing requests to a service that is likely to fail. When the circuit breaker determines the service is in a problematic state it opens the circuit and blocks or redirects subsequent requests to the service. Helps avoid wasting resources and improves overall system responsiveness.
(Examples) website says to try again later when try to many times a make a failed request
Drawbacks: Testing how the system response to various failure scenarios can be more complex

### [[Load Balancer]] (NetScaler, NGINX, AWS ELB)

Hardware: network devices, powerful machines, can handle high throughput. These machines are designed to distribute incoming traffic across multiple servers
Software: More flexible than hardware, because it can be deployed on hardware, virtual machines for cloud instances making them adaptable to multiple environments.

**Algorithms**

1. Round Robin: Requests are distributed in a cyclic order, ensuring each server receives an equal share of the traffic.
2. Least Connections: Incoming requests are sent to the server with the fewest active connections to evenly distribute the workload.
3. Least Response Time: Requests are directed to the server with the lowest average response time or latency to minimize overall response times.
4. Hash-based Algorithms: Requests are routed to specific servers based on a hashed attribute (e.g., client IP address), ensuring consistent handling for requests with the same attribute.

How the partitioner client know about load balancer: (DNS)
DNS: Internet phone books, maps domain name to IP address.
How does the load balancer know about partition service matches: (DNS)
load balancer need to register the services they are sending traffic to
How do load balancer guarantee high availability?

Load balancers perform **health checks** on the servers that are balancing, this helps. When a server fails a health check, the load balancer will temporality stop directing traffic to that server and direct traffic to a secondary server until the primary server becomes available again.
High availability: primary and secondary
Load balancers will monitor primary (different data centers)
The primary-secondary setup is a common approach to achieve high availability. In this configuration, if the primary system experiences a failure or becomes unreachable, the secondary system can seamlessly take over its responsibilities. This ensures continuity of service and minimizes downtime.

### **Partitioner service (Apache Kafka, AWS Kinesis)**

Partition strategy to define which partition gets what events
Hash-Based Partitioning: Events are assigned to partitions based on a hash function applied to a key or attribute.
How would a system handle hot partitions for time series data?
**Hot partition**s, a popular video, one partition gets a lot traffic for a certain amount of time.
Time Range Queries: Time-based partitioning enables efficient querying of data within specific time ranges. Instead of scanning the entire dataset, you can target specific partitions based on the time range of interest (i.e every minute change partitions). This approach significantly reduces the amount of data that needs to be processed, improving query performance.

In the minute time frame a single partition will have high traffic but over time data is spread out
Split the hot partition ins to 2:
**Service discovery: Mechanism used in distributed systems to locate and communicate with services and resources.**
Server side discovery: In server-side discovery, the service registry or discovery mechanism is managed by a separate component or infrastructure, often referred to as the service registry or service discovery server.

Server-Side Discovery Pros: Clients receive service instance recommendations from the registry, simplifying client code. The service registry can also perform additional functions like health checks and service monitoring.
Server-Side Discovery Cons: The service registry becomes a potential single point of failure or bottleneck. Clients may have limited control over load balancing and service selection, as it is determined by the registry’s policies. Clients need to make additional network requests to the registry, which may introduce latency.

Client side discovery: In client-side discovery, the responsibility of service discovery lies with the client. Clients are aware of a service registry or a centralized service discovery mechanism

Clients have more control over load balancing, failover, and service selection. Clients can implement custom algorithms or policies based on their specific requirements. It allows for more flexible and dynamic client behavior.

Clients need to be aware of the service registry and handle the discovery process, which adds complexity to the client code. Clients may also need to implement additional logic for service selection, load balancing, and fault tolerance.

Zookeeper: distributed coordination service that can be used for service discovery

Service Discovery: Clients interested in accessing a particular service query ZooKeeper for the available instances by inspecting the relevant path or directory in the Znode tree. ZooKeeper returns the list of registered service instances.

Netflix eureka:Eureka is **the Netflix Service Discovery Server and Client**. The server can be configured and deployed to be highly available, with each server replicating state about the registered services to the others.

**Replications**
when events are persisted in partition replication they need to be replicated
Single (SQL), multi leader and leader less replication (Cassandra)
Multi leader is for replication across several data centers
**Message format**
Texual (Json): human readable, be larger in size which can negatively impact network bandwidth and performance.
binary (thrift, protobufs) large scale, more compact fast to parse, field tags,
Use schemas, clients need to know schema to serialize the message, consumer uses the same schema to deserialze message

### Data Retrieval Path
![[Screenshot_2023-06-25_at_10.18.51_AM.png]]
Cold Storage:
Cold storage refers to long-term data storage that is accessed infrequently or rarely.

Hot Storage:
Hot storage refers to actively used and frequently accessed data storage.

Query results go in a cache, to increase performance

### How to identify bottle necks

Performance testing types

1. Load Testing: Load testing involves t**esting the system's performance under anticipated load conditions.** It helps determine the system's behavior when multiple users access it simultaneously or when the system experiences a high volume of transactions.
2. Stress Testing: Stress testing examines the system's behavior under **extreme conditions beyond its normal capacit**y. It involves pushing the system to its maximum limits by increasing the load or resources to observe how it performs and recovers from stress.
3. Spike Testing: Spike testing evaluates the system's ability to handle sudden and significant increases in load. It involves generating a **sudden surge in user traffic or transaction** volume to assess the system's response time and scalability.
4. Soak Testing: Soak testing, also known as endurance testing, checks the system's performance over an **extended period under a steady load.** It helps identify any memory leaks, resource utilization issues, or performance degradation that may occur with prolonged system usage.

Technology: ***Apache JMeter*** is a free and open-source system for performance testing. It enables you to simulate workloads and users of your web applications

How to monitor the health of a system?
We measure the Latency, Traffic, Errors and saturations, using monitoring such as AWS Cloudwatch

1. Latency: **Latency measures the time taken for a request or operation to complete.** It indicates the responsiveness of the system. Monitoring latency helps identify bottlenecks and ensures that the system is meeting performance expectations.
2. Traffic: Traffic monitoring **involves tracking the volume of incoming requests or data to the system.** It helps in understanding the system's load and capacity utilization. Monitoring traffic helps identify peak usage periods, plan for scalability, and detect unusual spikes or drops in traffic.
3. Errors: Monitoring **errors involves tracking the number and types of errors occurring within the system**. It helps identify issues, such as software bugs, configuration problems, or network issues. Monitoring errors allows for timely detection and resolution of problems to maintain system reliability and user satisfaction.
4. Saturation: Saturation monitoring measures the **utilization or capacity of system resources such as CPU, memory, disk, or network.** It helps identify resource bottlenecks and potential performance degradation. Monitoring saturation allows for proactive capacity planning and optimization to ensure efficient resource utilization.

### How to make sure the system produces accurate results?

	we need to accurately count ad views on videos to make sure we properly charge the ad owner and pay the video owner.
	We need an audit system to ensure the accuracy of our results.
	**Weak:** **Continuously run end to end tests**, When let's say once a minute we generate several video view events in the system, call query service and validate that returned value equals to the expected count.
	And it is **easy to implement and maintain such test.** But unfortunately, this test is not 100% reliable. What if our system loses events in some rare scenarios?

**Strong**: The key idea is to send events to a **batch system** and a **stream processing system** in parallel. And stitch together the results from both systems at query time.

store raw events  (stream processing) Apache Kafka

Stream processing deals with data that is continuously generated and processed in real-time or near-real-time.

count aggregated events (batch processing but it has much higher latency) (Apache Map Reduce)

**batch processing, where data is accumulated over a certain period or batch size before processing**

**MapReduce** is a [programming model](https://en.wikipedia.org/wiki/Programming_model) and an associated implementation for processing and generating [big data](https://en.wikipedia.org/wiki/Big_data) sets with a [parallel](https://en.wikipedia.org/wiki/Parallel_computing), [distributed](https://en.wikipedia.org/wiki/Distributed_computing) algorithm on a [cluster](https://en.wikipedia.org/wiki/Cluster_(computing)).[[1]](https://en.wikipedia.org/wiki/MapReduce#cite_note-1)[[2]](https://en.wikipedia.org/wiki/MapReduce#cite_note-2)[[3]](https://en.wikipedia.org/wiki/MapReduce#cite_note-GoogleMapReduce-3)

[[Lambda architecture]] is a data processing architecture that combines batch processing and real-time/streaming processing to provide a comprehensive and scalable solution for handling large volumes of data

### what if processing service cannot keep up with the speed of new message to arrive?
Use an method that combines batch and stream processing
- **Batch events and store them in AWS S3**.
- **Every time we persist a batch of events, we send a message to a message broker. For example SQS.**
- **Then we have a big cluster of machines, for example EC2, that retrieve messages from SQS, read a corresponding batch of events from S3 and process each event.**
- **This approach is a bit slower than stream processing, but faster than batch processing**
- More Info
    1. Batch Events and Storage: In this method, events are collected and stored in batches. This is a characteristic of **batch processing, where data is accumulated over a certain period or batch size before processing.** The events are stored in AWS S3, which serves as a durable and scalable storage solution.
    2. Message Broker: When a batch of events is persisted in S3, a message is sent to a message broker like Amazon Simple Queue Service (SQS). The message broker acts as a buffer and coordination mechanism between the data source and the processing cluster.
    3. Processing Cluster: The processing cluster consists of a big cluster of machines, such as Amazon EC2 instances, that retrieve messages from the message broker (SQS). Each machine in the cluster reads a corresponding batch of events from S3 and processes each event. This cluster-based processing can parallelize the workload and provide faster processing compared to traditional batch processing.

    While this approach does involve batching events and using a message broker for coordination, it does not handle the events in a strictly real-time or streaming fashion. Instead, it falls into a middle ground where events are processed in batches by the cluster of machines, offering faster processing compared to pure batch processing but not achieving the low-latency real-time processing of a dedicated stream processing system.

    By combining the benefits of batch processing (such as scalability, fault tolerance, and efficient resource utilization) with faster processing compared to pure batch processing, this approach strikes a balance between the two processing paradigms.

### Architecture Summary
![[Screenshot_2023-06-25_at_10.19.27_AM.png]]
### Outgoing  links
```dataview
LIST
FROM outgoing([[#]])
and -#map

SORT file.link asc
```
### Incoming to this page
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```

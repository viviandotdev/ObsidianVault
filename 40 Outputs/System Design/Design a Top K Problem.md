---
modified: 2025-03-30T11:45:04-04:00
---

up::  [[system-design]]
tags:: [[system-design]]
source::


# Top K Problem

### Top K Problem Types

Trends: topK searches
Popular products: topK products clicked
Volatile stocks: topK traded stocks
dDOs attack Prevention topK IP addresses that generates most number of requests

### **Functional Requirements**

Solution needs to calculate the top 100 lists for the last
1 minutes, 5 minutes, 15 minutes, 60 minutes

**Find the top K most viewed videos in a given time frame**

`TopK(vidId, start, end)`

### **Non Functional Requirements**

**Scalable**: The system is scalable and will work as the number of users grow
**Available**: The system is highly available, every request will receive a response.
**Fault Tolerant**: Networks are not reliable so the system should be able to handle network failures.
**Performance**: The system needs to be performant by making good use of its resource. Low latency
**Accurate**: The system should produce accurate values

### **Single Host Solution**

On a single host use a Hash Table Store the Frequency count of each video
Then using a heap algorithm sort get the topK elements in the hash in `O(log(k))` time

![[Screenshot_2023-06-29_at_10.08.17_AM.png|800]]
Why is this solution not scalable?

1. Events cannot be processed in parallel, this means the system will be slow and not performant

### **Multiple Hosts Solution**
![[Screenshot_2023-06-29_at_10.09.41_AM.png]]
Partition the data using **time range partitioning to** multiple hosts and use multiple hash tables to calculate the topK in each partition then combine the results

Pros:
More performant because requests can be processed in parallel

Cons:
In-Memory storage of the processing service will become very large

The storage host will store a list of the heavy hitters for every minute therefore info about other elements that do not make it to topK lists during the heap algorithm step will get lost.

What if we want to know that topK in an a hour? How can we build that from 60, one minute lists? This would not be accurate because a lot of data will be lost.

We would need the entire data set of the hour on that data to calculate the topK in longer time ranges.

Instead of storing values in a Hash table use

**Count-min sketch**

![[Screenshot_2023-06-29_at_10.11.12_AM 1.png]]
Instead use a fixed data structure such as a count-min sketch. Probabilistic data structure that is using sub linear memory.

**Imagine you have a large stream of items, and you want to keep track of how many times each item appears without storing the entire stream. The Count-Min Sketch solves this problem efficiently.**

Here’s how it works:

1. You start with an array of counters, initially set to zero. Let’s say this array has several rows and columns.
2. When an item from the stream arrives, the algorithm hashes the item to determine which counters to increment. Each row has its own hash function, and the hash values determine the columns to increment.
3. For each row, the corresponding counter in the selected column is incremented.
4. To estimate the frequency of an item, you apply the same hashing and look at the values in the corresponding counters. The minimum value among those counters gives you the estimated frequency.

The trick is that due to the probabilistic nature of the algorithm, there can be collisions, where different items get hashed to the same counter which leads to over counting.  **By incrementing multiple counters (rows)** (hash functions), the algorithm spreads out the collisions, reducing their impact on the estimation accuracy.

### High Level Architecture

API Gateway:
1. Single Entry point for all clients
2. Aggregates data. on the fly or via background processes
3. Serializes data into a binary format

Distributed Messaging System
1. Apache Kafka,
2.  Partitioning of messages

### Fast Path (Less precise)

![[Screenshot_2023-06-29_at_2.12.58_PM.png]]
**Fast processor:**
- API gateway aggregates the individual events by storing them a hash table when they're. Frequency counts. It sends this aggregated to a distributed messaging system.
- The fast processor pull data from the distributed messaging system and. Uses the count-min sketch and aggregates data for a short period of time
- Because memory in no longer problem we. Do not need to partition the data.
- Replication is nice to have but not needed
- Results are approximate

**Storage:**
- Flush the data to storage
- SQL, no SQL, builds the final count-min sketch and stores a list of top k elements for a period of time
- Data replication required

### Slow Path (More precise)
![[Screenshot_2023-06-29_at_2.15.13_PM.png]]
Produces more accurate results

**Data partitioner**
- Parses batches of events into individual events
- Hash partitioning, deals with hot partitions.

**Messaging System (Kafka)**
- Each partition will store a subset of the data

**Partition processor:**
- aggregates data in memory over the course of several minutes
- Single Data Processing path
- Tolerate approximate results-Fast path
- Accuracy is important and fast results - partition the data and aggregate in memory
- Time is not and issue, and we need accurate results on a large data set

**Map Reduce**
- Given large data set of millions of YouTube videos and their metadata information such as the likes and comments and would are asked to find which video has a certain number of likes.
- You would need to pass through the entire metadata information which is distributed across multiple machines and produce a output file.
- When you are given a large data set of files that are distributed across multiple machines and need to analyze all the times collectively, Map reduce is a good way to do that.
- For example in the TopK problem we use map reduce to get the frequency we take the input and split into in the form of key value pairs.
- The shuffle and sort phase we group the value of keys in the form of key value pairs.
- The reducer is applied to each of the groups, the reducer function combines the grouped key value pairs and combines them into a single output. Then the output of the reduce functions is combined to one output fine.
![[Screenshot_2023-06-29_at_2.16.47_PM.png]]
1. **The input to a MapReduce job is a set of files split into independent chunks which are processed by the map tasks in a parallel manner.**
2.  **First, the record reader parses the data into records and passes the data to the mapper, in the form of a key/value pair.**
3. **In the mapper, each key/value pair from the record reader is transformed into zero or more new key/value pairs, called the intermediate pairs.**
4. **In the next phase, the partitioner takes the intermediate key/value pairs from the mapper and assigns the partition. Partitioning specifies that all the values for each key are grouped together and make sure that all the values of a single key go to the same reducer.**
5. **The partitioned data is written to the local disk for each mapper.**
6. **During the shuffling phase, Hadoop MapReduce takes the output files produced by partitioners** and downloads them to the reducer machine, via HTTP. And the purpose of the sort is to group keys together.
7. **This way, the reducer task can easily iterate over values. Reducer then takes each key and iterates over all the values associated with that key. In our case, we just sum up all the values for the key. And the output of the reduce task is written to the file system.**

**The Top K MapReduce job takes this data, splits it into chunks, and sends each chunk to a mapper that calculates a local top k list. Then all the individual top k lists are sent to the single reducer that calculates the final top k list. As you may see, the Top K MapReduce is based on exactly the same idea we discussed before:**

- **Partition the data, find the top k list for each partition and merge individual lists into the one final list.**

### Data retrieval path
![[Screenshot 2023-07-23 at 2.09.09 PM.png]]
merge 1-hours lists to get 2 hour-list will not be 100% aggregate

### Drawbacks of Lambda Architecture
Send events to a batch system and stream processing system in parallel and then stitch together the results in query time
The main problem is complexity, the slow path is significantly more complex than the fast path

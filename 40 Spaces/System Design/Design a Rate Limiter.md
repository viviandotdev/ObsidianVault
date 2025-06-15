---
created: 2023-11-16 15:25
modified: Thursday 16th November 2023 15:25:39
alias:
---
up::  [[system-design]]
tags:: [[system-design]]

## Design a Rate Limiter

### Requirements
**What is a rate limiter**?
A rate limiter is a system limits the number of user requests allowed to be sent over a specified period.
**For example:**
- A website might restrict users to download a maximum of 5 large files (over 100 MB) per day
- A bank may enforce a limit where a credit card holder can perform a maximum of 10 transactions in a day

**Benefits of a Rate Limiter**
- Protects services from malicious activities, such as DDOS attacks and brute force attempts on passwords or credit card information.
- Reduce costs and resource usage, by efficiently managing resource consumption. Effective rate limiting is important for companies using third-party APIs that charge on the per-call basis. By restricting the number of calls to APIs, businesses can significantly reduce costs.

**Functional Requirements**
- Define Limits: Ability to set different rate limit rules for different resources
- Error Handling: Users should be notified when their requests are throttled.

**Non-Functional Requirements**
- Available and Fault Tolerant: The rate limiter should be resilient to failures, since it protects our service from malicious attacks.
- Scalable: The rate limiter is distributed, they are spread across multiple servers and can handle increased traffic volumes.
- Accurate: The rate limiter should accurately enforce the defined rate limiting rules.

### Where to rate limit?
Rate limiting is usually implemented within a component called [[API Gateway is an abstraction layer between the front end and backend microservices that routes the request sent from the client to the correct backend service.]] An API gateway acts as a centralized entry point for client requests in an application that uses multiple backend microservices.

TODO:  Api Gateway excalidraw image
### Rate Limiting Algorithms
**Token Bucket Algorithm**
A token bucket is like a container filed with tokens. The bucket has a maximum size it can hold, and tokens inside represent requests.

These algorithm takes in two parameters:
**Bucket Capacity:** The maximum capacity of the bucket, let's say 10 tokens maximum.
**Token Refill Rate:** The constant rate at which tokens are added back into the bucket, for instance, 2 tokens per second.

**Algorithm Steps**
1. When a client sends a request it requires a certain number of tokens to be fulfilled (let's say 3 tokens per request)
2. The rate limiter checks if the bucket has enough tokens
	1. If there are 3 or more tokens available, the request is processed, and 3 tokens are taken from the bucket.
	2. If there are fewer than 3 tokens available, the request is dropped since there aren't enough tokens to fulfill it.

**Benefits:**
	- It's relatively straightforward to understand and implement.
	- Provides flexibility in setting the bucket size and refill rate.
**Limitations:**
	- It may be difficult to tune the parameters refill rate and bucket size that would be optimal for all scenarios.
	- It might not be able to handle sudden massive surges well if the bucket capacity is smaller than the peak demand.

**Sliding Window Algorithms**
- **Fixed Window Counters:**
	- Divide the timeline into fixed window sizes and assign a a number of allowed request to each window
	- Count the number of requests in each time interval, if the request is less than the allowed request, it request goes through
- The main issue with fixed window rate limiting is there might be overload of requests in the edges.
- **Sliding Window Log**:
	- Map a user id to an array of requests with timestamps
	- Each time a new request comes in **remove** the requests with outdated time stamps.
	- **Add** the timestamp of the new request
	- If the updated array size is greater than the allowed count, this request is rejected, else it is accepted
- This algorithm fixes the issue where spikes in traffic at the edges of the fixed window will cause more than the allowed request to go through. However this. algorithm consumes a lot memory because each request will be need to be stored with a timestamp.
- **Sliding Window Counter**:
	- Combines fixed window and window log algorithm
	- Divide the timeline into fixed window sizes. In each window we will store the counts of the request in that window.
	- Estimate the number of requests in the rolling window by using a formula:
		- current window requests + (previous window requests * overlap percentage of rolling window and previous window)
	- If the number of requests is less than the allowed count reject the request else accept the request.
- This algorithm uses the fix window algorithm where it keeps track of the counts in each window instead of a timestamp for each request, making it more memory efficient. It also using the window log algorithm because instead of just looking at the count of requests in the fixed window we estimate the number of requests in the rolling window using a formula.
- However this is not 100% accurate because it **assumes that the requests in the previous window is evenly distributed** which may not always be the case.
### System Components
**In-memory Cache:** Stores the counters, which keeps track of how many requests are sent from the same user.
	**Benefits of using an in memory-cache**
	- Accessing an in-memory cache is fast, which is crucial for rapidly updating and retrieving counters in real-time.
	- Redis supports atomic operations, this allows multiple operations to be executed in a single transaction, this is important for incrementing counters while maintaining consistency and avoiding race conditions
**Rate limiter middleware:** fetches rate limiting rules and runs the rate limiting algorithm to determine if the request can be passed through to the API servers.

### System Architecture
![[rate limiter architecture diagram]]
1. Client sends a request to the server
2. The request goes through the rate limiter middleware
3. The rate limiter fetches the counters for the current window and previous window request and then computes the estimates the number of requests in the rolling window and compares with allowed number of requests
	- If the request is rate limited, return HTTP 429 too many request error to the client and the request is dropped
	- If the request is not rate limited forward the request to the API servers

### Distributed Rate Limiter
**Synchronization**
In a distributed environment, a single user might send requests to API servers across various regions each with it own rate limiter. To effectively enforce rate limits for this user's request we need a centralized global data store such as Redis. A centralized data store ensures synchronization between the different rate limiter, allowing them to maintain consistent counts of the user's requests regardless of the server which they interact with

**Race Condition**

in a distributed system where multiple components or servers are enforcing rate limits independently, a race condition can occur when two or more components concurrently check whether a user has reached their limit and allow a request to pass through. This race condition arises due to the asynchronous nature of the system, **where multiple processes are attempting to access and modify shared resources simultaneously.**

Let's say there are two servers running rate limiters for a particular user. Both servers use a shared data store (like Redis) to keep track of the user's request count. When a request comes in, both servers independently check the user's request count to determine if it exceeds the limit.

1. Server A checks the count and finds that the user is below the limit.
2. Meanwhile, at the same time, Server B also checks the count and sees the user is below the limit.

Both servers, seeing that the user is below the limit based on their individual checks, allow the request to proceed.
A Race condition occurs. It's possible for both servers to see the user's count as below the limit before any of them updates the count
To prevent this race condition, locks can be used to ensure mutual exclusion when accessing and updating the shared resource (in this case, the user's request count in the data store). When a server wants to check the count and potentially update it, it first acquires a lock. While the lock is held, no other server can access or modify the count.

By using locks to enforce exclusive access to the shared resource (the user's count), only one server can modify it at a time, preventing the race condition and ensuring that the rate limiting logic is consistently applied across servers in the distributed system.
However locks slow down the system
### Review of the Requirements
- **Accuracy** The following rate limiting algorithms, token bucket, sliding window, fixed window can accurately limit requests with minimal errors
- **Scalable** In a distributed environment, we can use a load balancer to distribute requests. The load balancer is managing requests across multiple servers and multiple data centers. We have multiple implementations of the rate limiter, as every data center has its own implementation of this middleware.
-
![[Screenshot 2023-12-01 at 9.03.07 AM.png]]

![[Screenshot 2023-12-01 at 9.03.17 AM.png]]

![[Screenshot 2023-12-01 at 9.03.40 AM.png]]

![[Screenshot 2023-12-01 at 9.03.43 AM.png]]

![[Screenshot 2023-12-01 at 10.04.11 AM.png]]




### Sources
[youtube.com/watch?v=mhUQe4BKZXs&themeRefresh=1](https://www.youtube.com/watch?v=mhUQe4BKZXs)

[Rate Limiter with Sliding Window Algorithm - YouTube](https://www.youtube.com/watch?v=Ph9odgg8wQ0)

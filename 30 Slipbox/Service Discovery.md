---
created: 2023-07-25 17:55
modified: Wednesday 9th August 2023 19:12:59
alias:
---
up::
tags::
related:  #system-design

## Service Discovery

**Service discovery: Mechanism used in distributed systems to locate and communicate with services and resources**

**Server side discovery:** The client makes a call to a discovery service registry and the discovery service makes the request to the correct service on the client's behalf

**Pros:**
Clients receive service instance recommendations from the registry, simplifying client code. The service registry can also perform additional functions like health checks and service monitoring.

**Cons**
The service registry becomes a potential single point of failure or bottleneck. Clients may have limited control over load balancing and service selection, as it is determined by the registry’s policies. Clients need to make additional network requests to the registry, which may introduce latency.

**Client side discovery:** In client-side discovery, the responsibility of service discovery lies with the client. The client makes a request to a discovery service to find out which service to call. Then the client will also make the call to the correct service.
**Pros**
Clients are aware of a service registry or a centralized service discovery mechanism

Clients have more control over load balancing, failover, and service selection. Clients can implement custom algorithms or policies based on their specific requirements. It allows for more flexible and dynamic client behavior.

**Cons**
Clients need to be aware of the service registry and handle the discovery process, which adds complexity to the client code. Clients may also need to implement additional logic for service selection, load balancing, and fault tolerance.

### Resources
[What is service discovery really all about? - Microservices Basics Tutorial - YouTube](https://www.youtube.com/watch?v=GboiMJm6WlA&list=PLqq-6Pq4lTTbEzejFKFRYfkLGYyOOwq58&index=4)

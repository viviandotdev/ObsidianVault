---
created: <% tp.file.creation_date() %>
modified: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
alias:
---
up::
tags:: #system-design #system-design/availability #system-design/reliability
related:

## Load Balancer
Technologies: (NetScaler, NGINX, AWS ELB)

**Evenly distributes events across partitioner service machines.** The load balancer receives the data from the API Gateway and distributes it across **multiple instances of the same service**. The load balancer ensures that the incoming data is evenly distributed to maintain a balanced workload across the partitioner service instances.


## Load Balancer Algorithms
1. Round Robin: Requests are distributed in a cyclic order, ensuring each server receives an equal share of the traffic.
2. Least Connections: Incoming requests are sent to the server with the fewest active connections to evenly distribute the workload.
3. Least Response Time: Requests are directed to the server with the lowest average response time or latency to minimize overall response times.
4. Hash-based Algorithms: Requests are routed to specific servers based on a hashed attribute (e.g., client IP address), ensuring consistent handling for requests with the same attribute

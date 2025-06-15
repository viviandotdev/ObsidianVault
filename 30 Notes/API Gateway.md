---
created: 2023-07-25 17:55
modified: 2025-06-15T07:04:49-04:00
alias: 
---
up::
tags:: [[system-design]]
related:

## API Gateway
API Gateway is an abstraction layer between the front end and backend microservices that routes the request sent from the client to the correct backend service.
### What problem does this solve?
An API gateway acts as a centralized entry point for client requests in an application that uses multiple backend microservices. **It provides an abstraction layer that shields the frontend (UI) developers from dealing directly with the complexity of calling individual microservices**. Instead, the UI developer can simply make requests to the API gateway, which handles the logic of routing the requests to the appropriate backend microservice. This simplifies the frontend code and promotes better separation of concerns between the UI and backend services.

![[Screenshot 2023-08-06 at 12.01.32 PM.png|400]]
Step 1 - The client sends an HTTP request to the API gateway.
Step 2 - The API gateway parses and validates the attributes in the HTTP request.
Step 3 - The API gateway performs allow-list/deny-list checks.
Step 4 - The API gateway talks to an identity provider for authentication and authorization.
Step 5 - The rate limiting rules are applied to the request. If it is over the limit, the request is rejected.
Steps 6 and 7 - Now that the request has passed basic checks, the API gateway finds the relevant service to route to by path matching.
Step 8 - The API gateway transforms the request into the appropriate protocol and sends it to backend microservices.
Steps 9-12: The API gateway can handle errors properly, and deals with faults if the error takes a longer time to recover (circuit break). It can also leverage ELK (Elastic-Logstash-Kibana) stack for logging and monitoring. We sometimes cache data in the API gateway.
### Resources
[What is API gateway really all about?](https://www.youtube.com/watch?v=1vjOv_f9L8I&list=PLqq-6Pq4lTTbEzejFKFRYfkLGYyOOwq58&index=11)

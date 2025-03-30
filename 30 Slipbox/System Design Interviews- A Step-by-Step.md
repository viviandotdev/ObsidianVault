---
created: 2023-10-15 09:41
modified: 2025-03-30T11:43:52-04:00
alias: 
Status: idea
Category: system-design
---
up:: [[System Design MOC]]
tags:: #system-design

### System Design Interviews: A Step-by-Step Guide

1. **Requirements Classifications (5 minutes)**
	Ask **clarifying questions** to understand the exact scope of the problem.
		Is this a mobile app? Or a web app? Or both?
		What are the most important features for the product?
		Can feed contain images, videos, or just text?
		Are we focusing on the backend only, or are we developing the front-end too?
		What are the performance expectations in terms of requests per
	**Functional Requirements**
	What endpoints and methods will the API have? For a key-value store, an example would get
	`get(key)`
	`put(key, value)`
	**Non-Functional Requirements:**
	- Performance
	- Scalability
	- Availability
	- Consistency
2. **Define the data model (2-3 minutes)**
	1. Choose database models
	2. Create scalability and sustainability
	Map out data flow among system components.
		- What type of data will the system handle?
		- Discuss tradeoffs between which database to use?
		- Discuss SQL vs NoSQL Databases
3. **Propose high-level design (10 - 15 minutes)**
	- Create the initial blueprint for core components such as the clients, servers, data stores, APIs, message queue etc.
	- Back of envelope calculations to validate your design decisions
4. **Detailed Design (10–25 minutes)**
	- Identify 2 - 3 components you want to further discuss with the interviewer.
		- Discuss pros and cons and consider the tradeoffs between the different options
5. **Identifying Bottlenecks and potential improvements (3-10 minutes)**
		- Are there any single points of failure?
		- Do we have enough replicas so that our system is fault-tolerant?
		- Error cases (server failures and network losses)
		- How to handle larger scale?
		- How will we monitor the performance of our service?


### Resources
[System Design Interview: A Step-By-Step Guide - YouTube](https://www.youtube.com/watch?v=i7twT3x5yv8)
[Complete Guide to System Design Interviews (and Top Questions) - Exponent](https://www.tryexponent.com/blog/system-design-interview-guide)
[Complete Guide to System Design Interviews (and Top Questions) - Exponent](https://www.tryexponent.com/blog/system-design-interview-guide?src=footer)



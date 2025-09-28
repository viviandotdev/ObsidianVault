---
created: 2024-01-16 12:57
modified: Tuesday 16th January 2024 12:57:12

---
up:: [[01 System Design Problems]]
tags:: [[system-design]]

[Designing INSTAGRAM: System Design of News Feed - YouTube](https://www.youtube.com/watch?v=QmX2NPkJTKg)

**News Feed System**

**Functional Requirements**
1. Publish posts- A user create a post and we save it to the cache and database.
2. View posts- To view posts, we aggregate the your friends' posts and display them in the order of most recently created.

**Non-functional requirements**
- **Low Latency**- the system should have a fast response time
	- cache
- **Scalable**- the system should handle a growing number of users and posts. As we have more users and posts, we need to scale our system by distributing our data onto multiple machines such that we can read/write efficiently.
	Sharding posts and metadata
	As we have more users and posts, we need to scale our system by distributing our data onto multiple machines such that we can read/write efficiently.

	Sharding feed data
	Since we only store a limited number of feeds in memory, we shouldn't distribute the feed data of one user onto multiple servers.
	We can partition the user feed data based on userId. We hash the userId and map the hash to a cache server. We would need to use [consistent hashing](https://liuzhenglaichn.gitbook.io/systemdesign/consistent-hashing).

- **Available**- the news feed should be highly available minimizing downtime and ensuring users can access the new feed at all times.
- master slave replication
	- read replicas, since this system will handle more reads than writes, there will much more users view posts than people uploading posts. this will help scalability and availability.

#### API
This endpoint allows users to create a new post
**POST: /publish**
Params:
	post_content: content of the post
	auth_token: used to authenticate users

This endpoint retrieves the latest posts from the user's friends..
**GET: /newsfeed**
Params
	auth_token: used to authenticate the request


#### Database Schema (NoSQL vs SQL)
Use a relational database like SQL because the database is highly related
![[Screenshot 2024-01-18 at 8.47.40 AM.png]]
[User Friends System & Database Design - by Herry Gunawan](https://www.thescalable.net/p/user-friends-system-and-database#%C2%A7two-way-friend-system)

You can follow other users without their consent
following_id
follower_id
if you are user with (userId 10) and you follow user with userId(15)
**You follow a user**
INSERT into follows (follower_id, following_id )
you are the follower (10) and are following userId (15)
**Get the the list of users you follow**
SELECT * FROM follows where (followerd is 10)
you are the follower and want to get all the users you are following
**Get all the users that are following you**
SELECT all from follows where  **followingID** is 10
you are being followed by these users


#### System Components
[[API Gateway is an abstraction layer between the front end and backend microservices that routes the request sent from the client to the correct backend service.]]- Centralized gateway that redirects client requests to the correct backend services/
## Publish Posts
1. User makes a request to the endpoint **/publish**
2. The request
**Post Service**- Stores created post in database and cache
**Fanout Service** - Sends new post to the feeds of its friends
	This service delivers posts to all friends. This is distributed message queue
		1. Fetch follower id data from the **graph database**
		2. Get friends info from the user cache and filter out friends that are muted.
		3. Sends friends list and new post id to the message queue
		4. Fanout workers fetch the data from the message queue and store the news feed data in the news feed cache. Append the new post to the news feed cache table
	Fan out **push** vs fanout **pull**
		- Fanout on write, new posts are **pushed** to the friends' caches **immediately after publication**.
			- Fast, because the news feed is already pre generated
		- Fanout on read, when the user loads their page the new feed service pulls the recent posts
			- Slow because the feed is not pre generated
**Hybrid Approach**
 **Celebrities** who have a lot of followers will use **fanout on read**, this is because fetching the follower. list of celebrities and generating new feed for all them is slow.
 **Normal people** will **fanout on write** because they don't have the hotkey problem.

**Notification Service**- Notifies the friends that new content is available on their feed
1. Notification service fetch metadata such as user info, and user notification settings from the users cache or database.
2. Sends list of users to message queue for processing
3. Consumers pull notification events from the message queue and sends them to third party services.
![[2024-01-18.excalidraw]]
## View Posts
Fetches data from the newsfeed database or cache

1. User makes a request to the endpoint **/newsfeed**
2. The web server calls the news feed service to fetch news feeds.
3. The news feed service listens for user upload requests to start the feed generate service. If it is a push the newfeed is already generated we can send it directly to client. Else if it is pull we need to generate it, by getting a list of postID it needs to show from the users followers list.
4. The new feed service uses the postID and userID to fetch the complete post and user data from their respective caches.
5. Generate a hydrated new feed in JSON format and send that data back to the client

![[2024-01-18_0.excalidraw]]

### Resources
[Instagram System Design. Overview | by Nikhil Gupta | Medium](https://nikhilgupta1.medium.com/instagram-system-design-f62772649f90

[Design Facebook | Twitter | Instagram news feed system| System Design Interview Question | by Shrutika Poyrekar | Medium](https://medium.com/@mumbaiyachori/design-facebook-twitter-instagram-news-feed-system-system-design-interview-question-393a8ccf57ef)

[Design a News Feed System - System Design](https://liuzhenglaichn.gitbook.io/system-design/news-feed/design-a-news-feed-system)

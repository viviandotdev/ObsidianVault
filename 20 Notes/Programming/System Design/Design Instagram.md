---
created: 2024-01-16 12:22
modified: 2025-06-15T18:27:14-04:00

---
tags::  [[system-design]]

**Functional Requirements**
1. Users can follow other users
2. Users can view a feed of content from the people they follow
3. Users can post images or video
4. Users can like, comment and share on others posts
**Non Functional requirements**
- Read heavy there will more people reading and looking posts then uploading and creating posts
- **Low latency** when viewing photos
- **Reliable**- Data store for images and content should be reliable, data should not easily lost.
- **Available**- the system must available and handle network failures.

### API
### **User API**
**Endpoint:**  POST `/signin`
**Parameters**:
- `email` (string, required): account email creds
- `password` (string, required): account password
**Response**
-  `success` (boolean): Indicates whether the signup was successful or not.
- `message` (string): Describes the outcome of the signup process.
- `user` (object): : Details about the signed-in user.

**Endpoint:**  POST `/signup`
**Parameters**:
- `username` (string, required): account user name
- `email` (string, required): account email
- `password` (string, required): account password
**Response**:
-  `success` (boolean): Indicates whether the signup was successful or not.
- `message` (string): Describes the outcome of the signup process.
- `user` (object): Details about the newly created user.
**Endpoint:** POST `/follow`
**Parameters**:
- `auth_token` (string, required): authenticate logged in user
- `user_id` (string, required): ID of the user to be followed.
**Response**:
-  `success` (boolean): Indicates whether the follow action was successful or not.
- `message` (string): Describes the outcome of the follow action.
- `follower` (object): Details about the follower user.
- `user_to_follow` (object): Details about the user who was followed.

### Posts API
**Endpoint**: POST `/post`
**Parameters**:
- `auth_token` (string, required): authenticate logged in user
- `content` (string, required): content of the post
**Response**:
-  `success` (boolean): Indicates whether the follow action was successful or not.
- `post` (object): Details about the created post
**Endpoint:** GET `/newsfeed`
**Parameters:**
- `user_id` (string, required): ID of the user requesting the newsfeed.
- `limit` (integer, optional): Maximum number of posts to retrieve.
- `offset` (integer, optional): Offset for pagination.
**Response:**
- `success` (boolean): Indicates whether the request was successful or not.
- `message` (string): Describes the outcome of the request.
- `newsfeed` (array of objects): List of posts in the newsfeed.
### Data Model
- **Users:** Each user has a unique identifier, profile information, followers, following, etc.
- **Posts:** Posts contain content (text, images, videos), metadata (time, location), and are associated with the user who created them.
### System Components
[[API Gateway]] abstraction layer between front and backend services that routes request sent from the client to the correct backend service.
	**Auth Service** (Authenticates and Authorizes User)
	**Rate Limiting**
[[Load Balancer]] distributes incoming client requests across multiple servers evenly to ensure high availability and reliability
**API Servers**
	**Posts Service**
		**Create Posts**- Link to Write posts in news feed generation
	 **Feed Service**
		 **Get Posts**- since we have more reads that writes we may want to use the [[Master Slave Replication]] pattern to distribute the load for reads. (Link to View Posts in news feed generation)
	 **Fanout Service**- distributes new post content to the multiple followers of a user.
**Database Servers**
	SQL- Stores structured data like user profiles, account information
**Object Storage S3** - designed to store and retrieve unstructured data such as images, and videos,
**Metadata DB** (what is a metadata DB stores the **reference id** t o the files in our object storage such as S3)
	**ObjectID**- Unique identifier for each object stored in S3.
	**BucketName**: Name of the S3 bucket where the object is stored.
	**UserId**- user who posted
	**Size**: Size of the object in bytes.
	**ContentType**: MIME type or content type of the object.
	**LastModified**: Timestamp indicating the last modified time of the object.>)



### Resources
[Designing Instagram](https://www.designgurus.io/course-play/grokking-the-system-design-interview/doc/638c0b61ac93e7ae59a1afbd)
[Instagram System Design](https://www.enjoyalgorithms.com/blog/design-instagram)
[Instagram System Design. Overview | by Nikhil Gupta | Medium](https://nikhilgupta1.medium.com/instagram-system-design-f62772649f90)
[Facebook System Design | Instagram System Design | System Design Interview Question - YouTube](https://www.youtube.com/watch?v=9-hjBGxuiEs)
[User Friends System & Database Design - by Herry Gunawan](https://www.thescalable.net/p/user-friends-system-and-database#%C2%A7two-way-friend-system)

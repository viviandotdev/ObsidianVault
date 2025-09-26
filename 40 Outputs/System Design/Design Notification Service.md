---
created: 2023-08-07 17:43
modified: Monday 7th August 2023 18:39:37

---
up::  [[system-design]]
tags:: [[system-design]]
related:
## Design Notification Service

[System Design Interview - Notification Service - YouTube](https://www.youtube.com/watch?v=bBTPZ9NdSk8)
[Messaging Pattern: Publish-Subscribe - A. Rothuis](https://www.arothuis.nl/posts/messaging-pub-sub/)
Create a system that sends a message in reaction to a certain event
### System Requirements
**Functional Requirements:**
1. Send Notifications
2. Pluggable and extendable
**API**
createTopic(topicName)
publish(topicName, message)
subscribe(topicName, endpoint)
**What is a topic?**
	Notifications can have different topics or channels associated with them, indicating their type or purpose, ex: "UserEvents", "OrderUpdates", "Promotions"
	When a publisher sends a notification to a topic, the message broker ensures that all subscribers who have expressed interest in that topic receive the notification.

**Non-Functional Requirements:**
1. Scalable: Handle many publishers, topics and subscribers
2. Available
3. Durable: messages are delivered to subscribers at least once.
4. Performant: messages are sent to subscribers quickly

[[04:35]]
### Pub Sub Pattern
**Publishers** publish notifications to specific topics on the message broker.
**Subscribers** express interests in specific topics by subscribing to them on the message broker. Subscribers provide callback functions or endpoints to receive notifications when they are published.
**Delivery** Message broker ensures that all subscribers who have expressed interest in that topic receive the notification. The message broker sends a copy of the notification to each interested subscriber's callback function or endpoint.
![[Screenshot 2023-08-09 at 10.30.48 AM.png]]
### High level architecture
![[Screenshot 2023-08-09 at 10.33.55 AM.png]]

**Service 1 to N:** They represent different services that triggers notification send events and send notifications via APIs provided by the notification servers.
Examples: Billing service that sends emails to remind customers a payment is due or a shopping website that tell customers that their package will be delivered tomorrow
**Notifications Servers:** (**Publisher**)
1. Provide the APIs for services to send notifications and build notifications payloads for third party services.
2. Carry out validations to verify contact info, email, phone numbers
3. Query database or cache to fetch the metadata needed to render a notifications
4. Push notification data to message queues for parallel processing
- [[09:19]]
**Metadata Database and Cache**
**Cache**: Frequently used, user info, device info and notifications templates are cached. (Redis)
**Database**: stores contact info, user data, notifications
Discuss the tradeoff between SQL vs **NOSQL**
	(we don't need acid operations, or need to run complex dynamic queries)
Cassandra: column or key-value store

**Workers**: Pulls notifications events from the message queues and sends them to the third party services.
1. A service calls APIs provided by notification servers to send notifications.
2. Notification servers fetch metadata such as user info, device token, and notification setting from the cache or database.
3. A notification event is sent to the corresponding queue for processing. For instance, an iOS push notification event is sent to the iOS PN queue.
4. Workers pull notification events from message queues. 5. Workers send notifications to third party services.
6. Third-party services send notifications to user devices.

- [[11:47]]
**Message Queue**
They **remove dependencies between components**. Message queues serve as buffers when high volumes of notifications are to be sent out. Each **notification** **type** is assigned with a distinct message queue, so an outage in one third-party service will not affect other notification types.
Technologies: Amazon SQS, RabbitMQ
**Third Party Services**
1.  Delivers notifications to users
2. These services subscribe to the message queue with notifications of their type. Therefore, when will only receive notifications of their type and send them out to the users.
3. While integrating with third-party services, we need to pay extra attention to extensibility. Good extensibility means a flexible system that can easily plugging or unplugging of a third-party service.
### Detailed Design
![[Screenshot 2023-08-09 at 11.13.03 AM.png]]
**How do we prevent data loss?**
1. Notification systems must be durable and cannot lose data. To satisfy this requirement, the notification system persists data in a database and implements a **retry mechanism.
	-  When a third-party service fails to send a notification, the notification will be added to the message queue for retrying. If the problem persists, an alert will be sent out to developers.**
**Will recipients receive a notification exactly once? [[21:00]]**
- Dedupe mechanism to handle duplicate notifications from retries
	- When notification arrives, check if we have seen it before by checking the eventID if seem before discard it, else send the notification.
**Rate Limiting**
To avoid overwhelming users with too many notifications, we can limit the number of notifications a user can receive. This is important because receivers could turn off notifications completely if we send too often.
In addition, we can register subscribers, email owners need to confirm the subscription.
**Security in push notifications**
For iOS or Android apps, appKey and appSecret are used to secure push notification APIs. Only authenticated or verified clients are allowed to send push notifications using our APIs. Interested users should refer to the reference material.
**Monitor queued notifications**
A key metric to monitor is the total number of queued notifications. If the number is large, the notification events are not processed fast enough by workers. To avoid delay in the notification delivery, more workers are needed.
**Events tracking**
Notification metrics, such as open rate, click rate, and engagement are important in understanding customer behaviors. Analytics service implements events tracking. Integration between the notification system and the analytics service is usually required.
**Notification Templates**
Provide efficient notification creation. We can reuse templates for notifications with similar format.
![[Screenshot 2023-08-09 at 5.44.47 PM.png]]

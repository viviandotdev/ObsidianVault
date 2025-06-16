---
created: 2024-04-10 15:27
modified: Wednesday 10th April 2024 15:27:44
alias:
Status: hold
Category: system-design
tags: "[[system-design]]"
---
up::  [[system-design]]

source::
## Design a Payment System
Try to do most of this without looking at the summarized information,
Watch a high level summary on youtube on what you need to know .
with notebook in hand only write down information that is insightful, just absorb the information at the high level,
Look at the system design book at look through the sources watch the content to build your own notes and summary
How to create a system design articles?
What is the problem what system are you trying to build?
What are the requirements and features of the system?
What are the non-functional requirements of the system?
	how will the system full-fill these requirements
What are the components of the system?
How will the components talk to each other?
Read engineering blogs about real world systems
Day one- gather resources, you will look at into, articles and videos to watch,
Day-2-4, take notes on the resources and create an article on the system design.

**Problem**:
Build a payment backend system for an e-commerice application. The customer places an order on the site and the payment handles everything to settle the transaction.

What are the Functional Requirements
What are the Non-Functional Requirements
**Functional Requirements**
Pay In- the payment system receives money from customers on behalf of the sellers.
Pay Out- the payment system sends money to sellers around the world


**Asynchronous Payments**
Async Communcation

**System Components**



#### Sources
[Scaling Airbnb’s Payment Platform | by AirbnbEng | The Airbnb Tech Blog | Medium](https://medium.com/airbnb-engineering/scaling-airbnbs-payment-platform-43ebfc99b324)






Payment Flow- How do payments work?
https://stripe.com/guides/introduction-to-online-payments

Players
1. Cardholder- the user with the credit card
2. Merchant- the seller or business owner
3. Acquirer- bank that processes the card payments for the merchange,
    and routes them through card networks( Visa, Mastercard, etc.)
4. Issuing bank, the bank that extended credit and issues cards to
customers (Chase?)


Steps
1. Establish relationship with acquirer or payment processor
2.

---
created: 2024-04-22 18:31
modified: Monday 22nd April 2024 19:41:23

---
up::  [[Joy of React]]
tags:: #note/atomic
source::
## Why did facebook build react?

In the context of Facebook's chat system, using a traditional [[Model View Controller]] architecture could lead to issues such as phantom chat notifications due to the circular dependencies between components. Let's explore how this might happen:

### Traditional MVC Architecture

In a traditional MVC setup, the Model represents the data layer, the **View** displays the data (UI layer), and the **Controller** handles the input, updating the Model or the View accordingly.

### Scenario: Phantom Chat Notifications

Imagine a scenario where you have two main components in the chat system:

1. **View1 (Chat List)**: This shows a list of all the chats.
2. **View2 (Unread Messages Counter)**: This displays the number of unread messages.

Both of these views depend on **Model1 (Chat Data Model)**, which holds information about the chat messages, including whether they have been read.

### The Problem

1. **User Reads a Message**: When a user reads a message, View1 (Chat List) updates Model1 (Chat Data Model) to mark the message as read.
2. **Model Updates View2**: Model1 then notifies View2 (Unread Messages Counter) to decrement the count of unread messages.
3. **Circular Dependency Issue**: In an MVC architecture where updates are bidirectional, updating the Model based on changes in one View can inadvertently trigger updates in another View. If not carefully managed, this can lead to situations where View2 might update Model1 (e.g., to reset some state or due to another logic tied to the unread messages count), which then tries to update View1 or View2 again, creating a loop.

### Phantom Notifications

A "phantom" notification could occur if, due to these circular dependencies and updates, the Unread Messages Counter (View2) gets out of sync with the actual number of unread messages. For example:

- The counter might decrement, indicating a message has been read, but due to a loop in updates and notifications, it might not accurately reflect the actual unread messages.
- Alternatively, a user might receive a notification for a new message, but upon checking, finds no new messages, because the notification was a result of the system incorrectly handling the state changes due to the circular dependencies.

### Flux Solution

Flux architecture addresses these issues by enforcing a unidirectional data flow:

1. **Actions**: User interactions or system events that describe what happened.
2. **Dispatcher**: Manages the actions and dispatches them to the appropriate stores.
3. **Stores**: Hold the application's state and logic, updating the state based on the actions received.
4. **Views**: Reflect the state of the stores, updating to represent the current state.

In Flux, when a user reads a message, an action is dispatched, and the relevant store updates the state (e.g., marks a message as read and updates the unread count). The Views then update based on the new state. This unidirectional flow prevents the circular dependencies and the issues like phantom notifications seen in MVC architectures.



![[Screenshot 2024-04-22 at 7.59.00 PM.png]]
Initially facebook has an external control method of handle actions. The action would do through a handler and the handler will control the three different elements. This is not scalable because as we add more features and components the handler gets increasingly more complex. The handler is a piece of code that manages the action. Based on the action the handler decides whether add or remove messages to each component.


![[Screenshot 2024-04-22 at 8.00.36 PM.png]]
A better solution would be to move the **control to the individual components so that the state is right next to the logic that updates that state**



**Linked References to this Note**
These notes point directly to this note. But this note doesn't point back.
```dataview
LIST
FROM [[#]]
and !outgoing([[#]])
and -#map

SORT file.link asc
```

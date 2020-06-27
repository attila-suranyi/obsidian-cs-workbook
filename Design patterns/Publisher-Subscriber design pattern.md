
## Publisher/Subscriber design pattern

### Reference
- Source:
	- https://hackernoon.com/observer-vs-pub-sub-pattern-50d3b27f838c
	- https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern
	- https://docs.microsoft.com/en-us/azure/architecture/patterns/publisher-subscriber
- Keywords:
	- #designPattern, #computerScience
- Relevant notes:
	- [[Observer design pattern]]
	- [[Message queue]]
	- [[Message broker project]]

### Concept
#### Problem
In cloud-based distributed systems sending messages between components is often required. In a synchronous fashion the sender would wait for the receivers response, whether it got the message or not. This blocking can cause prolonged waiting time, especially if the receiver is not available or overloaded.

#### Solution
Using an asynchronous process to transfer a message to a middleware that takes care of the message.

The Pub/Sub pattern is similar to the [[Observer design pattern]], but there is a third component, a [[Message queue|message broker]].

![[observer vs sub-pub pattern.png]]

#### Observer vs Pub/Sub pattern
- In Pub/Sub pattern the sender and receiver don't know anything about each other.
- In Observer pattern the process is usually **synchronous**.
- Observer pattern needs to be implemented in a single application address space -> **intra**-application usage, while Pub/Sub pattern is used in **inter**-application communication.

#### Advantages
- Decouples components.
- Message handler is an independent system, so it will still operate if other systems don't.
- Separation of Concerns.
- Sender can continue to work because of asynchrounity.
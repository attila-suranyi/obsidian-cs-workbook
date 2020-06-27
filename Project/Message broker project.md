# Message broker project

## Reference
- Relevant notes:
	- [[Message queue]]
	- [[Publisher-Subscriber design pattern]]
	- [[Sprint Plan]]

## Expectations 
- Routing messages to different exchanges according to headers: data-type, auto-delete, etc.
- Different exchange types: direct, topic, fanout
- Queue like data storage for messages
- Establish point-to-point and publish-subscribe message channels
- Message Broker deletes the message only when the receiver received it
- High test coverage through at least partial TDD

## Planning 
- __Custom HTTP request headers__ contain the necessary information (__routing key__) for the broker about the message handling, while the data in the body needs to be transfered
- Periodic notification of the receiver when message is available (according to _push_ technique)
- Dynamic publisher and subscriber list on publish-subscribe channels
- Subscribing needs authentication
- Periodic scan of messages and their durability and other properties:
delete if auto-delete set, or queue reached max size, or receiver got the message, etc.
- Layers separated by interfaces
- **Multithreading** for the different queues and subscribers, while the broker manages the thread pool.


## Would be nice to have
- Security through encrypted messages and encryption keys
- Appropriate traffic testing
- Work queue as load balancer

## Questions
- How to store messages? DB? How to easily build queue like structure?
- What to use for subcsriber authentication? Simple hashed password? JWT?

## Todo
[ ] Observer and publisher/subscriber design pattern
[ ] Redis
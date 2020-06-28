## Message queue
### Reference
- Source:
	- https://fulmanski.pl/tutorials/computer-science/big-data/message-queues/
	- https://www.cloudamqp.com/blog/2015-05-18-part1-rabbitmq-for-beginners-what-is-rabbitmq.html
-  Keywords:
	-  #computerScience 
-  Relevant notes:
	-  [[Publisher-Subscriber design pattern]]
	-  [[Message broker project]]

### Basics
![[message queue.png]]

- The __Receiver__ gets notified about the waiting message by the __Message Broker__. This is one of two techniques, the _push_ method.

- The application adding data doesn't necessarily know what particular application will end up retrieving the data.
- Queue manager stores the messages until a receiving application connects and takes the message.
- Before the message is completely removed from the queue it may be required that the process that reads the message confirm that it completed the transaction so the removal is possible and safe.
- A message consists of two basic parts, just as in any other communication protocol:
	 - __Header__ Information used by the messaging system that describes the data being transmitted, its origin, its destination, and so on.
	 - __Body__ The data being transmitted; generally ignored by the messaging system and simply transmitted as-is. 
- The message needs to be sent in __predetermined and predictable__ ways: to a particular, carefully choosen, _message channel_. Same for the receiving side.
When an application sends data, it doesn't randomly add it to any channel available; it adds the info to a __channel whose specific purpose is to share that sort of data__.
- There are two different kinds of message channels:
    - __point-to-point:__ Communication protocol used to establish a direct connection between two nodes.
    - __publish-subscribe:__ Communication protocol where senders called publisher do not sent data directly to specific receivers, called subscribers, but instead categorize published messages into classes without knowledge of which subscribers, if any, there may be. Similarly, subscribers express interest in one or more classes and only receive messages that are of interest, without knowledge of which publishers, if any, there are.


### Exchanges, routing keys and bindings
![[exchange.png]]

#### Standard message flow:
1. The producer publishes a message to the exchange.
2. The exchange receives the message and is now responsible for the routing of the message.
3. Binding must be set up between the queue and the exchange. In this case, we have bindings to two different queues from the exchange. The exchange routes the message into the queues.
4. The messages stay in the queue until they are handled by a consumer.
5. The consumer handles the message.

__Exchange:__ it is responsible for __routing__ the messages to different queues with the help of: __header attributes, bindings, and routing keys.__

__Binding:__ it is a __link__ that you set up to bind a queue to an exchange.

__Routing key:__ it is a message attribute the exchange look s at when deciding how to route the message to queues (depending on exchange type).

#### Exchange types
...

#### Options for message passing
- **Durability**: how to persist message.
- **Security policies**: which applications should have access to these messages?
- **Message purging policies**: queues and messages may have a *time to live*
- **Delivery policies**: do we need to guarantee that a message is delivered a certain amount of times? Once? At least once?
- **Batching policies**: do we send messages immediatly, or in packages?
- **Receipt notification**: do we notify the publisher that the message has been received? Bi-directional communication is needed (Request/Reply pattern)
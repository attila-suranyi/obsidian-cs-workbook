## Observer design pattern
### Reference
- Source: 
	- https://sourcemaking.com/design_patterns/observer
	- Head First design patterns
- Keywords:
	- #designPattern, #computerScience
- Relevant notes:
	- [[Publisher-Subscriber design pattern]]

### Concept
The goal is to decouple the message sender and receiver.

#### Example
Think of a newspaper company: the **publisher** publishes newspapers, the people who are interested can **subscribe** to a particular publisher, and every time there is a new edition, the newspaper will get from the publisher to the subscriber.

#### Definition
>The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.

#### Structure
![[Observer design pattern.png]]
- The **subject** and **observers** are decoupled through interfaces.
- Each subject can have many observers.
- Objects with the subject interface can `subscribe` and `unsubscribe` observers.
- The `notify()` method gets called when the subjects state changes, and it calls the observers `update()` method.

#### Advantages
- Loose coupling.
- Dependency Inversion: coding to interfaces.
- List of Observers is __dynamic__, and can change at runtime -> we don't need to alter the code after every new Observer
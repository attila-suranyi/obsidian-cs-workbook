# Guiding principles

## General

- ### SOLID principles
	>These principles help to keep our code flexible, maintainable, readable and __clean__.

	#### SRC: 
	Our method, class, module, layer should serve only one function, it should have only one responsibility.
	- Responsibility could be defined as a _reason to change the code_: 
	Consider a module that compiles and prints a report. Imagine such a module can be changed for two reasons. First, the content of the report could change. 
	Second, the format of the report could change. These two things change for very different causes.
	- This results many small classes with very precise names.
	- Separating the responsibilities makes our code more modular. We can more safely change one part of our code, without the need of touching other parts.

	#### Open-closed principle: 
	Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
	- Extend functionality by adding new code instead of changing existing code.
	- Goal is to keep the core of your system safe.
	- Using inheritance makes this easier.

	#### Liskov Substitution principle: 
	Any derived class should be able to substitute its parent class without the consumer noticing it.
	- Every part of the code should get the expected result, no matter what instance of a class you send to it, given it implements the same interface.
	- Duck parent class, RubberDuck subclass, inherited _quack_, _fly_, _swim_ methods. RubberDuck can't fly, overwrites inherited fly method.
	It violates the substitution principle, since RubberDuck can be used where Duck is used, but an unexpected behaviour will emerge when it uses the _fly_ method.
	- Another example: this is why we can't change the access modifier of a subclass to a more restrictive one.

	#### Interface segregation principle: 
	A client should never depend on methods it doesn't use.
	- Extract the needed method to an interface, so it will depend only on it.
	- Replace big interfaces with many small, specific ones.

	#### Dependency Inversion principle: 
	Never depend on anything concrete, only depend on abstractions.
	- High level modules should not depend on low level modules, they should depend on abstractions. We only use the interface, we don't care how it is implemented, the low level code should be decoupled, thus allowed the change independently.
	- Able to change an implementation easily without altering the high level code.
	- Eg.: If you later decide to change the ArrayList to a LinkedList, no problem, it is also a List, and you were forced to use the methods of the List interface in the first place, so changing to a LinkedList won't break anything.

	```java    
	List<> myList = new ArrayList<>();
	```

- ### What is Separation of Concerns?
    Very similar to the Single Responsibility principle: the essence is to break the code into **smaller parts**, so they are reusable, easier to develop and maintain. Multiple developers can work on different parts without effecting each other, or breaking another part of the application.

	Separation of concerns (SoC) is a design principle for separating a computer program into distinct sections such that each section addresses a separate concern. The modular code supports the principles of __encapsulation, information hiding, layered design, and well defined interfaces.__ 

- ### What is Dependency Injection?
	A technique whereby one object supplies the dependencies of another object.
	It can be achieved through setters, constructors and reflection.
	This makes mocking easier, and facilitates an important principle, the Separation of Concerns.

## Architecture

- ### Layered design
	>It is a client–server architecture applying the Separation of Concern design principle.

	The most widespread use of multitier architecture is the three-tier architecture:
	- presentation (client), 
	- application processing (logic), 
	- and data management functions are __physically__ separated. 

	As server applications got thicker and thicker, a couple of new layers were proposed:

	![[layered-architecture.png]]
	- a server-side __presentation or web layer__ connecting client-side actions with business services (e.g. controllers)
	- the __service/application layer__ contains complex "commands" that can change the state of the domain model (like a "money transfer" command in banking)
	- the __domain model__ deals with the fundamental entities of the given domain (like "accounts" in banking)
	- a data access or __persistence layer__ connecting business actions to data management services (e.g. DAOs)

	__The main points of this design:__
	- there should be separate components / layers (SoC)
	- the layers ideally should have a linear, hierarchical structure
	- the layers should interact only with their direct neighbor below them
	- this interaction should be asymmetrical: one may use the services of the the one below, and that's all.

	This way we can enjoy the advantages of SoC:
	developers can create flexible and reusable applications. By segregating an application into tiers, 
	developers acquire the option of modifying or adding a specific layer, instead of reworking the entire application.
	
- ### Microservice design
	Links:
	- https://www.brunton-spall.co.uk/post/2014/05/21/what-is-a-microservice-and-why-does-it-matter/
	- https://www.youtube.com/watch?v=j1gU2oGFayY
	- https://www.youtube.com/watch?v=DLRfT44e8uQ

	Before the microservice architecture:
	1. The applications were developed as a single, unified, __monolithic__ application, which contained everything it needed, since it
	was used on the users desktop computer.
	2. Applications got more and more __complex__ --> monolithic app development is difficult: deployment, testing, scaling.
	3. Then __web applications__ spread --> application is on a remote server --> we don't need to install the __whole__ app on __one__ machine!
	4. __Cloud services__ enable to create/destroy virtual servers with a click (load balancing).

	#### Microservices:
	A service oriented architecture composed of loosely coupled elements that have bounded contexts.

	- Small problem domain
	- Independently built and deployed (easily replaceable)
	- Communicate through well-known interfaces (HTTP)
	- Owns its own data storage

	#### Advantages:
	It helps to minimize __synchronization cost__, and maximize __independence__.

	1. __Faster__ feature development:
		- The scope of the work is __limited__ (it's easier to understand and work on smaller domains).
		- The releases are __independent__, so you don't have to wait for someone else.

	2. __Scalability__:
		- __Limited__ scope is easier to optimize.
		- __Independent__ scaling.
		- __Independent__ storage.

	3. __Flexibility__: 
		- Possible to use different (newer or more adequate) technologies or even languages at any point (but it is not recommended).
		- __Partial__ failures, strict error boundaries.

	#### Disadvantages:
	In case of __smaller__, __less complex__ systems building microservices could be unnecessary. New problems can arise from the complex 
	communication between the microservices, the extra services and tools become a must, and so on.
	
- ### Service-oriented architecture (SOA)
	- **Context**:
		It is similar to the [[Guiding principles#Microservice design|microservice architecture]], both offer are **distributed** designs, offering the advantages of decoupling. While SOA is more infrastructure heavy, microservices offer a more lightweight and flexible solution.
		
	The services communicate through a protocol over a network, RESTful technology uses this pattern. 
	
	A service in SOA:
	- Logically represents a business activity
	- Self-contained
	- Black box to its consumers
	
- ### What is the DAO (Data Access Object) pattern? When and how to implement?
	Link: https://www.baeldung.com/java-dao-pattern

	A structural pattern that allows us to __isolate__ the application/business layer from the persistence layer using an __abstract API__.
	The functionality of this API is to __hide__ from the application all the complexities involved in performing CRUD operations in the underlying storage mechanism.

	A simple DAO API:
	```java
	public interface Dao<T> {

		Optional<T> get(long id);

		List<T> getAll();

		void save(T t);

		void update(T t, String[] params);

		void delete(T t);
	}
	```

	It consist of following:
	- Data Access Object __Interface:__ This interface defines the standard operations to be performed on a model object(s).
	- Data Access Object __concrete class__: This class implements above interface. 
	This class is responsible to get data from a data source which can be database / xml or any other storage mechanism.
	- __Model Object:__ This object is simple POJO containing get/set methods to store data retrieved using DAO class.
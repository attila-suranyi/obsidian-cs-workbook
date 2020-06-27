# Object Oriented concepts

## Basic concepts

- ### What is an object oriented program?
	In object oriented programming, __importance is given to data__ rather than just instructions or functions to complete a task.
	This opposes the historical approach to programming where emphasis was placed on how the logic was written rather than how to define the data within the logic.

	An object is a thing or idea that you want to model in your program.
	An object can be defined as a data field that has unique attributes and behavior.

- ### What is a class?
	A class describes what the object will be, but is separate from the object itself. 
	In other words, classes can be described as __blueprints__, descriptions, or definitions for an object. 
	You can use the same class as a blueprint for creating multiple objects (it's called instantiation - the realization of a predefined object). 

- ### What is an object?
	An object is an instance of a class.
	Software objects are conceptually similar to real-world objects: they consist of **state** and **behavior**. 
	An object stores its state in fields (variables in some programming languages) and exposes its behavior through methods (functions in some programming languages). 
	Methods operate on an object's internal state and serve as the primary mechanism for object-to-object communication. 

- ### What is a constructor?
	Constructor is a block of code that initializes the newly created object. 
	A constructor resembles an instance method in Java but it's not a method as it doesn't have a return type.

- ### Instantiation, Attribute, Method
	- __Instantiation__: Creating an object from a class.

	- __Attribute__: A variable within a class and object. These are the properties of a "thing", describes how it is, what color, how heigh, etc.

	- __Method__: A function within a class and object. These are the verbs of a "thing", describes what it can do, jump, eat, calculate probability, etc.

- ### What are access modifiers?
	A Java access modifier specifies which classes can access a given class and its fields, constructors and methods. Access modifiers can be specified separately for a class, its constructors, fields and methods.
![[Access modifiers.png]]

- ### What is the default access modifier in a class?
	Also called _"package-private"_, the marked members can only be seen from inside its class and its package.

- ### What does the ‘static’ keyword mean?
	Static means that the variable or method marked as such is available at the class level. 
	In other words, you don't need to create an instance of the class to access it.

- ### Why is the main() method declared as static?
	For the most part it is only because convention:
	- The `static` keyword with "main" makes it clear to the JVM to run main first, so it doesn't have to decide which constructor to call.
	- The `static` keyword allows main to be called without having to instantiate a particular instance of the class. 
	This is necessary since main is called by the Java interpreter before any objects are made.

- ### Abstract classes and methods
	__Abstract classes__:
	- an _abstract_ class can contain both abstract and concrete methods as well,
	- It can contain fields that are `static`,` non-static`, `final`, `non-final`.
	- It can have class members like `private`, `protected`, etc.
	- it can have constructors and `static` methods as well,
	- it can have `final` methods which will force the subclass not to change the body of the method.

	__Abstract methods__:
	- it __must__ be implemented in the first concrete subclass,
	- it __must__ be in an abstract class,
	- it __can't__ be: `final`, `static`, `private`

- ### What is an interface?
	An interface is a __contract__, ensuring the __capabilities__ of a given class.  It's not about _how_ to do something, but _what_ to do.

	- methods can be: `abstract`, `static`, `default`
	- fields can only be: `static`, `final`.
	- only access modifier: `public`

- ### Interface vs Abstract class

	Class: __IS-A__, while an interface: __CAN__ relationship.

	We use an interface when:
	- we want to ensure the __functionalities__ of a class, to __standardize__ it,
	- There isn't a mutual superclass which could contain the properties or behavior. 
	Like the capability of flying. There are several animals which can fly, but they don't have a mutual superclass. 

- #### Interface:
	- It is about what an object __can do__: it is a __contract__.
	- The only fields that can appear in an interface must be declared both `static` and `final`.
	- Only `public` access modifier.
	- It supports __multiple inheritance__.
	- Only abstract methods? __NOPE__: since Java 8 it can contain __default methods__.

- #### Abstract class:
	- It is about what an object __is__.
	- It can contain state: fields that are `static`,` non-static`, `final`, `non-final`.
	- It can have class members like `private`, `protected`, etc.
	- It is mostly used to avoid duplication: the implementation in the abstract class is same in the derived classes.

- ### Interface default methods
	Link: https://www.baeldung.com/java-static-default-methods

	Since Java 8 interfaces can have `static` and `default` methods.

	- #### Why default methods are needed

		If we want the same implementation of a method in all the present and future classes, then using concrete, `default` methods are an efficient way to deal with this issue. 
		They __allow us to add new methods to an interface that are automatically available in the implementations__. 
		Thus, there's no need to modify the implementing classes.

		In this way, __backward compatibility__ is neatly preserved without having to refactor the implementers.

	- #### Multiple interface inheritance rules

		- Since Java allows classes to implement multiple interfaces, it's important to know what happens when a class implements several interfaces that define the same default methods. 
		In this case the __code won't compile__, as there's a conflict. The program doesn't know which method to be called. 
		- To solve this ambiguity, we must explicitly __provide an implementation__ for the methods.
		- We can also have our class use the default methods of one of the interfaces:

		```java
		@Override
		public String turnAlarmOn() {
			return Vehicle.super.turnAlarmOn();
		}
		```

- ### Can a static method use non-static members?
	Without specifing what non-static instance member to use, **NO**.

- ### How do you make a class immutable?
	Link: https://www.geeksforgeeks.org/create-immutable-class-java/

	Immutable class means that once an object is created, we cannot change its content. In Java, all the wrapper classes (like Integer, Boolean, Byte, Short) and String class is immutable. We can create our own immutable class as well.

	Following are the requirements:
	- The class must be declared as final (So it can't be extended)
	- Data members in the class must be declared as final (So that we can’t change the value of it after object creation)
	- Initialize all the fields via a constructor performing deep copy.
	- Getter method for all the variables in it
	- No setters (To not have the option to change the value of the instance variable)
	- Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.

- ### What is casting? What is the difference between up vs downcasting?
	Link: https://www.baeldung.com/java-type-casting

	Casting __primitives__ and __reference__ variables are _very different_:
	- **Primitive** variable contains its value, and narrowing (downcasting) conversion of a primitive variable means irreversible 
	changes in its value. E.g.: an int can only store 32 bits of data, so casting a 64 bits long to int means information loss.

	- The **reference** variable only refers to an object but doesn’t contain the object itself. Casting a reference variable doesn’t touch the object it refers to, but only labels this object in another way, expanding or narrowing opportunities to work with it. Upcasting narrows the list of methods and properties available to this object, and downcasting can extend it.

- ### Which order should we catch the exceptions? Why?
	Downcasting, because upcasting to a superclass is straightforward, every subclass has only one superclass in Java.
	But downcasting is more dangerous, because there can be multiple subclasses.

## Hiding, overriding, overloading
- ### Variable and method hiding
	Link: https://www.baeldung.com/java-variable-method-hiding

	- #### Variable hiding
		Variable hiding happens when we declare a property in a local scope that has the same name as the one we already have in the outer scope.
		- __Local__ variables hide outer scope variables.
		- Variable in __subclass__ hides the one in the superclass.

	- #### Method hiding
		In case of `static` methods: [[OOP#Hiding Static Methods]]

- ### Difference between overloading and overriding?
	Link: https://www.javatpoint.com/method-overloading-vs-method-overriding-in-java

	- #### Overloading 
		Overloading allows different methods to have the same name, but different signatures where the signature can differ by the number of **input parameters** or type of input parameters or both. Overloading is related to **compile time** (or static) polymorphism.

	- #### Overriding
		Overriding is a feature that allows a subclass or child class to provide a specific implementation of a method that is already provided by one of its super-classes or parent classes. When a method in a subclass has the same name, same parameters and same return type (or sub-type) as a method in its super-class, then the method in the subclass is said to override the method in the super-class.
		It is related to **runtime** polymorphism.
		For more differences see the table in the link.

- ### Difference between hiding a static method and overriding an instance method
	- #### Overriding Instance Methods
		An instance method in a subclass with the same signature and return type as an instance method in the superclass overrides the superclass's method.
		It is determined at __runtime__.  

	- #### Hiding Static Methods
		Static methods can not be overridden. If a subclass defines a static method with the same signature as a static method in the superclass, then the method in the subclass hides the one in the superclass.
		It is determined at __compile time__. 

	- #### Differences
		- Overridden Instance Methods: the method in the subclass __replaces__ the method in the superclass. 
		(Unless it is called from the subclass with super.myMethod())
		- Hidden Static methods: When you hide a static method, the hidden method only replaces the parent methods in the scope defined in the subclass. 
		It depends on whether it gets invoked from the superclass or the subclass.

- ### Java: @Override annotation
	The annotation is used to ensure us that we are indeed overriding a method instead of for example overloading it.
	The compiler will check the superclass, and throw an `error` if we are not overriding the method.

- ### Java: When you use method overriding, how can you change the access level of the method?
	Link: https://stackoverflow.com/questions/6851612/when-overriding-a-method-why-can-i-increase-access-but-not-decrease-it

	A sub-class can always widen the access modifier, because it is still a valid [[Guiding principles#Liskov Substitution principle|substitution]] for the super-class. Making protected/public things less visible would violate this idea; you could make child classes unusable as instances of the parent class.
	
- ### Java: Can the main method be overridden?
	No, because the main is a static method and a static method cannot be overridden.
	
- ### When you use method overriding, can you throw fewer exceptions in the subclass than in the parent class? Why?
	Yes.

	What matters isn't the number of these exceptions, but the relationship between them. 
	If the parent class' method throws an exception, e.g. `IOException`, its subclass overriding the method can throw subclasses of that exception, like `SocketException`.

	We cannot do this the other way around, though. 
	If the parent throws `IOException`, the overridden method cannot throw a broader exception than that, like `Exception`. 
	In that case, the method in the parent class would also need to throw `Exception`.

	This is because of __polymorphism__. 
	If we created a new instance of the subclass:

	```java
	Superclass instance = new Subclass();
	```
		
	and the subclass throws `SQLException`, then the compiler could not force us to catch it, because we are referring to this instance of the subclass by its superclass. 
	On the other hand, if `IOException` is handled, any subclass of it will be handled as well.

## Higher order concepts

- ### Why is it not a good practice to write a lot of static methods?
	The concept of `static` violates a few OO concepts.
	In OO, computation is performed by networks of self-contained objects which send messages to each other. Sending a message is the only way of communication / computation.
	Static methods don't do that. They aren't associated with any object. They __break encapsulation__.

	They also:
	- they prevent reusability as they cannot be overridden.
	- they remain in the memory for a long time, as long as the class it belongs to is. Using a lot of static methods occupy more memory.
	- Make multithreaded applications and testing really difficult, since it binds the program to a static part.

- ### What is data hiding?
	Using access modifiers to hide data from other layers or users of the application.
	Encapsulation is **NOT** only data hiding: https://stackoverflow.com/questions/12013448/encapsulation-vs-data-hiding-java

- ### Object Oriented Principles
	- #### Encapsulation 
		The implementation and state of each object are held inside a defined boundary, or class. 
		In general, the purpose of encapsulation is to __bundle similar items into a container__.
		Encapsulation is the way to accomplish __data hiding__.
		With data hiding we can reveal internal mechanisms that are relevant for the use of other objects, hiding any unnecessary implementation code. 
		This characteristic of data hiding provides greater program security and avoids unintended data corruption.     

	- #### Abstraction 
		Abstraction is a process of hiding the implementation details and showing only functionality to the user.
		It lets you focus on what the object does instead of how it does it.
		There are two ways to achieve abstraction in java:
		1.    Abstract class
		2.    Interface

	- #### Inheritance 
		Relationships and subclasses between objects can be assigned, allowing developers to **reuse** a common logic while still maintaining a unique hierarchy. 
		This property of OOP forces a more thorough data analysis, reduces development time and ensures a higher level of accuracy. 
		It is the mechanism in Java by which one class is allow to inherit the features(fields and methods) of another class.
		Inheritances expresses “is-a” relationship between two objects. 
		Using Inheritance, in derived classes we can reuse the code of existing super classes. 

	- #### Polymorphism 
		It means one name many forms. Objects are allowed to take on more than one form depending on the context. 
		The program will determine which meaning or usage is necessary for each execution of that object, cutting down on the need to duplicate code. 
		It has two types — static and dynamic. 
		**Static** polymorphism is achieved using method overloading and **dynamic** polymorphism using method overriding. 
		It is closely related to inheritance. 
		We can write a code that works on the superclass, and it will work with any subclass type as well.

- ### Polymorphism
	The 3 steps of object declaration and assignment:

	```java
	Dog myDog = new Dog();
	```

	1. First we __declare__ that there is a `myDog` variable, and the JVM should allocate memory for this reference variable.
	Here, the variable will be `Dog` type forever.
	2. We create a `Dog` object, and JVM should allocate memory for that as well.
	3. We assign (in this case initialize, since this is the first assignment) the `Dog` object to the reference.

	In this case, the reference type and the object type are the same.
	But with polymorphism...

	```java
	Animal myDog = new Dog();
	```
	... the reference type can be a superclass of the actual object.

- #### Types of polymorphism

	The __compiler__ only looks at the __reference__ type to decide whether you can call a method on that reference, but at __runtime__ the JVM looks at the actual object.

	- __Compile Time polymorphism__:
		- ...or __Static polymorphism__,
		- method overloading is an example of it,
		- Java knows which method to invoke by checking the method signatures.

	- __Runtime polymorphism__:
		- ...or __Dynamic polymorphism__,
		- a call to an overridden method is resolved,
		- In this process, an overridden method is called through the reference variable of a superclass: 

		```java
		class ABC{
		   public void myMethod(){
			System.out.println("Overridden Method");
		   }
		}
		public class XYZ extends ABC{

		   public void myMethod(){
			System.out.println("Overriding Method");
		   }
		   public static void main(String args[]){
			ABC obj = new XYZ();
			obj.myMethod();
		   }
		}
		Output: "Overriding Method"
		```
		- When an overridden method is called through a reference of parent class, then type of the object determines which method is to be executed.
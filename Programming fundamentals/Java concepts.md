# Java concepts

- ### What is autoboxing and unboxing?
	Autoboxing: Converting a primitive value into an object of the corresponding wrapper class is called autoboxing. For example, converting `int` to `Integer` class. 
	The Java compiler applies autoboxing when a primitive value is:
	- Passed as a parameter to a method that expects an object of the corresponding wrapper class.
	- Assigned to a variable of the corresponding wrapper class.

	Unboxing is the same just the opposite direction.

- ### What is the purpose of the ‘equals()’ method?
	It makes it possible the compare the fields of two objects.

- ### What is the difference between == and 'equals()'?
	Link: https://javarevisited.blogspot.com/2012/12/difference-between-equals-method-and-equality-operator-java.html

	We can use == operators for reference comparison (address comparison) and `.equals()` method can be __overriden__ for defining a condition on which two domain objects will be considered equal. 

	The __default implementation__ of equals provided in Object class is similar to == equality operator and return true if you are comparing two references to the same object.
	However, if `.equals()` is overriden, like for example in the case of Strings, the content is compared.

	In simple words, == checks if both objects point to the same memory location whereas _the overridden_ `.equals()` evaluates to the comparison of values in the objects.

	Some example:
	```java
	String string1 = "dog";
	String string2 = "dog";

	String string3 = string1;

	String string4 = new String("dog");

	// the two variable points to the same memory because of the string pool
	System.out.println(string1 == string2);

	// just as string3 and string1 reference the same memory place
	System.out.println(string1 == string3);

	// string4 is an object, so they have different memory addresses
	System.out.println(string1 == string4);

	// In case of Strings the .equals() method is overriden so it checks the content
	System.out.println(string1.equals(string4));


	// However, if you compare two objects that doesn't override the .equals() method,
	// then it does the same thing as the '==' operator

	Thread t1 = new Thread();
	Thread t2 = new Thread();

	// they can have the same content, but the memory address is different
	System.out.println(t1.equals(t2));
	```
	
- ### What is the connection between equals() and hashCode()? How are they used in HashMap?
	- Links: 
		- https://www.baeldung.com/java-equals-hashcode-contracts
		- https://crunchify.com/how-to-override-equals-and-hashcode-method-in-java/
		- https://stackoverflow.com/questions/2265503/why-do-i-need-to-override-the-equals-and-hashcode-methods-in-java

	- #### equals()
		The default implementation of `equals()` in the class `Object` uses the `==` operator, which compares memory addresses, so __identity__ will determine equality.
		When working with custom classes we often want to __overwrite__ this, so for example important fields will determine equality. 

	- #### hashCode()
		It is provided by `java.lang.Object` and returns an integer representation of the object memory address.
		The `hashCode()` method is closely related to `equals()`: 
		objects that are equal to each other must return the __same hashCode__.
		This criteria has a consequence: __if we overwrite `equals()` we must override `hashCode()` as well.__

	- #### HashMap Key With an Inconsistent hashCode()
		Let's see an example when __only__ the `equals()` has been overridden: 

		```java
		Map<Team,String> leaders = new HashMap<>();
		leaders.put(new Team("New York", "development"), "Anne");
		leaders.put(new Team("Boston", "development"), "Brian");

		Team myTeam = new Team("New York", "development");
		String myTeamLeader = leaders.get(myTeam);
		```
		We would expect myTeamLeader to return “Anne”. But with the current code, __it doesn't__.
		According to the overridden `equals()` the two `new Team("New York", "development")` are the same, since we specified that these fields "matter" to us in equality. But the `hashCode()` uses memory address, so we can't retrieve the value from the HashMap since the hashCodes of the two objects are different.

		This is all because we violated the above mentioned criteria: __Equal objects return the same hashCode.__
	
- ### Enums
	Link1: https://www.baeldung.com/a-guide-to-java-enums
	Link2: https://www.geeksforgeeks.org/enum-in-java/

	Enum is used to define `public`, `static`, `final` variables in a specific way, which makes our code more readable, allow compile-time checking and avoid unexpected behaviour due to invalid values being passed in.

	You can define __constructors, methods, and fields__ inside enum types that make it very powerful.

	If you create for example a ColorType.SPADES enum, it calls its constructor, and gives values to its fields (suitNumber -> 3, suitName -> “spades”). 
	This constructor must be private or default (package-private).

	Enum can contain getters as well. With them you can reach the values of the fields. 
	It is possible to create setters as well if the fields are not final (???). 
	It may not be a good idea, considering enums should be constants. 

	You can also create methods that make calculations based on the field values of the enum constant.
	
- ### What are “generics”? When to use?
	Using java generics programmers are able to write more general methods. 
	It means that it is not necessary to specify the input type of a method, therefore it can handle Strings, Integers, Doubles and so on. 
	It is very useful when for example we want to implement a sorting method. 
	If we use generics our method will handle more type of Lists.
	
- ### How can we initialize a final variable?
	1. When you declare it.
	2. Inside a constructor.
	3. Inside an instance-initializer block (IIB)
	
- ### What does "final" mean in case of a variable, method or a class?
	Link: https://www.geeksforgeeks.org/final-keyword-java/

	- A final variable’s value cannot be modified or if it is a reference to an object, you cannot refer to another object with it.
	- A final method cannot be overridden.
	- A final class cannot be extended.

- ### What is the benefit of having “generic” containers?
	Link: https://www.geeksforgeeks.org/non-generic-vs-generic-collection-in-java/

	__Code Reuse__: By using Generics, one needs to write a method/class/interface only once and use for any type. 
	Whereas in the non-generics, the code needs to be written again and again whenever needed.
	
- ### What happens if you try to delete/drop an item from an array, while you are iterating over it?
	The length of an array is **fixed** after creation, therefore it is not possible to remove any elements while iterating, or just picked by value or index. 

	However there is a method removeElement() in class ArrayUtils. 
	This creates a new array without the element we want to remove. 
	This works via iterating.
	
- ### What happens if you try to delete/drop/add an item from a List, while you are iterating over it?
	It will cause a `ConcurrentModificationException`, unless you are using an iterator and say iterator.remove(). 
	Essentially, the `ConcurrentModificationException` is used to fail-fast when something we are iterating on is modified. 
	
- ### What is the JVM?
	The __Java Virtual Machine__ is the "transformer" which makes java code platform independent, 
	known as the "write once, run everywhere" principle. The second main purpose of the JVM is to manage 
	and optimize program memory.
	![[JVM.png]]
	
- ### What is the difference between the JRE and the JDK?
	Link: https://stackoverflow.com/questions/1906445/what-is-the-difference-between-jdk-and-jre

	The JRE is the __Java Runtime Environment__. 
	It is a package of everything necessary to run a compiled Java program, including the Java Virtual Machine (JVM), 
	the Java Class Library, the java command, and other infrastructure. 
	However, it cannot be used to create new programs.

	The JDK is the __Java Development Kit__, the full-featured SDK for Java. 
	It has everything the JRE has, but also the compiler (javac) and tools (like javadoc and jdb). 
	It is capable of creating and compiling programs.

	__JDK__ = __JRE__ + __JVM__ + Java Class Library + other infrastructure
	![[jdk-jvm.png]]
	
- ### What is a garbage collector, in a nutshell?
	If we want to delete an object, we delete all reference to it, this way making it unreachable. But this process doesn't free the heap memory the object is stored on. Luckily, in Java, there is a program that always running in the background,
	checking if an object became unreachable, and if it is, the program frees the memory place. This program is called garbage collector.
	
- ### What is Error in Java and how does it relate to Exception?
	An Error indicates serious problems that a reasonable application should not try to catch.
	Errors are the conditions which cannot get recovered by any handling techniques. 
	It surely cause termination of the program abnormally. 
	Errors belong to __unchecked__ type and mostly occur at runtime. 
	Some of the examples of errors are `Out of memory error` or a `System crash error`.
	As the above image indicates, both the Error and the Exception class extends the Throwable superclass.
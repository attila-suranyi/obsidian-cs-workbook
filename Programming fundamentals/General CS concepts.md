# General CS concepts

- ### Iterator
	It is an object that enables us to **traverse** a container, and also to **access** the elements, but it does not perform the iteration itself. It is behaviorally similar to a *database cursor*.
	Internal iterators are *higher order functions* such as *map, filter, reduce*, because they implement the traversal, and applying the given function to every element.

- ### Generator
	One way to implement the iterator pattern. Instead of returning only once, the generator can *yield* values to its caller multiple times.
	In Python, a generator is an iterator constructor, it returns an iterator with the `yield` statement.
	
- ### Call stack
	The call stack helps the interpreter (like Python interpeter) to keep track of its current place or what function is currently running, and how did it get there.
	
	Just like in a stack structure, the function that is called pushed into the stack, the function starts to being executed, and if another function is called within the first function, that is pushed to the stack as well.
	If a function is finished, it is being poped from the top of the stack.
	
	#### Stack overflow
	If the call stack pointer exceeds the maximum size of the call stack, the **stack bound**, stack overflow occurs. It usually happens when an infinite loop is present.
	
- ### Function signature
	A function signature (or type signature, or method signature) defines input and output of functions or methods. 
	A signature can include:
	- parameters and their types
	- a return value and type
	- exceptions that might be thrown or passed back
	- information about the availability of the method in an object-oriented program (such as the keywords public, static, or prototype).

- ### Immutability
	**Link**: https://www.youtube.com/watch?v=5qQQ3yzbKp8
	>Immutable object can't be changed after it is created. 
	
	It doesn't mean that you can't **assign** a new value to an immutable object, but it won't override the original value, bit create a new one, with a different **memory address**.
	
	In Java Strings are immutable this is why StringBuffer is more efficient way to modify strings in Java.
	
	
	
	
	
	
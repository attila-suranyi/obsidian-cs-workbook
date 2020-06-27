# Functional programming
- ### Properties
	Pure function is **idempotent**:
	- no side effects
	- doesn't use global state
	- doesn't change the arguments (immutable)
	- result only depens on arguments

- ### Lambda
	**Link**: https://gist.github.com/ericelliott/414be9be82128443f6df
	
	>The most important, defining characteristic of a lambda expression is that it is used as **data**. That is, the function is passed as an argument to another function, returned as a value from a function, or assigned to variables or data structures. This is basically the definition of a first class function.

	Lambdas and anonym functions are often used interchangeably, like in lambda calculus. 
	
	In this Javascript example `myFunc` is a lambda, because it is passed as an argument to the `map` method, but not an anonym function.
  ```javascript
  const array = [1, 2, 3];
  const incremented = array.map(n => function myFunc(n) {return n + 1; });
  ```
  However, in Python you can't define an anonym function without it being lambda, but you can use a named function as lambda:
  
  ```python
  array = [1, 2, 3]
  incremented1 = map(lambda num: num + 1, array)
  incremented2 = map(increment, array)
  ```
  
 - ### Lazy evaluation
 	>Lazy evaluation, or call-by-need is an evaluation strategy which delays the evaluation of an expression until its value is needed and which also avoids repeated evaluations (sharing).
	
	For example, in Java intermediate stream operations won't be called without a terminal operation.
	
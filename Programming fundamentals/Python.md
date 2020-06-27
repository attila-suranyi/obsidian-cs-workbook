# Python

## Data structures
- ### Tuple
	```python
	tup1 = ('hey', 3, [1, 2, 3])
	```
	It is an **immutable** sequence, unlike the list, which is mutable, but both are **ordered**.
	They are used to represent *records*, data that belongs together.

- ### Set
	**Unordered** collections of unique elements. Because it is unordered, it does not support indexing and slicing.
	Set is implemented using dictionaries, thus the same applies for the set elements as for dictionary keys: it cannot contain mutable elements, such as lists or dictionaries. However, they can contain immutable elements such as [[Python#Tuple|tuples]].
	

## Computer Science
- ### Argument types in Python
	- **Default Argument**: there is no value provided for the argument in advance.
	- **Keyword Argument**: we provide a key-value pair when calling the function with the arguments, so order doesn't matter. In order to work, all keyword arguments has to match one of the arguments accepted by the function.
		```python
		def my_function(child3, child2, child1):
  			print("The youngest child is " + child3)
			
		my_function(child1 = "Emil", child2 = "Tobias", child3 = "Linus") 
		```
	- **Variable-length Argument (\*args, \*\*kwargs)**: if we don't know in advance how many arguments there will be, we can refer to them as \*args, or, if we want to use the keyworded version, \*\*kwargs.
		Kwargs works like a dictionary, with key and value.
		```python
		def arg_func(*argv):
			for arg in argv:
				print(arg)
				
		def kwarg_func(**kwargs):
			for key, value in kwargs.items(): 
        		print (f"The key is {key}, the value is {value}") 
  
		myFun(first ='Geeks', mid ='for', last='Geeks') 
			
		```
		
- ### What happens if you try to delete/drop/add an item from a List, while you are iterating over it in Python?
	It continues the iteration.
	
- ### Slicing
	With the slice object we can slice sequences like string, tuple, list, or anything else which supports sequence protocol. 
	```python
	my_array[start:stop] # the item at the stop index will be excluded
	my_array[start:] 	 # items start through the rest of the array
	my_array[:stop] 	 # items from the beginning, until the stop item
	my_array[:] 		 # copy of the whole array
	
	my_array[start:stop:step] # start through not past stop, by step
	
	# with negative numbers we count from the end of the list
	
	my_array[-1]    # last item in the array
	my_array[-2:]   # last two items in the array
	my_array[:-2]   # everything except the last two items
	
	my_array[::-1]  # all items reversed
	```
	
- ### List / set / dictionary comprehension vs generator expression
	The comprehension returns a collection, and the [[General CS concepts#Generator|generator]] returns an [[General CS concepts#Iterator|iterator]].
	If you have an infinite stream, it is more efficient to use a generator.
	```python
	# Generator expression -- returns iterator
	stripped_iter = (line.strip() for line in line_list)

	# List comprehension -- returns list
	stripped_list = [line.strip() for line in line_list]
	```

- ### Exception handling
	Excpetion occurs when syntactically **correct code** results an error. 
	```python
	try:
		print("Noob")
	except NameError:
		print("Exception occured")
	finally:
		print("Exception handled")
	```
	
	
	
	
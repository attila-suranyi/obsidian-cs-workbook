# Data structures, algorithms, and big O

## Data sctuctures
- ### What is a linked list? 
	It is a **traversable** data structure, meaning the elements can be visited in a predefined order. The elements, called **nodes** or links, 
	contain the data and a reference to the next node (and also to the previous node if it's a doubly linked list). Imagine it like a chain. 
	The first node in the list is the **head**.

- ### How to find if a linked list has a loop?
	The fastest method finding whether the linked list contains a loop or not can be done with the two pointers method.
	If the fast and slow pointers arrive at the same node the list contains a loop.
	
- ### How does HashMap work?
	**Links**:
	- https://www.youtube.com/watch?v=KyUTuwz_b7Q
	- https://medium.com/@dhruvamsharma/how-hashmap-works-a-missing-piece-of-hood-29dd28c4c01e

	The purpose of HashMap is mixing the powers of an ArrayList (the O(1) retrieval) and the Linked List (the dynamic addition and deletion of nodes).

	HashMap stores the data in the form of a **key-value pairs**, because it makes the retrieval of data easier.

	![[hashmap.png]]

	---------------------------------
    #### HashMap Workflow:
	1. A __hashcode__ is generated from the __key__.

	2. We want to store the data in an array, and __index__ it accordingly to the hash. All entries of keys having same hashcode are placed in the same bucket. Since the hash is a big integer, usually bigger than the length of the array we want to store the data in, a more fitting index is generated ("mapping": usually a simple modulo calculation: hash % array_size).
	The hash marks the bucket/array, and the shorter index generated from it marks the correct place in that bucket.

	3. The data is placed in the array according to the index. Since the index is calculated from the key, we dont need the check the whole array to find where the data is. Knowing what the key is we calculate the index, and the retrieval of the data is O(1) this way (ideally... -> collisions)!

	#### HashMap collision:
	- If the different data has the same index, a __linked list__ is placed at that index from the two (or more) collisioned data.
	This is called __chaining__, it is only one way of solving collisions (open addressing).

	---------------------------------

	The HashMap stores the object in the form of _Entry Class_. 
	Entry class is in the form of a linked list.
	An Entry class looks like this:

	```java 
	static class Entry<K,V> implements Map.Entry<K,V>
	{
	  final K key;
	  V value;
	  Entry<K,V> next;
	  final int hash;
	  ........
	}
	```

	Keys and values are stored in the Entry Object one by one... 
	...and each entry object will be a LinkedList Node.
	
- ### Why is it important for keys in a map to have an immutable type? (Consider String for example.)
	Immutability is required, in order to prevent changes on fields used to calculate the hashCode.

	If we overwrite the key the HashMap won't recalculate its hashCode and put it to the correct place, but will leave it there.
	We won't be able to retrieve it using the new key, because it is still sitting on the location which was calculated using the old key.
	It won't be reachable either using the old key, because the position it is pointing to is correct, but the key is different, so the `.equals()` will return false.

	![[hashmap immutable key.png]]

- ### Can a HashMap key be null?
	__Yes.__

	HashMap does not call `hashCode()` when `null` is passed as key and `null` Key is handled as special case.
	Null key is put into bucket 0 and maps `null` as key to passed value.
	Hence there can only be one `null` key in one hashMap object.

- ### What is the difference between Stack and Queue data structure?
	- Queue is a first-in-first-out (FIFO), and stack is a last-in-first-out (LIFO) data structure.
	- Insertion and deletion in stacks takes place only from __one end__ of the list called the top.
	- Insertion and deletion in queues takes place from the __opposite ends__ of the list. The insertion takes place at the rear of the list and the deletion takes place from the front of the list.
	- In stacks we maintain only __one pointer__ to access the list, called the top, which always points to the last element present in the list.
	- In queues we maintain __two pointers__ to access the list. The front pointer always points to the first element inserted in the list and is still present, and the rear pointer always points to the last inserted element.

- ### Graphs
	A graph is simply a collection of **nodes** with **edges** between (some of) them.

	A **simple graph** is an unweighted, undirected graph containing no graph loops or multiple edges. 
	A simple graph may be either connected or disconnected.

	![[graphs.png]]

	If arrows may be placed on one or both endpoints of the edges of a graph to indicate directedness, the graph is said to be directed.

	A weighted graph is a graph in which each branch is given a numerical weight.

- ### How can you store graphs in programs? What are the advantages/disadvantages per each?
	#### Adjacency List 
	Every node stores the adjacent nodes.

	```java
	class Node {
		public String label;
		public List<Node> adjacents;
	}
	```

	__Advantages:__
	- requires less memory than matrix (no redundant data)
	- adding new nodes and edges is easier
	- getting the adjacent nodes of a node in O(1) time

	__Disadvantages:__
	- getting whether there is an edge between two given nodes takes more time
	- removing a node or edge takes more time

	#### Adjacency Matrix
	A two-dimensional matrix, in which the rows represent source vertices and columns represent destination vertices.

	__Advantages:__
	- removing a node takes less time
	- getting whether there is an edge between two given nodes takes less time

	__Disadvantages:__
	- adding a node or edge takes more time
	- needs more memory because of all the redundant information 


## Algorithms
- ### Given an array of integers going from 1 to 100 (both inclusive) there is a duplicated entry. How to find it?
	- If the array is not sorted, then we have to traverse the whole array, so the time complexity of finding the duplicate is **O(n)**, using a HashMap. 
	- If it is sorted, then doing a **binary search** we compare the value and its the index. It's time complexity is **O(log n)**. If it is shifted, then the duplicate is on its left side, otherwise its on the right side. We continue the binary search on the side where the duplicates presence is proved.

	```java
	private static int getDuplicate(int[] sorted_arr) {
		int lower_limit = 0;
		int higher_limit = sorted_arr.length - 1;
		int mid;

		while (lower_limit <= higher_limit) {
			mid = (higher_limit + lower_limit) / 2;

			//if the value is at proper position, then the duplicate is at the right side
			if (sorted_arr[mid] == mid + 1) {

				//check the immediate neighbor to tell whether the mid is the duplicate
				if (sorted_arr[mid] == sorted_arr[mid + 1]) {
					return sorted_arr[mid];
				} else {
					lower_limit = mid + 1;
				}
			//duplicate is at the left side
			} else if (sorted_arr[mid] == mid) {
				if (sorted_arr[mid] == sorted_arr[mid - 1]) {
					return sorted_arr[mid];
				} else {
					higher_limit = mid - 1;
				}
			}
		}
		return -1;
	}
	```

## Big O complexity
- ### What is the Big O time complexity of the common operations in an ArrayList, LinkedList, HashMap? And of a bubble sort, quicksort, finding items in a Binary Search tree?
	Link: https://www.bigocheatsheet.com/

	#### ArrayList:
	- adding/removing from the beginning (or near the beginning): the whole list needs to be "re-indexed", so O(n)
	- adding/removing from the end (or near to the end): O(1)
	- get (by index): O(1)
	- contains: O(n)

	#### LinkedList:
	- adding/removing from the beginning or end: O(1)
	- adding/removing elsewhere (somewhere middle): O(n)
	- get: O(n)
	- contains: O(n)

	#### HashMap:
	Link: https://www.quora.com/What-is-the-Big-O-for-operations-in-a-Hashmap
	- every task takes a single operation: O(1) (except in edge cases, like hash clash).

	#### Bubble Sort:
	Link: https://www.studytonight.com/data-structures/bubble-sort
	- needs a nested for loop, so: O(n^2)

	#### Quicksort:
	Link: https://en.wikipedia.org/wiki/Quicksort
	- on average: O(n log n)
	- worst case: O(n^2)

	#### Binary Search Tree:
	- O(log n); (n log n != log n)
	- worst case (degenerate tree): O(n)
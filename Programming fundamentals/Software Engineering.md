# Software engineering

## Version control / Git
![[git stages.png]]
- ### Working directory
	This is where your files are, and they can be __tracked or untracked__. Here if you make changes and do not explicitly save them to git, you will lose the changes made to your files. Here you can work on code that you don't want to save yet.
	
- ### Staging area
	This is where git starts tracking and saving changes. You collect the changes here you will commit to the repository. If you don't save the changes, you will lose them.
	
- ### Repository
	This is where Git stores the snapshots of your code, the saved changes of your commits. Here they are safely stored in your local database. 
	
- ### Tracked and untracked files
	Tracked files are files the Git knows about, they were in the last snapshot.
	
- ### Merge conflict
	A merge conflict happens when two branches both modify the same region of a file and are subsequently merged. Git can't know which of the changes to keep, and thus needs human intervention to resolve the conflict.
	
- ### Through what series of commands could you put a new file into a remote repository connected to your existing local repository?
	1. Adding it to the _Staging area_, thus making it _tracked_:
		```add new_file```

	2. Commiting it to the local git repository:
		```commit new_file```

	1. Pushing it to the remote repository on a specific branch:
    	```push new_file origin/branch```
		
- ### Atomic commits
	Atomic commits mean that the commit code should be a small, focused, working unit.
	
- ### git vs GitHub
	Git is a VCS, while GitHub is a hosting service for Git repositories.
	
## Testing
- ### Test case vs assertion
	A **test case** is basically what we call a test in everyday language: it is a set of **conditions** under which the tester decides if the reaction of the subject is satisfactory. A simple example: test passes **if** the application saved a message correctly.
	
	A **test assertion** is part of a test case, it is an expression which encapsulates some testable logic.
	
	Example:
	```java
	class Test {

		Service service = new Service();

		@Test
		void itemAffordable() {
			User user1 = User.builder()
				.id(1L)
				.balance(1.000.000)
				.build();

			Item item = Item.builder()
				.id(1L)
				.price(500)
				.buyer(user1)

			assertTrue(service.buy(item1));  //<-- Only this line is the assertion.
		}
	}
	```
	
- ### Types of testing
	- #### Unit testing 
		The modules of the application (whatever you decide a unit is, like a class, method, etc) works well in **isolation**, or without any interaction with dependencies.
	- #### Integration testing 
		When putting together several units of the application that interacts, you test that the integration of these units didn't introduce any new errors.
	- #### Regression testing
		After the integrating (and maybe fixing), running the unit tests again is advised. This ensures that fixing the integration didn't break the unit tests.
	- #### Acceptance testing
		When a user/customer/business tests a **functionality** to ensure that the functionality meets their requirements.
	- ### Test coverage
		It is a measurement quantifying the ratio of how much code is executed when tests are running. This ratio can be compared to lines of code, methods, classes, etc.
	- ### Mocking
		Simulating the behavior or reaction of a dependency. This way we can isolate a unit from its dependencies.
		
		It can be done manually using polymorphism. For example, you can substitute a class with its subclass, where you override parts to result the desired behaviour.
	- ### TDD
		![[TDD.png]]
		Test-driven-development
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

			assertTrue(service.buy(item1));  
			//Only this line is the assertion.
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
		Test-driven-development is a software development technique that heavily relies on tests, and using a very shortdevelopment cycle: requirements are turned into very specific test cases, the software is improved so that the tests pass, then the code is revised and refactored.
		This is opposed to software development that allows software to be added that is not proven to meet requirements.
		
		Some of the __benefits__:
		 - Writing the tests first requires you to really consider what do you want from the code.
		 - You receive fast feedback.
		 - TDD creates a detailed specification. 
		 - You're forced to write small classes focused on one thing.

	- ### Unit testing best practices
		- **Isolated**: The tested unit if isolated from dependencies, like databases, or other classes. This way we can narrow down the tested subject, and tell more accurately where the problem lies.
			Examples for isolating units: mocking dependencies, or initializing dependencies without the IoC container (if a DI framework is used).
		- **Arrange, Act, Assert**: an advised pattern: arrange your objects, act on them, then assert their behaviour.
		- **Write minimally passing tests**: The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.
			This way tests become more resilient to future changes in the codebase.
		- **Minimize logic in tests**: Less chance to introduce a bug.

## DevOps
- ### What is DevOps?
	__Development and Operations__.
	Typical tasks of a DevOps person is everything IT related except actually writing the software. 
	In practice this means the following:

	- Build systems that enable CI/CD workflows.
	- Manage the "cloud", set up its infrastructure, security, install and configure apps.
	- Make sure that there are monitoring and alerting systems in place in case of issues.
	- Automate everything: deployments, releases, upgrades.
	
- ### Continuous integration
	It means merging the changes back to the main branch as often as possible. The developer's changes are validated by __automated tests__.
	Using CI you avoid the integration hell that usually happens when people wait for release day to merge their changes into the release branch.
	This can be achieved using Jenkins, or Gitlab CI for example.
	![[devops techniques.png]]
	
- ### Continuous delivery
	Continuous integration + releasing new changes quickly. Release is automated, but deploy is still manual.
	
- ### Continuous deployment
	One step further, even the deployment is automated.
	
## Software Methodologies
- ### Software-lifecycle models
	Agile, Waterfall.
	
- ### UML diagram, types
	UML is a way of visualizing a software program using a collection of diagrams. 

	Structural UML diagrams:
	- Class diagram
	- Package diagram
	- Object diagram

	Behavioral UML diagrams:
	- Communication diagram
	- Interaction overview diagram

- ### Design pattern examples
	- [[Guiding principles#What is Dependency Injection|Dependency Injection]]
	- [[Guiding principles#What is the DAO Data Access Object pattern When and how to implement|Data access object]]
	- [[General CS concepts#Iterator|Iterator pattern]]
	- [[Observer design pattern]]
	- [[Publisher-Subscriber design pattern]]
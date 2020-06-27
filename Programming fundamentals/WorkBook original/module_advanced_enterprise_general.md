# Software engineering

## Testing
### What is TDD? What are the benefits?
![alt text](https://www.startpage.com/av/proxy-image?piurl=https%3A%2F%2Fmarsner.com%2Fwp-content%2Fuploads%2Ftest-driven-development-TDD.png&sp=1589381905T59632e6099ada75f37aa68ad838af97c6fac3294daea74d3b8ddd05e4e0daa73)
Test-driven development (TDD) is a software development process that relies on the repetition of a very short development cycle: 
requirements are turned into very specific test cases, then the software is improved so that the tests pass. 
This is opposed to software development that allows software to be added that is not proven to meet requirements.

Some of the __benefits__:
 - Writing the tests first requires you to really consider what do you want from the code.
 - You receive fast feedback.
 - TDD creates a detailed specification. 
 - You're forced to write small classes focused on one thing.

### What are the unit testing best practices? (Eg. how many assertion should a test case contain?)
- __Isolated__: Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as a file system or database.
- __Naming your tests__: The name of your test should consist of three parts:
    - The name of the method being tested.
    - The scenario under which it's being tested.
    - The expected behavior when the scenario is invoked.
- __Arrange, Act, Assert__: it is a common pattern when unit testing. As the name implies, it consists of three main actions:
    - Arrange your objects, creating and setting them up as necessary.
    - Act on an object.
    - Assert that something is as expected.
- __Write minimally passing tests__: The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.
This way tests become more resilient to future changes in the codebase.
- __Avoid logic in tests__: When writing your unit tests avoid manual string concatenation and logical conditions such as if, while, for, switch, etc.
Less chance to introduce a bug inside of your tests.

## DevOps

### What is continuous integration? Why is CI important?
- https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment
![alt text](https://wac-cdn.atlassian.com/dam/jcr:b2a6d1a7-1a60-4c77-aa30-f3eb675d6ad6/ci%20cd%20asset%20updates%20.007.png?cdnVersion=712)

Developers practicing continuous integration merge their changes back to the main branch as often as possible.
The developer's changes are validated by __automated tests__.

Using CI you avoid the integration hell that usually happens when people wait for 
release day to merge their changes into the release branch.

### Why are tests important in the CI workflow?
With developers merging to the main branch several times a day, the risk of __production bugs__ is high.
This can be only avoided with all kinds of tests and automation.

### Name some software that help the CI workflow!
Jenkins, Gitlab CI.

### What is Continuous Delivery?
Continuous delivery is an extension of continuous integration to make sure that you can release new changes to your 
customers quickly in a sustainable way. 
This means that on top of having automated your testing, you also have automated your release process and you can deploy 
your application at any point of time by clicking on a button.

### What is Continuous Deployment?
Continuous deployment goes one step further than continuous delivery. With this practice, every change that 
passes all stages of your production pipeline is released to your customers. 
There's no human intervention, and only a failed test will prevent a new change to be deployed to production.

### What is DevOps?
__Development and Operations__.
Typical tasks of a DevOps person is everything IT related except actually writing the software. 
In practice this means the following:

- Build systems that enable CI/CD workflows
- Manage the "cloud", set up its infrastructure, security, install and configure apps
- Make sure that there are monitoring and alerting systems in place in case of issues
- Automate everything: deployments, releases, upgrades.

## Software Methodologies
### What kind of software-lifecycle models do you know?
- Waterfall
- Agile

### What is a UML diagram? What kind of diagram types do you know?
UML is a way of visualizing a software program using a collection of diagrams. 

Structural UML diagrams:
- Class diagram
- Package diagram
- Object diagram

Behavioral UML diagrams:
- Communication diagram
- Interaction overview diagram

### What is a UML class diagram? What are the typical elements?
It describes the static structure of a system consisting of classes.

Elements:
- Fields of a class
- Visibility modifiers of a member
- Relationships 

### What kind of design patterns do you know? Bring at least 3 examples.
- Singleton design pattern
- Dependency Injection
- Separation of Concern
- DAO
- Lazy initialization

### What is the purpose of the Iterator Pattern?
To decouple algorithm from containers. 

### How would you separate data storage code and business logic code (which uses stored data) in an application?
Using the DAO pattern, which separates the two layer with an abstract API.

# Computer science

## Data Structures

### What are trees? What are binary trees? What are binary search trees?
Trees are special kind of graphs with the following properties:

- They don't have cycles (= a path which starts and and ends at the same node)
- They are connected (= there is a path from each node to each node)

![alt text](https://learn.code.cool/media/algorithms/tree.png)

- Each tree has a root node.
- The root node has zero or more child nodes.
- Each child node has zero or more child nodes, and so on.
- The node which doesn't have any children called a _leaf_.

__Binary Tree__: It is a tree in which each node has __maximum two children__.

__Binary Search Tree__: In this binary tree the nodes are __ordered__ according to their property:
ALL left descendants <= node < ALL right descendants.

![alt text](https://learn.code.cool/media/algorithms/binary-search-trees.png)

- Storing data in a BST has the advantage of receiving items in __O log(n)__ time, but adding and removing them slower
compared to arrays.
    

### What are graph traversal algorithms? What is BFS, how does it work? What is DFS, how does it work?
DFS: https://www.programiz.com/dsa/graph-dfs

__Depth-first search__: The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) 
and explores as far as possible along each branch before backtracking.

    Set visitedNodes;
    Stack stack;
    
    stack.add(initial node);
    
    while stack has nodes in it:
        put the top of the stack to visitedNodes;
        if the adjacent nodes isn't in visitedNotes:
            put the adjacent nodes to the stack;
            
__Breadth-first search__: It explores all of the neighbor nodes at the present depth prior to moving on to the nodes at the next depth level.

    Set visitedNodes;
    Queue queue;
    
    queue.add(initial node);
    
    while queue has nodes in it:
        put the end of the queue to visitedNodes;
        if the adjacent nodes isn't in visitedNotes:
            put the adjacent nodes to the start of the queue;

### How does dictionary work?
Like a HashMap.

## Algorithms
### What is QuickSort? Describe the main logic of this sorting algorithm.
QuickSort is a _"divide and conquer"_ sorting algorithm.

1. Choose an element randomly from the array, called the _pivot_ element.
2. Start two pointers from either side of the array.
3. Compare the value of the elements the pointers point at to the pivot:
    - If the __left__ element is bigger or equal to the pivot element, stop the pointer at that element,
    if it is smaller, move it to the right, and compare that element as well.
    - Same with the __right__ element, only we stop the right pointer at an element if it is bigger or equal to the pivot.
4. If both pointers stopped (and they didnt reach each other), we swap the elements they point at.
5. Repeat this until the pointers reach other.
6. Partitioning the array where the left pointer stopped, we repeat this progress on the parts until 
we cant divide them further.

# Software design

## Security

### What is OAuth2?
- https://www.youtube.com/watch?v=t4-416mg6iU
- https://www.youtube.com/watch?v=CPbvxxslDTU

__The problem__:

Think of when you want to login into LinkedIn with your Google account.
The two services don't trust eachother, and the user can't simply give his Google password to LinkedIn. 
The user doesn't want to give access to its whole account.
Google need to authorize LinkedIn, and give it __limited__ access to the users account. 

__The solution__: The OAuth Flow

1. User want to login to LinkedIn using his Google account.
2. LinkedIn sends request to Google for the user account details. 
3. Google notifies user about this, and asks user whether he gives __limited__ access to his Google account.
4. If user gives access, then Google gives LinkedIn an __access token__ (JWT token).
5. Now LinkedIn can use this token to gain limited access to the users account.

![alt text](https://www.researchgate.net/profile/Krishna_Shingala/publication/331587509/figure/fig1/AS:734025253650432@1552016666040/Use-of-JWT-as-access-tokens-in-OAuth.ppm)

OAuth is __authorization between services__.

OAuth 2 is an authorization protocol/framework that enables applications to obtain limited access to user accounts on an HTTP service, 
such as Facebook, GitHub, and DigitalOcean. 
It works by delegating user authentication to the service that hosts the user account, and authorizing third-party applications to access the user account. 
OAuth 2 provides authorization flows for web and desktop applications, and mobile devices.

A browser or mobile/desktop client makes a request to the authentication server containing user login information. 
The authentication server generates a new __access token__ and returns it to the client. 
The client stores this token (as a cookie/in a file/in LocalStorage/..) and sends it on every request in the HTTP header (Authorization field) to the server(s).

### What is Basic Authentication?
It is a method for an HTTP client (e.g. a web browser) to provide a user name and password when making a request. 
In basic HTTP authentication, a request contains a header field in the form of 
    
    Authorization: Basic <credentials>
    
where the credentials contain the user id and password.

In the case of a "Basic" authentication, the exchange must happen over an HTTPS (TLS) connection to be secure.

### What is CORS, why it’s needed in browsers?
Cross-Origin Resource Sharing  is a mechanism that uses HTTP headers to tell a browser to let a web application running at one origin (domain) 
have permission to access selected resources (=API endpoints) from a server at a different origin.

It is needed, because nowadays you run your frontend app and backend services on different machines (hosts/domains).

### How can you initialize a CSRF attack?
Cross-Site-Request-Forgery  is an attack that tricks an end user to execute unwanted actions on a web application in which they're currently authenticated.

It can be achieved via social engineering, like sending a link to the user tricking him into executing actions of the attacker's choosing.

![alt text](https://www.imperva.com/learn/wp-content/uploads/sites/13/2019/01/csrf-cross-site-request-forgery.png)

### What is JWT used for? Where to store it on client side?
- https://www.youtube.com/watch?v=_XbXkVdoG_0
- https://jcbaey.com/authentication-in-spa-reactjs-and-vuejs-the-right-way

#### JWT
- JSON Web Token (JWT) is an open standard that defines a compact and __self-contained__ way for securely transmitting information between parties as a JSON object. 
This information can be verified and trusted because it is digitally signed.

- __Structure:__ The content of the _header_ and the _payload_ is "visible", a simple encoding shows their value. 
But to decrypt the _signature_ a password is needed, which the server knows. 
You can't simply copy the signature of a token then change the content of the payload, because the signature depends
on the payload, and changes if the payload is changed. 
This way from the signature the server knows if the payload has been tampered with.
   
![alt text](https://learn.code.cool/media/web-security/jwt_structure.png)

- JWT can store any type of data, which is where it excels in combination with OAuth.

#### Why use JWT Authorization

Because __HTTP is stateless__, in order to associate a request to any other request, you need a way to store user data between HTTP requests.

__Session tokens__ are widely used for this purpose: the server stores all the necessary information about the user, 
and it gives him a session token with an ID, so every time a user sends a request with the ID, the server looks up the ID with all the necessary data. 
This token is a __reference token__.

However, with the rise of microservices this method became difficult, because multiple services need to access the database
where the details are stored about the user.

The JWT authorization solves this problem: all the necessary data (usually user ID, access rights, email...) is safely stored
in the token and signed by the server, so the server only need to validate the signature, and don't need to look up anything. 
This is why it is called a __value token__.

#### How to use JWT Authorization

__Sending the token:__

- __Bearer Token__: it goes into the Authorization header of any HTTP request:
    
   - not stored automatically
   - not sent automatically with every request
   - no expiry date
   - no associated domain
   
- __Authorization Cookie:__ this is better for sending, also a storage method, see below

__Storing the token:__
- __localStorage:__ 
    - JS code can access it
    - remains after the user closes the browser

- __Authorization Cookie:__
    - automatically stored in the browser
    - automatically sent with every request
    - expiry date
    - associated domain
    - HTTP only: JS cannot read it -> secured from XSS attacks
    - Secure: HTTPS

## Threaded programming

### When do you need to use threads in an application?
### What is a daemon thread?
### What is the difference between concurrent and parallel execution of code?
### What is the most important problem developers are faced when using threads?
### In what kind of situations can deadlocks occur?
### What are possible ways to prevent deadlocks from occurring?
### What does critical section or critical region mean in the context of concurrent programming?

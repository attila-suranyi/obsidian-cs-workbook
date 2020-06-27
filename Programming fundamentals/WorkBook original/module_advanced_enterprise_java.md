# Enterprise module (Java branch)

### Java Enterprise and Spring

#### What are the possible uses of reflection?
Reflection is an API which is used to examine or modify the behavior of methods, classes, interfaces at runtime.
- `instanceOf`
- call/invoke methods by name at runtime
- write code that maps arbitrary JSONs to Java objects (which is what Jackson or Gson is doing)
- unit testing frameworks

#### What is Inversion of Control (IoC)?
The process in which an object defines its dependencies without creating them. 
This object delegates the job of constructing such dependencies to an IoC container.

#### What is Spring?
https://www.youtube.com/watch?v=gq4S-ovWVlM

The most popular _framework_ for enterprise Java (more popular than the official Java Enterprise Edition / Java EE ).

__It is an IoC container__:

A typical problem an enterprise application has to face is the need to share __single__ instances of objects, like a service.
Spring manages the instantiation/lifecycle and dependencies of these object with the __Application Context__. Managing the dependencies
is done with __dependency injection__.
  
#### What is Spring Boot?
- _Convention-over-configuration_ addition to Spring. 
- It contains a lot of modules which help you up and running ASAP.

Spring vs Spring Boot:
If Spring is a pool which contains and manages the objects, then Spring Boot is a strand,
with multiple pools and other structures (security, JPA, etc.).

#### What is the major difference between the Standard edition (JSE) and Enterprise edition (JEE)? You can choose Spring (Spring Boot) instead of JavaEE. Focus on comparing them.
- __Java SE__ API provides the __core functionality__ of the Java programming language. 
It defines everything from the basic types and objects of the Java programming language to high-level classes that 
are used for networking, security, database access, graphical user interface (GUI) development, and XML parsing.

- The __Java EE__ platform is built __on top of__ the Java SE platform. 
The Java EE platform provides an API and runtime environment for developing and running large-scale, 
multi-tiered, scalable, reliable, and secure network applications.

#### What are the advantages of the Spring Framework? Focus on the Core part.
- It gives good support for __IoC and Dependency Injection__ results in loose coupling.
- It is __modular__. It is designed in such a way that no module is dependent to other module , except Spring core module
- __Versatile__: Spring is designed to be used with all other frameworks of Java, you can use ORM, Struts, Hibernate and other frameworks of Java together.

#### What is Spring MVC?
https://www.javatpoint.com/spring-mvc-tutorial

Spring MVC __maps requests to responses__.
- it is a Java framework
- it uses the __Model - View - Controller__ design pattern
- using the DispatchServlet class

The MVC design pattern:

![alt text](https://static.javatpoint.com/sppages/images/spring-web-model-view-controller.png)

- __Model__: A model contains the data of the application. A data can be a single object or a collection of objects.
- __Controller__: A controller contains the business logic of an application. Here, the @Controller annotation is used to mark the class as the controller.
- __View__: A view represents the provided information in a particular format. Usually a template of the page that is filled with data from the model.
- __Front Controller__: In Spring Web MVC, the DispatcherServlet class works as the front controller. It is responsible to manage the flow of the Spring MVC application.

#### What is a servlet? What is the purpose of DispatcherServlet in Spring?
A Servlet is a class that handles requests, processes them and reply back with a response.
It is a technology which is used to create a web application.

__DispatcherServlet__: responsible for directing incoming HttpRequests to all of an application's other controllers and handlers.

#### When do you use RestControllers, when just simple Controllers?
In case of creating a RESTFUL API, using RestController is advised.
If you want to return a __template__, then you should you a simple Controller.

#### What is Spring Application Context?
The __IoC container__ in Spring is represented by the Application Context interface.
It is responsible for instantiating, configuring and assembling objects, the lifecycle of these objects (beans).
It manages possible reuses and pooling, since __instantiating a new object is expensive__.

#### Why is Field injection not recommended?
Link: https://blog.marcnuri.com/field-injection-is-not-recommended/
- It doesn't allow **immutable or final** fields to be injected, because these fields need to be instantiated at class instantiation. Only constructor-based injection can solve this problem.
- The whole point of dependency injection is decoupling. With field injection these fields can only be injected by the Spring container, so we tightly couple again. This way the class is useless outside a Spring container, so if you want to unit test it, you are forced to use the application context.

#### What is a Spring Bean?
In Spring, the objects that form the backbone of your application and that are managed by the Spring IoC container are called beans. 
A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container.

#### What are the main ways to define a bean in the Application Context?
There are three different ways in which you can define a Spring bean:
- annotating your class with the stereotype __@Component__ annotation (or its derivatives)
- writing a bean factory method annotated with the __@Bean__ annotation in a custom Java configuration class
- declaring a bean definition in an XML configuration file

#### Spring Bean Scopes
https://www.baeldung.com/spring-bean-scopes

The scope of a bean defines the life cycle and visibility of that bean in the contexts in which it is used.

__Singleton Scope:__
Defining a bean with singleton scope means the container creates a single instance of that bean, and all requests for that bean name will return the same object, which is cached. 
Any modifications to the object will be reflected in all references to the bean. 
This scope is the default value if no other scope is specified.

__Prototype Scope:__
A bean with prototype scope will return a different instance every time it is requested from the container.

#### What is Spring RestTemplate?
https://www.baeldung.com/rest-template

It is the Spring REST Client which can be used for handling REST requests and reponses:

GET Plain JSON:
```java
    RestTemplate restTemplate = new RestTemplate();
    String fooResourceUrl = "http://localhost:8080/spring-rest/foos";
    ResponseEntity<String> response
      = restTemplate.getForEntity(fooResourceUrl + "/1", String.class);
      
#GET POJO:

    Foo foo = restTemplate.getForObject(fooResourceUrl + "/1", Foo.class);
    
#POST request with the _exchange_ API:

    RestTemplate restTemplate = new RestTemplate();
    Cryptocurrency cryptoCurr = restTemplate.exchange(
            apiEndpoint,
            HttpMethod.GET,
            new HttpEntity<>("parameters", this.buildHeaderWithAPIKey()),
            CryptoCurrency.class
    ).getBody();
```

!WebClient -> async: https://www.baeldung.com/spring-webclient-resttemplate

#### Difference between .jar and .war files.
Both are zipped files using java jar tool, but for different purposes:
- __.jar__: it contains libraries, resources and accessories files like property files.
- __.war__: WAR stands for Web Application Resource. It is used to package web applications 
that we can deploy on any Servlet/JSP container.

#### What are the major differences between Maven, Ant and Gradle?
- https://www.baeldung.com/ant-maven-gradle

They are all build automation tools:
- __Ant__: The main benefit of Ant is its __flexibility__. 
Ant doesn't impose any coding __conventions__ or project structures. 
Consequently, this means that Ant requires developers to write all the commands by themselves, 
which sometimes leads to huge XML build files which are hard to maintain or understand.
- __Maven__: Maven continues to use XML files just like Ant but in a much more __manageable__ way. 
The name of the game here is __convention over configuration__.
While Ant gives the flexibility and requires everything to be written from scratch, 
Maven relies on conventions and provides __predefined commands__ (goals). 
Maven also prescribes __strict__ project structure, while Ant provides flexibility there as well.
- __Gradle__: it's not using XML files, unlike Ant or Maven, but a __domain specific language__.

#### What is Maven used for?
It is a build automation and dependency management tool.

#### What does a pom.xml file contains in Maven?
It is an XML file that contains information about the project and configuration details used by Maven to build the project. 
It contains default values for most projects, for example the build directory, the test source directory, and so on.

### Object Relational Mapping, JPA

#### What is an ORM? What are the benefits, when to use?

![alt text](https://s14-eu5.startpage.com/cgi-bin/serveimage?url=https%3A%2F%2Fimg.scoop.it%2Fc2qqf-9VCVpyWfAs3raQDzl72eJkfbmt4t8yenImKBVvK0kTmF0xjctABnaLJIm9&sp=7df9e6e7d58829f7eb411346341da989&anticache=852559)

Object Relational Mapping is a technique converting data between incompatible type systems 
(e.g. a __relational database__) using object-oriented programming languages.

__Benefits__:
- __DRY__: Removes repeating code. This is especially a case when you have lots of business entities.
- __Security__: Not passing anything directly to query execution code greatly reduces the chances of messing with SQL injections.
- __Testability__:  With ORM I can quickly create a database for a test run with just a few lines of code. 
- __Deployment__: Pushing the app that can roll out its own database schema from its own code is a modern approach when everything including infrastructure should be a code.

#### What is the difference between JDBC and JPA? Which are the advantages and disadvantages of each? Give a general overview.
https://stackoverflow.com/questions/11881548/jpa-or-jdbc-how-are-they-different

- __Java DataBase Connectivity__ (JDBC) is a standard for Database Access
- __Java Persistence API__ (JPA) is a standard for ORM

Main difference between JPA and JDBC is level of abstraction.

__JDBC__ is a standard for connecting to a DB directly and running SQL against it - e.g `SELECT * FROM USERS`, etc.
Data sets can be returned which you can handle in your app, and you can do all the usual things like 
`INSERT`, `DELETE`, run stored procedures, etc. 
It is one of the underlying technologies behind most Java database access (including JPA providers).

One of the issues with traditional JDBC apps is that it can result _complicated code_ where 
lots of mapping between data sets and objects occur, _logic is mixed in with SQL_, etc.

__JPA__ is a standard for Object Relational Mapping. 
This is a technology which allows you to map between objects in code and database tables. 
This can "hide" the SQL from the developer so that all they deal with are Java classes, and the provider allows you to 
save them and load them magically. 
Mostly, XML mapping files or annotations on getters and setters can be used to tell the JPA provider 
which fields on your object map to which fields in the DB. 
Under the hood, Hibernate and most other providers for JPA write SQL and use JDBC to read and write from and to the DB.

__JDBC__:
- developer must do a lot of things manually, like: query optimization and ORM
- scaling is difficult

__JPA__:
- database independent

#### What is Hibernate? What are the advantages, limitations?
- https://www.baeldung.com/jpa-hibernate-difference
- https://www.roseindia.net/hibernate/examples/hibernate-advantages-and-disadvantages.html

The Java Persistence API (JPA)  is a specification (__a contract__) that defines the management of relational data in a Java application. 
The API maps out a set of concepts that defines __which__ objects within the application should be persisted, and __how__ it should persist them:
- @Entity defines which objects should be persisted
- Another core concept of JPA is field persistence
- JPA specifies how we should manage relationships between different database tables (@OneToOne, @OneToMany...)
- The EntityManager contains common Create, Read, Update and Delete (CRUD) operations

JPA is only a specification and that it needs an implementation to work. 

__Hibernate is an implementation of JPA.__

__Advantages__:
- supports Inheritance, Associations, Collections
- has its own query language, i.e hibernate query language which is _database independent_
- _supports annotations_, apart from XML

__Disadvantages__:
- _Lots of API to learn_: A lot of effort is required to learn Hibernate. So, not very easy to learn hibernate easily.
- _Debugging_: Sometimes debugging and performance tuning becomes difficult.
- _Slower_ than JDBC: Hibernate is slower than pure JDBC as it is generating lots of SQL statements in runtime.

#### Name 3 different annotations used in JPA, what can they do for you?
- __@Entity__: a "plain old Java class" (POJO) decorated with this annotation can be used as a
JPA entity and use JPA services with it, like saving.

- __@OneToMany__: defining one-to-many relationships. 
Set the _mappedBy_ attribute on the inverse (non-owning) side of the association to the name of 
the field or property that owns the relationship. Relations have to be defined at both ends!
_Cascade_ properties can be also defined here.

- __@Id__: the field marked with this annotation will be the entities primary key.

#### What is object-relational impedance mismatch?
https://en.wikipedia.org/wiki/Object-relational_impedance_mismatch
https://hibernate.org/orm/what-is-an-orm/

It is a set of conceptual and technical difficulties that are often encountered when a relational database management system (RDBMS) 
is being served by an application program (or multiple application programs) written in an object-oriented programming language or style, 
particularly because objects or class definitions must be mapped to database tables defined by a relational schema. 

Some examples:
- __Different data types__:  The relational model strictly prohibits by-reference attributes (or pointers), 
whereas OO languages embrace and expect by-reference behavior.

- __Inheritance__ is a natural paradigm in object-oriented programming languages. 
However, RDBMSs do not define anything similar on the whole.

- __Associations__ are represented as unidirectional references in Object Oriented languages whereas RDBMSs use the notion of foreign keys. 
If you need bidirectional relationships in Java, you must define the association twice. (@OneToOne at both sides)

#### What is a JpaRepository? What are the 2 main methods to define queries in them?
!!!

JpaRepository is an _interface_.

By extending it we get a bunch of generic CRUD methods we can use, like `findBy..` or `deleteBy..`.

We can also define our own queries using the `@Query` annotation. 

#### Why is the Set preferred over List when we want to store OneToMany relations?
We can prevent duplicating relations this way.

#### What kind of inheritance strategies are available? Which annotations are used to solve this?
- https://www.baeldung.com/hibernate-inheritance

There are four strategies: 
- __@MappedSuperclass__: The parent class won't be persisted in the DB by itself. 
The subclass (marked with the @Entity annotation) will be persisted with the inherited fields.

Annotations for strategies below: @Inheritance(strategy = InheritanceType.STRATEGY_NAME

- __Single Table__: 
Creates one table for each class hierarchy. 
The attributes of all entities are mapped to the __same database table__. 
Each record uses only a subset of the available columns and sets the rest of them to null. 
This is also the default strategy chosen by JPA. 
Since only one table needs to be accessed this strategy makes polymorphic queries very efficient and provides the best performance.

- __Joined Table__: 
Each class in the hierarchy is mapped to its table. 
The relations are handled with identifiers as foreign keys, which will be used for joining them when needed. 

- __Table per class__:
The Table Per Class strategy maps each entity to its table which 
contains all the properties of the entity, including the ones inherited.
Very similar to the _Mapped super class_ strategy, but unlike it, 
table per class will indeed define entities for parent classes.
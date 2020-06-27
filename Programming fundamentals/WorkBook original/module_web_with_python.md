# Web with Python questions

## Software design

### Clean code

#### Point out 5 suggestions, how to format an SQL query!

1. Use either all lowercase, or uppercase for sql statements.
2. Structure your code vertically. For example, list fields vertically in a SELECT.
3. Maximum one SQL keyword per line.
4. The SQL query should do one thing. Separate the logic into multiple steps if necessary.
5. Only use comments when absolutely necessary, and the comment should be short and stating the general purpose of the code

#### What layers can you name in a simple web application?
[layers](https://docs.google.com/presentation/d/1PUggE2mhGVsbtOd62m82mNX8pl0P5MsmSrFw5G4zBfw/edit#slide=id.p7)

I. Client: Browser frontend

II. Controller/Routing: Python Flask

III. Data storage: SQL, CSV

IV. Templating engine: jinja -> HTML

### Error handling
#### What error can occur, when an array does not have an element on the requested index?

"index out of range"

#### What is the “finally” block, and how would you use it?
[link](https://docs.python.org/3/tutorial/errors.html)

The `finally` block can be part of error handling, after the `try` statement. 

A `finally` clause is always executed before leaving the `try` statement, whether an exception occurred or not. 
It is also executed "on the way out" when any other clause (feltétel) of the try statement is left via a "break", 
"continue" or "return" statement. 
It is especially useful in these situations. 

#### Why should we catch special exception types?

To handle these exceptions accordingly, and alter the behaviour of our code more fitting to the situation. 
For example in case of user-end failure we want to notify the user of the possible cause, and let him to try again.

### Security
#### What is SQL injection? How to protect an application against it?

It is a computer attack, in which code/SQL commands are injected to the backend database.

This way the end user input can alter the original SQL query to do things it wasn't originally designed to.
For example to gain access to data the end user wouldn't have permission for, or to delete data.

The root cause of almost every SQL injection is invalid input checking.

__First__, filtering escape characters. 
This way statements like:

    SELECT * FROM table
    WHERE Name = ' "Username 
    ' OR '1' = '1 

can't be given as input, just like script injection.

__Second__, use SQL parameters for protection. 
Cursor execute uses this when variables are passed to it separately.
(Also sql.SQL...sql.Identifier)

#### What is XSS? How to protect an application against it?
Check the examples: https://en.wikipedia.org/wiki/Cross-site_scripting

XSS: Cross-Site Scripting

No. 1. vulnerability on the web today.
Another type of injection, where the attacker uses a web application to obtain data from another end user. 
The attacker injects side scripts into a website, which the other user's browser
will believe to be trusted when visiting that website, then download and execute them.

These scripts can access cookies, session tokens or any other information stored by the browser of the attacked user.
XSS can be prevented by validating input, including forms, query strings, cookies, request headers
and basically anything that we cannot be sure about being completely secure.

#### How to properly store passwords?

Use a hashing algorithm with salt, and store it in a database.

#### What is HTTP?
HTTP: HyperText Transfer Protocol

A __request-response__ protocol in the __client-server__ model.
It is the foundation of data-communication for the web (__www__).

#### What is HTTPS?

HTTPS: Hypertext Transfer Protocol Secure

- HTTPS is an extension of the HTTP.
- HTTPS is used for secure communication, the communication protocol (request-response) is therefore __encrypted__ 
to protect against man-in-the-middle attacks.
- The client, through HTTPS, asks for the web server's __TLS certificate__ (TLS: Transport Layer Security), 
which verifies the website's identity. TLS certificates are like online ID cards.
When it is verified, an encryption method is chosen, so only at the endpoints are the message decrypted.
(For the detailed process check below asymmetric and symmetric encrypting)
		
#### What is encryption and decryption?

Encryption is the process of translating plain text data (plaintext) into something that appears to be random and 
meaningless (ciphertext).
Encryption is usually done using key algorithms.

Decryption is the process of converting ciphertext/encoded data back to plaintext.

#### What is hashing?

Hashing is:

- a type of algorithm
- which takes any size of data
- and turns it into a fixed-length of data, to a "fingerprint" or "hash" 
(two different objects can have the same hash, since there is infinite number of strings for example, but finite number of hash)
- this is a one-way process, it can not be reversed
- it is deterministic, meaning that the same message always results in the same hash.

#### What is the difference between encryption and hashing? When would you use which?

Encryption is done using key algorithms, which also used for description, so the original data can be restored.

Hashing is a one-way process, and the original data can not be recovered.

When the original data needs to be used, for example human-readable messages, encryption is advised.
When the original data is not important, only the difference or "fingerprint" of it, like passwords, then hashing is more fit.

#### What encryption methods do you know?
[link1](https://www.venafi.com/blog/what-are-best-use-cases-symmetric-vs-asymmetric-encryption)
[Symmetric encryption](https://www.cryptomathic.com/news-events/blog/symmetric-key-encryption-why-where-and-how-its-used-in-banking)

__Symmetric Key__:
- The encryption and decryption keys are the __same__. In these algorithms the same cryptographic keys are used for 
both encryption and decryption.
- The main advantage of symmetric cryptography is that it is much __faster__ than asymmetric cryptography.
- The disadvantage is __key management__: 
    + Key exhaustion: every use of a key ‘leaks’ some information that can potentially be used by an attacker to reconstruct the key.
    + Unlike asymmetric (public-key) Certificates, symmetric keys do not have embedded metadata to record information such as expiry date or 
    an Access Control List to indicate the use the key may be put to - to Encrypt but not Decrypt for example.
- Use cases: 
    + Banking sector: Due to the better performance and faster speed of symmetric encryption, symmetric cryptography is 
    typically used for bulk encryption of large amounts of data. Example: Payment applications.
    + Data at rest: Data that is not actively moving from device to device or network to network.
    

__Asymmetric Key__:
- Asymmetric encryption uses __two__ keys for encryption. 
The _public key_ is available for anyone to use and encrypt messages.
However, only the possessor of the _private key_ can decrypt the message. 
- The main disadvantage of asymmetric encryption is that it is __slow__ when compared with symmetric encryption.

![alt text](https://upload.wikimedia.org/wikipedia/commons/4/4d/Illustration_of_digital_signature.svg)

- __Digital Signatures__: it is used to detect unauthorized modifications to data and to authenticate the identity of the signatory.
Digital signatures are intended for use in electronic mail, electronic funds transfer, electronic data interchange, software distribution, 
data storage, and other applications that require data integrity assurance and data origin authentication.

__Use Case of Asymmetric and Symmetric Encryption: HTTPS__:

An HTTPS connection between a client and a server, employs both types of encryption. 
Asymmetric encryption is used first to establish the connection, which is then replaced with symmetric encryption (called the session) for the duration of the connection.

Steps:
1. For the server and client to engage in a secure conversation, a __TLS certificate__ needs to be created and verified.
2. The browser sends a __ClientHello__ message and indicates that it would like to start a conversation with a secure server. 
The ClientHello message contains all the information the server needs in order to connect to the client.
ClientHello -> You can reach me here, this is how we can talk.
3. The server responds with a __ServerHello__ message which includes the TLS version to be used, the server TLS certificate, and the server’s asymmetric public key.
ServerHello -> This is how we gonna communicate, this is who I am, encrypt message using this.
4. The browser verifies the server certificate, and creates a random __session key__.
5. The session key is __encrypted__ using the server’s public key and is sent back to the server.
6. The server __decrypts__ the session key with its own private key.
7. Now both parties have the session key. The public key encryption is terminated and replaced with __symmetric encryption__. 
The session with the server continues using only symmetric encryption.

The asymmetric encryption is only used briefly in the beginning to exchange the symmetric session key which is used for the rest of the connection. 
This is done in order to overcome the main disadvantage of asymmetric encryption, being slow and resources exhaustive because of its mathematical complexity. 
On the other hand, the use of asymmetric encryption solves the problem of key distribution experienced in symmetric encryption.

#### What hashing methods do you know?
https://blog.jscrambler.com/hashing-algorithms/

SHA-family.

Bcrypt.
It uses salt to protect against rainbow table attacks and the iteration count can be increased over time to 
resist brute-force search attacks.

Salting:
Short, random set of characters that are appended to the ends of a user's passwords before they are hashed.
Salts are added automatically after a user enters their password, they are not aware of the existence of the salt.
Salts are stored in plain text along with the hashed output, so the system knows which salt to use when it comes to verifying.

#### How/where would you store sensitive data (like db password, API key, ...) of your application?

As an environment variable.

## Computer science

### Algorithms

#### What is the difference between Stack and Queue data structure?
https://www.youtube.com/watch?v=8aGhZQkoFbQ&list=PLLzzURkevF3K67E0Kygy6Qv4w-bHuCtCb&index=6&t=0s

Both are ordered list of elements.

__Stack__:
- both adding new items (push) and removing them (pop) happens at only one end of the Stack called TOP, this means...
- the element inserted at the last is the first element to come out (LIFO: last in first out) 
- a data type with a limited capacity
- the Stack is said to be in Overflow when it is full, and Underflow when it is empty

__Queue__:
- adding new elements (enqueue) happens at the REAR, and removing (dequeue) happens at the FRONT, this means...
- the first element inserted is the first element to be removed (FIFO: first in first out)
	
#### What is BubbleSort? Describe the main logic of this sorting algorithm.

![alt text](https://en.wikipedia.org/wiki/Bubble_sort#/media/File:Bubble-sort-example-300px.gif)

A sorting algorithm which considered simple but slow and impractical in most cases.
The algorithm repeatedly walks through the array, and swaps adjecent (szomszédos) pairs of numbers if necessary. 
After each iteration, the last element doesn't need to be compared, because the highest number "emerged" 
to the last position, this is why this algorithm called "BubbleSort".
The process continues until the array is sorted. 

It's time complexity is O(N^2).

#### Explain the process of finding the maximum and minimum value in a list of numbers!

Min search:

The algorithm needs to repeatedly compare two numbers. It can be done in a single walk through.
The algorithm first compares the first two number of the array, and selects the smaller, and stores it in a 
variable. Then compares the third number and the stored one, and the stored one will be changed if it is smaller. 
If it's not smaller, the algorithm compares the forth one with the stored one, and so on, and at the end of the array
returns the stored smallest number.
    
    
#### Explain the process of calculating the average value in an array of numbers!

We need two values to calculate the average, the SUM of all the elements in the array, and the number of elements,
or the length of the array. Each can be calculated in a single walk through.

#### What is Big O complexity? Explain time and space complexity!

The big O notation describes the time or space complexity of a code based on the input.
It means how much resource (time or memory) is needed to complete a task, and how will it change with the size of the input.

Time complexity:

- O(1): _Constant time complexity_, meaning the time needed for the task doesn't change with the size of the input. 
For example: getting the first element of an array, or sending a message with a pigeon.

- O(log N): _Logarithmic time complexity_. Always assume that searching algorithms on a sorted array are log(n), 
like doing binary search in a sorted list is O(log2 N) complexity. 

- O(N *(log N)): Sorting.

- O(N): _Linear time complexity_, N meaning the amount of data. Twice the data needs twice the time, like iterating through the 
elements of an array.

- O(N^x): in case of nested loops, x means the number of loops. N^2 is for example: every element in a collection has to be compared to every other element ("The handshake problem").

- O(x^N): _Exponential time complexity_. Recursive solution for calculating the Fibonacci series. This is really bad. Try to avoid it!

Calculating rules:
- round up to the worst scenario
- drop non-dominant terms: 6x^4 - 2x^3 + 5 -> O(x^4)

#### Explain the process of calculating the average value in a linked list of numbers!

Similarly to finding the average value of a list, we add the value of all the nodes, then dividite it
by the number of nodes.

### Procedural
#### How the CASE condition works in SQL?

The CASE statement evaluates values based on the conditions defined, and returns a value defined with the
THEN statement if true, or the value defined with the ELSE statement if false. If there is no ELSE statement
and none of the conditions evaluate true, it returns NULL. Once a condition evaluates true, the value is returned
and no other conditions are evaluated.

```sql
SELECT character, has_won
CASE
    WHEN has_won = 'true' THEN 'Win'
    WHEN has_won = 'false' THEN 'Die'
    ELSE 'There is no middle ground'
END
FROM game_of_thrones;
```

#### How the switch-case condition works in JavaScript?

```javascript
switch( 2 + 2 === 4) {
  case true:
    console.log('Correct!')
    break;
    
  case false:
    console.log('Nope!')
    break;
    
  default:
    console.log('Neither(?!?!)')
}
```

#### How to achieve a switch-case-like structure in Python?

```python
def switch_in_python(expression): 
    switcher = { 
        'fruits': 'apple, orange, strawberry', 
        'vegetables': 'carrot, broccoli, cucumber', 
    } 
    return switcher.get(expression, "junk food")
    

print(switch_in_python('fruits')) 
# should output 'apple, orange, strawberry'
```

Python's built-in get() method returns the value of the key passed as the first parameter, and returns a default
value passed as second parameter.

#### Explain variable scoping in Python!

__Scope__: the part of the program where a variable is accessible.

__Global variable__: defined in the main body. It can be accessed from anywhere in the file.

__Local variable__: defined inside a function. Accessible only inside the function it has been defined in, and
exists until the function is executing.
    
```python
a = 0

def func():
    a = 3 #--> does not change the global variable
    print(a) #--> the local variable will ALWAYS take precedence
    
func() #--> 3
print(a) #--> 0
```

#### What’s the difference between const and var in JavaScript?
https://www.youtube.com/watch?v=6vBYfLCE9-Q

VAR:
- function scoped (hoisting)

CONST:
- block scoped (just as "let")
- value can be assigned only ONCE 
(but for example if it's an object, the value of the object can be changed, but a new object can't be assigned to it.)
    
#### How the list comprehension looks like in Python?

```python
arr = [1, 2, 3, 4]
new_list = []

for i in arr:
    new_list.append(i * 2)
    
#List comprehension:

new_list = [i * 2 for i in arr]
```

#### How the “ternary expression” looks like in Python?
http://book.pythontips.com/en/latest/ternary_operators.html

Blueprint:
'exprIfTrue' if 'condition' else 'exprIfFalse'

Example:

    age = 26
    beverage = "Beer" if age >= 21 else "Juice"
    
    print(beverage)  # "Beer"

#### How the ternary expression looks like in JavaScript?
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator

Blueprint:
'condition' ? 'exprIfTrue' : 'exprIfFalse' 

Example:
    
    var age = 26;
    var beverage = (age >= 21) ? "Beer" : "Juice";
    console.log(beverage); // "Beer"
        
#### How to import a function from another module in Python?

    from file_name (without the ".py" extension) import function_name

#### How to import a function from another module in JavaScript?
https://v8.dev/features/modules

__External__:

I. Mark the function you want to export with the `export` keyword:


    export const repeat = function (string){
        return `${string} ${string}`;
    
II. Import the function with the `import` keyword, and the `from` keyword to mark the file:

// 📁 main.js

    import {repeat, shout} from './lib.js';


III. Mark in html you are using modules:


    <script type="module" src="main.js"></script>

__Internal__:

	</div>
	<script type="module">
		import { Student } from './models/student.js';

		window.onload = function () {
		    var x = new Student();
		    x.course.id = 1;
		    document.getElementById('myDiv').innerHTML = x.course.id;
		}
	</script>

### Functional
#### What is recursion?

When a function calls itself.

#### Write a recursive function which calculates the Fibonacci numbers!

    def recur_fibo(n):

       if n <= 1:
           return n
       else:
           return(recur_fibo(n-1) + recur_fibo(n-2))
    
    nterms = 10
    
    for i in range(nterms):
        print(recur_fibo(i))

#### How to store a function in a variable in Python?

    def my_func():
        print('yep')
    
    f = my_func
    
    f() # 'yep'

#### List the ways of defining a callable logical unit in JavaScript!
    !!!!!!!!!!!

    var my_func = func() {
        hablaty;
    };
    
    function my_func() {
        hablaty;
    };
    
    !!!!!!!!!!!
    
#### What is an event listener? How to attach one?

The event listener calls a given function (callback) whenever an event is delivered to the target.

1. We need the element to put event listener on:


    let element = document.querySelector('#idOfElement')

(1/b. If you have multiple elements you need to iterate through them)

2. Use the addEventListener function
3. Declare the event you want to listen to
4. And the callback function you want to execute in case the event happens:


    element.addEventListener('click', function() {
    console.log('tits');
    })
        
#### How to trigger an event in JavaScript?
https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/dispatchEvent
https://javascript.info/dispatch-events

Using the dispatchEvent().

	<button id="elem" onclick="alert('Click!');">Autoclick</button>

	<script>
	  let event = new Event("click");
	  elem.dispatchEvent(event);
	</script>
    
#### What is a callback function? Tell some examples of its usage.

A callback is a function which is passed as an argument to another function.
The "main" function can call this callback function immidiately (sycnhronous callback), 
or at another given time/occasion (asynchronous callback).

The addEventListener is passed a callback, which will be executed when the event is triggered.

#### What is a Python decorator? How does it work? Tell some examples of its usage.

A decorator is a function that takes another function as an argument (function_to_wrap), generates a new function (func_wrapper), 
using the behaviour of the original function, and returning the generated function so we can use it anywhere.

	def function_to_wrap(text_parameter):
	   return "Wrapped function. Its parameter: " + text_parameter

	def decorator(func):	       #the decorator delivers/returns the modified function, the func_wrapper
	    def func_wrapper(name):    #the func_wrapper will be the modified function that will be returned 
			print("Wrapper function first part")
			print(func(name))
			print("Wrapper function last part")

	    return func_wrapper


	function_to_wrap = decorator(function_to_wrap)     #the original function (function_to_wrap) is modified by the decorator, and its new 
							   							#value/function will be the returned 'func_wrapper' function
	function_to_wrap("John")

It prints out:
Wrapper function first part
Wrapped function. Its parameter: John
Wrapper function last part

Python decorator syntax:

	def decorator(func):

	    def func_wrapper(name):
			print("Wrapper function first part")
			print(func(name))
			print("Wrapper function last part")

	    return func_wrapper


	@decorator   #instead of 'function_to_wrap = decorator(function_to_wrap)'
	def function_to_wrap(text_parameter):
	   return "Wrapped function. Its parameter: " + text_parameter


	function_to_wrap("John")

Example:
Askmate connection handler. The function containing the SQL query was the function_to_wrap, and the connection handler was 
the decorator which returned a modified function which contained the necessary code to open the database, initialize the cursor, 
close the database.

#### What is the difference between synchronous and asynchronous execution?

__Synchronous__:
In a synchronous execution tasks are executed consecutively (egymást követően). This means every task needs to be finished before
moving to another task. 

__Asynchronous__:
In asynchronous execution multiple tasks can be executed in the same time, on multiple threads. 

## Programming languages

### SQL

#### How can you connect your application to a database server? What are the possible ways?

Using __PSQL__:

1. Start psql in your project by entering to terminal: psql

2. Connect to the database by running the following command:
\c database_name

3. Save the environment variables in your IDE to make connection automatic

#### When do you use the DISTINCT keyword in SQL?

When you are only interested in _unique_ values, and want to eliminate duplicates.

#### What are aggregate functions in SQL? Give 3 examples.
https://www.zentut.com/sql-tutorial/sql-group-by/
https://sqlbolt.com/lesson/select_queries_with_aggregates

An aggregate function allows you to perform a calculation on a set of values to return a single scalar value. 

1. __GROUP BY__:
It is used to group records into a set of summary rows based on values of columns.
It is mostly used when you don't just want to aggregate across all the rows, but instead use it on individual groups.

2. __AVG__:
It calculates the average of the given values.

3. __SUM__:
It calculates the sum of the given values.

#### What kind of JOIN types do you know in SQL? Could you give examples?

1. __JOIN/INNER JOIN__:
Shows the records from the joined entities that have matching values in both.

2. __LEFT JOIN__:
Shows the records from the first entity with matching second (right-most) entity records.

3. __FULL JOIN__:
Shows all records from all entities.

#### What are the constraints in sql?

SQL constraints are rules used to limit the type of data that can go into a table.
E.g.: NOT NULL, UNIQUE.

#### What is a cursor in SQL? Why would you use one?
https://www.c-sharpcorner.com/article/cursors-in-sql-server/

It is an object which executes the commands from record-to-record.

#### What are database indexes? When to use?
- https://www.youtube.com/watch?v=zDzu6vka0rQ
- https://www.essentialsql.com/what-is-a-database-index/

Database indexes order the records of a table according to an index, like a phonebook, where the names are in alphabetical order. 
This helps to speed up database queries, because you dont have to go through every record, but can jump to the correct index.
Especially useful in the case of bigger databases.

#### What are database transactions? When to use?

A transaction is a list of commands that alter a database, like INSERT, DELETE, UPDATE. 
The difference between an actual list of commands and a transaction is, that in a transaction the commands are _ACID_:

- __Atomic__: all the commands are executed successfully, otherwise the transaction is aborted, and the changes are "rolled back"
to the previous state

- __Consistent__: the database properly changes in case of successful transaction

- __Isolated__: Each transaction is independent and transparent from/to eachother

- __Durable__: The change of the transaction stays even in the case of system failure

#### What kind of database relations do you know? How to define them?

__One-to-One__: Two tables have only _one_ matching values. Like the ID of a person in one table, and tax-identification in another.

__One-to-Many__: One of the table has multiple matching values in another. Like a person can have only one hometown, but a
town can be the hometown of many.

__Many-to-Many__: It's like two one-to-many relation through a reference table, where the primary keys of the two tables are.
Like in the PA database. Genres and shows, each genre can belong to many shows, and each show can have many genres.

#### You have a table with an “address” field which contains data like “3525, Miskolc, Régiposta 9.” (postcode, city, street name and address). How would you query all records related to Miskolc?

	WHERE address LIKE '______Miskolc%'

#### How would you keep track of what kind of data has changed after an UPDATE or DELETE operation in a table?

The most common solution to this is having an audit table, which “logs” the changes made in the table, 
when those changes are happening. For each column of the original table we should have an audit-column in the other 
plus a column for who made the change. 

### HTML & CSS

#### What’s the difference between XML, XHTML and HTML?

Markup Languages: Sets the __structure__ of the data, rather than the behaviour of it, like python.

__HTML__: The original language of the web, HyperText Markup Language.

__XML__: It is a meta-markup language, meaning it can be used to create other markup languages, to store and transfer data.
It is platform independent. 
It grew out of a desire to be able to use more than just the fixed vocabulary of HTML on the web. 
Special tags can be defined (in the DTD). 
The syntax is much stricter than in HTML.

__XHTML__: It is a reformulation of HTML using XML syntax. The structural conditions are much stricter. It uses XML rulesets as well(?).

#### How to include a JavaScript file in a webpage?

	<script type="javascript" scr="path/to/js/file.js"></script>

#### How to include a CSS file in a webpage?

External:

	<link rel="stylesheet" href="path/to/file.css">

Internal:

	<style>
	body {
	  background-color: linen;
	}

	h1 {
	  color: maroon;
	  margin-left: 40px;
	} 
	</style>

	_Inline_:
	<h1 style="color:blue;margin-left:30px;">This is a heading</h1>

#### How to select an element using its id in CSS?

	#id

#### How to select elements using their class in CSS?

	.class
	
#### How to select elements which have the ‘alpha’ and ‘beta’ classes in CSS?

	.alpha.beta

#### How to select all list items in all ordered lists on the page in CSS?

	ol li

#### How to select elements using their attributes in CSS?

	[attribute]

#### What are UX and UI?

__UI__: User Interface. It's the graphical layout of an application, on which the user interacts with the application.

__UX__: User Experience. The users experience interacting with the application. An application can have a nice UI, but for
example the application's response takes too long, then the UX is bad.

#### Please list some points that an application should fulfill to have good UX.

- Usability: user can understand and use the application in a short time.

- Respinsive design: it looks good on any screen

#### What is XML, XSLT, DTD?

__XML__: Extensible Markup Language. A meta-markup language, used to create other markup languages. Special tags can be defined (in the DTD).
        The syntax is much stricter than in HTML.

__DTD__: Document Type Definition. It is a set of markup declarations that define the valid building blocks of an XML document.
It is part of every XML document.

__XSLT__: Extensible Stylesheet Language Transformations. It is a language for transforming XML into HTML.

#### What is the difference between HTML and XML?

While HTML is a predefined markup language, XML provides a framework for creating markup languages.

### Javascript

#### What is javascript?

It is a lightweight, interpreted (just-in-time compiled) programming language. It is the scripting language of the web,
but also used in non-browser environments.

#### When to use AJAX? Bring examples of its usage.

AJAX: Asynchronous JavaScript And XML.
It is a __set__ of web development techniques on the __client side__ (HTML, DOM, JSON, Javascript, XMLHttpRequest).

Send and retrieve data in the background, __asynchronously__, without  interfering with the display and behavior of the existing page (refreshing the page).

By __decoupling__ the data interchange layer from the presentation layer, Ajax allows web pages and, by extension, web applications, 
to change content dynamically without the need to reload the entire page.
It is useful because:

- __Can be faster__: in the case of needing only some particular data, and instead of loading the whole page again 
you just have to request that data.

- __More practical, more comfortable__: for example, you don't have to reload the page after you posted a new message in a chat room,
or in the case of other real time applications.

- __Reduces server load__: because doing it only when needed, asynchronously, means less http requests, so the load time will be shorter.

__Examples__:
- Form validation
- Sort or Filter
- Chat websites
- Vote or rating

#### What is DOM and how to manipulate it from Javascript?
https://www.youtube.com/watch?v=H63dVFDuJDM
https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction

__DOM__: Document Object Model

- __Document__: the webpage
- __Object__: every HTML element in the document is an object (and we can modify objects)
- __Model__: the hierarchy between the elements, the parents and children -> the DOM Tree

Through the DOM we can manipulate the HTML page.
The DOM represents the document as __nodes__ and objects.

Javascript __uses__ the DOM to access the document.
We can create new elements, or change and delete an existing one.

#### What are events and how/why to use them in Javascript?

Event is a signal that something happened. 

We can use them with a function, called "event handler".

#### What is event bubbling/capturing? How would you use it?
https://javascript.info/bubbling-and-capturing

When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.
It emerges, like a bubble.
It can be stopped with _event.stopPropagation_.
It is useful when you dont have the clicked element yet, but know which will be its parent, so you put a listener on the parent.

Event capturing means that the event first has to go down to the element from the "top": window -> document -> <html> -> <body> ...

#### What is JSON and how do we use it?

- JavaScript Object Notation.
- JSON is a file and data interchange format, that uses human-readable text to __store__ and __transmit__ data objects.
- The objects consist of __attribute-value pairs__ and __array__ data types.
- It is widely used to _send/receive_ data between servers, or to _store_ data in localStorage or sessionStorage.

## Software engineering

### Version control

#### What type of branching strategy would you use?
https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow

Gitflow Workflow

#### What would you do if you find a bug on the production code (master branch)?

1. Create a new branch from master called hotfix
2. Fix the bug
3. Test it
4. Merge it into master and development  (or the current release branch)

#### How can you move changes from one branch to another in GIT?

    git merge <branch>

#### How does a VCS help with code reviews?
https://www.youtube.com/watch?v=jFnYQbUZQlA

__VCS__: Version Control System, like git

It helps to keep track of the changes, who changed what, and compare files and code snippets. 
With a VCS accessing the code by multiple people is also easier.

#### What is your favorite git command? Why?

    git checkout -b <branch_name> 
    
Because it creates and checks out a new branch at the same time

#### What does remote/local mean in Git?

Local repos stored locally.
Remote repos stored on a remote server and can be accessible for multiple people.

### DevOps

#### Why is it good to use a package manager software?

__pip__:

- Helps with complex dependencies (it downloads all the dependencies a package needs)
- Helps checking if there is a newer version

#### Why is it good to use a virtual environment for a project?

A virtual environment is like an isolated box. 
It can contain different environments for different projects.
This way conflicting requirements can be kept separately.

### Networks

#### What kind of HTTP status codes do you know?

- 200: OK
- 300: Redirected
- 400: Client side error (404: page not found)
- 500: Server side error

#### What is a API?
https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/

Application Programming Interface is like a _user interface_, but for applications, which allows the 
applications to communicate.
It specifies how these applications should interact.

It's the _"middle man"_ that serves the information, the part of a system which is created for communication.
It can be a piece of software with the task of communication.
It can be a whole server, a whole app, or just a small part of an app.

#### What is REST API?
[REST article](https://launchschool.com/books/working_with_apis/read/rest_and_crud#rest)

[REST video](https://www.youtube.com/watch?v=Q-BpqyOT3a8)

_Representational State Transfer_ is: 
- an architectural style,
- using __CRUD__ (in HTTP: Create: POST, Read: GET, Update: PUT, Delete: DELETE) methodology,
- to build APIs.

By limiting actions to CRUD, REST requires thinking in a __resource-oriented__ way.
The resources are the server objects, like a blog-post, which can be acted upon.

__State transfer__ refers to how HTTP is a stateless protocol. This means that servers don't know anything at all 
about the clients, and that everything the server needs to process the request (the state) is included in the request itself.

REST APIs can be used by virtually any programming language, because it mainly uses the HTTP protocol and JSON format for communication.

REST API conventional endpoints specify the __resource__ you want to act upon:
- __GET__ a resource: /profiles/:id
- __POST__ a resource: /profiles  (request has body)
- __PUT__ a resource: /profiles/:id (request has body)
- __DELETE__ a resource: /profiles/:id

__Guiding principals__:
- __Client-server__: separate the user interface and data storage system, so the UI can be used elsewhere as well, and the server side will be simpler, so easier to scale-up

- __Stateless__: each request must contain every necessary information.

- __Layered system__: the system is made up of layers, hierarchically, and their behaviour specified. 
For example: the layers cannot "see" beyond the immediate layer they are interacting with.

#### What is JSON? When to use?

Read above. When two systems, like client-server, or server-server wants to communicate.

#### What is TCP/IP? What layers does it define, what are they responsible for?
https://searchnetworking.techtarget.com/definition/TCP-IP
![alt text](https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/UDP_encapsulation.svg/800px-UDP_encapsulation.svg.png)

It's a protocol (Transmission Control Protocol/Internet protocol) which defines how information moves from sender to receiver.

Application layer --> Transport layer -->  Network layer --> Physical layer

1. __Application layer__: Standardized data exchange. __HTTP, FTP, DNS__.
2. __Transport layer__: Reliability control and data correction. 
Maintains end-to-end communications across the network. It divides the data into smaller packets. __UDP__ (e.g. DNS), __TCP__ (e.g. HTTP).
3. __Internet layer__: It encloses the packet, and decides where to send it. Internet protocol: __IPV4, IPV6__.
4. __Physical layer__: this layer interconnects nodes or hosts in the network and transmits the packets over a specific network hardware. __WIFI, Ethernet__. 

#### What’s the difference between TCP and UDP?

In __TCP__ an error message is sent if a package has not arrived, so it will be sent again.
 
__UDP__ throws the error-checking. So it will be faster, BUT: packets are just sent to recipient without caring he get them or not.
UDP is used when speed is desirable and error correction is not necessary. /live broadcasts, streaming/

#### How does an HTTP Request look like? What are the most relevant HTTP header fields?
https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages#HTTP_Requests
http://go-colly.org/articles/scraping_related_http_headers/

    GET /home.html HTTP/1.1
    Host: www.yoursite.com

__Start-line__:
1. HTTP method (GET, POST, PUT...): the verb (or noun), which describes the action to be performed.
2. Request target: usually a URL
3. HTTP version

__Headers__: key-value pairs in a single line, which doesn't relate to the content of the message.
        Some of the most important ones:

- Host: the address of the sender (this is a mandatory header field) 
- User-Agent: a description of the client's application type, browser, operating system
- Cookies

#### How does an HTTP Response look like? What are the most relevant HTTP header fields?
https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages#HTTP_Responses

    HTTP/1.1 200 OK
    Date: Mon, 27 Jul 2009 12:28:53 GMT
    Server: Apache/2.2.14 (Win32)
    Content-Length: 88
    Content-Type: text/html
    Connection: Closed

__Status-line__:
1. HTTP version
2. Status code, indicating success or failure of the request

__Headers__:
- Content-type
- Content-length
- Cookies

#### What is DNS? How does it work?

The __Domain Name System__ (DNS) is a naming database in which internet domain names are located and translated 
into internet protocol (IP) addresses. 

#### What is a web server?
https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server

A web server includes several parts that control how web users access hosted files, at minimum an HTTP server. 
An HTTP server is a piece of software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages). 
It can be accessed through the domain names (like mozilla.org) of websites it stores, and delivers their content to the end-user's device.

#### Explain the client-server architecture.

Describes how a server provides resources and services to one or more clients.
This type of architecture has one or more client computers connected to a central server over a network or internet connection.

#### What would you use a session for?

Because HTTP is stateless, in order to associate a request to any other request, you need a way to store user data between HTTP requests.
Cookies are suitable ways to transport data between two or more request. 
However mobiles can't deal with cookies.
The solution is to store data server side, give it an id, and let the client only know that id.
This is especially useful in websites where login is required.
However, nowadays JWT is used for this purpose:

https://www.youtube.com/watch?v=soGRyl9ztjI

Session token: __Reference__ token

JWT: __Value__ token

#### What would you use a cookie for?

__Cookie__: a cookie is a small piece of data sent from a website and stored on the user's computer by the user's web browser 
while the user is browsing. Since it is stored on the client side, it can be deleted or modified by the user 
or the user can disable the whole cookie feature in her browser.

Cookies are mainly used for simple data that shouldn't be trusted (since the user can tamper with it), 
mainly for preferences settings on a site (but cookies are used for e.g. showing you personalized ads as well).

EXCEPT!

HTTP only cookies can't be tampered with, that's why it is widely used for authorization, using JWT.

## Software Development Methodologies

#### What kind of software development methodologies do you know? What are the main features of these?
http://www.agilenutshell.com/what_is_agile

Agile is more adaptable to changes as there is no in-depth planning at the beginning of a project rather 
there are changing requirements throughout the course of the project. 
A constant feedback from the end users is encouraged. In agile, there is an incremental and iterative development approach.

__Agile__: 
- Time boxed
- Iterative approach (starting with something simple, and adding to it incrementally (fokozatosan))
- Working incrementally instead of trying to deliver the product all at once

__How does it work?__:
- Make a TODO list about the features the customer wants: user stories
- Estimation
- Execute
- Update the plan as you go -> Adaptive planning


__The 12 principles of the Agile Manifesto__:
- Customer satisfaction is of highest priority
- Accommodate changing requirements even in later phases of development.
- Deliver working software frequently in a shorter timescale.
- Business team and developers must collaborate on a daily basis throughout the project.
- Higher autonomy is given to the team members with greater support and trust.
- Face-to-face interaction is critical for conveying information within a development team.
- The progress of the project is measured by working software.
- Promote sustainable development by maintaining a constant pace indefinitely.
- Technical excellence and good design should be the main focus.
- Simplicity is essential for progress.
- Self-organizing teams are required for the best architectures and designs.
- The teams should reflect on how to become more effective regularly and adopt the changes to increase effectiveness.

#### What are the SCRUM roles?

__Product owner__: the person with the project vision. Breaks down the project into tasks, prioritizes them, so everything
                meets the objectives and goals of the customer.

__Scrum master__: makes sure the project follows the SCRUM framework. His responsibility is to the process rather than the team.

__Development team__: who execute the project.

#### What are the SCRUM ceremonies?
https://www.visual-paradigm.com/scrum/what-are-scrum-ceremonies/

- Sprint planning
- Daily scrum
- Sprint review
- Sprint retrospective

#### What are the SCRUM artifacts?
https://www.visual-paradigm.com/scrum/what-are-scrum-artifacts/

- Product vision: define the long-term goal of the project/product
- Sprint Goal
- Product backlog: a list of all the changes (features, functions, requirements, enhancements, and fixes) that are required in the product. 

#### What is the main goal of a retrospective meeting?

An opportunity for the Scrum Team to inspect itself and create a plan for improvements for the next Sprint.
	
#### Explain, when would you recommend to use the waterfall methodology?

Suited for Milestone-Focused Development, when the requirements do not change. 
Like when human lives are at stake: building a space shuttle.


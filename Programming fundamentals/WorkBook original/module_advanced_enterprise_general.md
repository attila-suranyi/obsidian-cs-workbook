# Software design

## Security

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

## Threaded programming

### When do you need to use threads in an application?
### What is a daemon thread?
### What is the difference between concurrent and parallel execution of code?
### What is the most important problem developers are faced when using threads?
### In what kind of situations can deadlocks occur?
### What are possible ways to prevent deadlocks from occurring?
### What does critical section or critical region mean in the context of concurrent programming?

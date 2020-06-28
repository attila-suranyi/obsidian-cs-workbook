# Security
- ### JWT^[https://www.youtube.com/watch?v=_XbXkVdoG_0]^[https://jcbaey.com/authentication-in-spa-reactjs-and-vuejs-the-right-way]
	- JSON Web Token (JWT) is an open standard that defines a compact and __self-contained__ way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed.
	
	- __Structure__ 
		![[JWT structure.png]]
		The content of the _header_ and the _payload_ is "visible", a simple encoding shows their value. But to decrypt the _signature_ a password is needed, which the server knows. You can't simply copy the signature of a token then change the content of the payload, because the signature depends on the payload, and changes if the payload is changed. This way from the signature the server knows if the payload has been tampered with.
		
	- JWT can store any type of data, which is where it excels in combination with OAuth.

	- #### JWT for Authorization
		Because __HTTP is stateless__, in order to associate a request to any other request, you need a way to store user data between HTTP requests.

		__Session tokens__ are widely used for this purpose: the server stores all the necessary information about the user, 
		and it gives him a session token with an ID, so every time a user sends a request with the ID, the server looks up the ID with all the necessary data. 
		This token is a __reference token__.

		However, with the rise of microservices this method became difficult, because multiple services need to access the database where the details are stored about the user.

		The JWT authorization solves this problem: all the necessary data (usually user ID, access rights, email...) is safely stored
		in the token and signed by the server, so the server only need to validate the signature, and don't need to look up anything. 
		This is why it is called a __value token__.
	
	- #### How to use JWT Authorization	
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

- ### Oath2^[https://www.youtube.com/watch?v=t4-416mg6iU]^[https://www.youtube.com/watch?v=CPbvxxslDTU]
	OAuth is __authorization between services__.
	
	__The problem__:
	Think of when you want to login into LinkedIn with your Google account.
	The two services don't trust eachother, and the user can't simply give his Google password to LinkedIn. The user doesn't want to give access to its whole account.
	Google need to authorize LinkedIn, and give it __limited__ access to the users account. 
	
	
	__The solution__: The OAuth Flow
	1. User want to login to LinkedIn using his Google account.
	2. LinkedIn sends request to Google for the user account details. 
	3. Google notifies user about this, and asks user whether he gives __limited__ access to his Google account.
	4. If user gives access, then Google gives LinkedIn an __access token__ (JWT token).
	5. Now LinkedIn can use this token to gain limited access to the users account.
	
	![[OAuth flow.png]]
	
	OAuth 2 is an authorization protocol/framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, GitHub, and DigitalOcean. 
	It works by delegating user authentication to the service that hosts the user account, and authorizing third-party applications to access the user account. 
	
	A browser or mobile/desktop client makes a request to the authentication server containing user login information. 
	The authentication server generates a new __access token__ and returns it to the client. 
	The client stores this token (as a cookie/in a file/in LocalStorage/..) and sends it on every request in the HTTP header (Authorization field) to the server(s).
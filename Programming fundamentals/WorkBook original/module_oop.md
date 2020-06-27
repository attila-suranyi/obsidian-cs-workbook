# Software design

## Error handling

### What does 'fail fast' mean in terms of exception handling? Why is it a good practice?
Fail-fast systems are usually designed to stop normal operation (throw an exception) rather than attempt to continue a possibly flawed process.
This way we quickly reveal all problems in our software making it easier to spot and fix them. Shortening the feedback loop results a more stable application.

# Computer Science
## Database
### How can you connect your application to a database server? What are the possible ways?
Java can reach the database via two different interfaces:

- JDBC (Java DB Connectivity) is the lower level. You can run SQL queries via this.
- JPA (Java persistence API) is the higher level one. This is the Java standard for ORM (Object Relational Mapping). 
I.e. it maps DB tables to classes so the Java developer do not need to deal with DB tables, only objects.

### What do you know about database normalization?
Database normalization is the process of structuring a relational database in accordance with a series of so-called normal forms in order to reduce data redundancy and improve data integrity.
Structuring means organize a database into tables and columns. The idea is that a table should be about a specific topic and that and only supporting topics included.


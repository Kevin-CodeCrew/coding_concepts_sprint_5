###### Top
[Back to Concepts](README.md) | [Jump to Bottom](#Bottom) | [Resource](#)
## Restful Web Service + HTTP Requests

### What does RESTful mean?

REST stands for `REpresentational State Transfer`. REST is web standards based architecture and uses HTTP Protocol. It revolves around resource where every component is a resource and a resource is accessed by a common interface using HTTP standard methods. REST was first introduced by Roy Fielding in 2000.

A REST Server simply provides access to resources and REST client accesses and modifies the resources using HTTP protocol. Here each resource is identified by URIs/ global IDs. REST uses various representation to represent a resource like text, JSON, XML but JSON is the most popular one.

REST refers to a set of defining principles for developing API. It uses HTTP protocols like GET, PUT, POST to link resources to actions within a client-server relationship. In addition to the client-server mandate, it has several other defining constraints. The principles of RESTful architecture serve to create a stable and reliable application that offers simplicity and end-user satisfaction.

### CRUD

CRUD is an acronym for `CREATE`, `READ`, `UPDATE`, `DELETE`. These form the standard database commands that are the foundation of CRUD.

Many software developers view these commands as primitive guidance, at best. That’s because CRUD was not developed as a modern way to create API. In fact, CRUD’s origins are in database records. By definition, CRUD is more of a cycle than an architectural system. On any dynamic website, there are likely multiple CRUD cycles that exist.

For instance, a buyer on an eCommerce site can CREATE an account, UPDATE account information, and DELETE things from a shopping cart. A Warehouse Operations Manager using the same site can CREATE shipping records, RETRIEVE them as needed, and UPDATE supply lists. Retrieve is sometimes substituted for READ in the CRUD cycle.
```
Create
CREATE procedures generate new records via INSERT statements.

Read/Retrieve
READ procedures reads the data based on input parameters. Similarly, RETRIEVE procedures grab records based on input parameters.

Update
UPDATE procedures modify records without overwriting them.

Delete
DELETE procedures delete where specified.
```
### HTTP Request Methods
HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred to as HTTP verbs. The HTTP verbs comprise a major portion of our “uniform interface” constraint and provide us the action counterpart to the noun-based resource. The primary or most-commonly-used HTTP verbs (or methods, as they are properly called) are POST, GET, PUT, PATCH, and DELETE. These correspond to create, read, update, and delete (or CRUD) operations, respectively.
```
GET
The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.

POST
The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server.

PUT
The PUT method replaces all current representations of the target resource with the request payload.

DELETE
The DELETE method deletes the specified resource.
```
###### Bottom
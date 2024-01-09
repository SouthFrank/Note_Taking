An application programming interface is a way for two or more computer programs to communicate with each other. It is a type of software interface, offering a service to other pieces of software. A document or standard that describes how to build or use such a connection or interface is called an API specification.

#### RESTful API
A RESTful API is an architectural style for an application program interface (API) that used HTTP requests to access and use data. That data can be used to GET, PUT, POST, PATCH, DELETE, which refers to the creating, reading, updating, and deleting of operations concerning resources. This is commonly referred to as a [[CRUD]] application.

In REST terminology, we refer to individual data objects, such as the notes in our application, as resources. Every resource has a unique address associated with it - its URL. According to a general convention used by json-server, we would be able to locate an individual note at the resource URL _notes/3_, where 3 is the id of the resource. The _notes_ URL, on the other hand, would point to a resource collection containing all the notes.

Data formats the REST API supports include:

- application/json
- application/xml
- application/x-wbe+xml
- application/x-www-form-urlencoded
- multipart/form-data

Resources are fetched from the server with HTTP GET requests. For instance, when using json-server, a GET request to the URL *notes/3* will return the note that has the id number 3. An HTTP GET request to the *notes* URL would return a list of all notes.

Creating a new resource for storing a note is done with an HTTP POST request. The POST request is made to the URL where the collection is held.


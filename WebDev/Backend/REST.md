Representational State Transer, aka REST, was introduced in 2000 in Roy Fielding's dissertation. REST is an architectural style meant for building scalable web applications.

 Singular things, like notes in the notes application of FSO, are called **resources** in RESTful thinking. Every resource has an associated URL which is the resource's unique address/

One convention for creating unique addresses is to combine the name of the resource type with the resource's unique identifier.

Let's assume that the root URL of our service is www.example.com/api.

If we define the resource type of note to be notes, then the address of a note resource with the identifier 10 has the unique address www.example.com/api/notes/10.

The URL for the entire collection of all note resources is www.example.com/api/notes.

Different operations can be used on the resources. The operation to be executed is defined by the HTTP verb:
![[Pasted image 20240130102210.png]]

This is how we manage to roughly define what REST refers to as a **uniform interface**, which means a consistent way of defining interfaces that makes it possible for system to cooperate.

This way of interpreting REST falls under the second level of RESTful maturity in the Richardson Maturity Model. According to the definition provided by Roy Fielding, we have not defined a REST API. In fact, a large majority of the world's purported "REST" APIs do not meet Fielding's original criteria.

In some places you will see our model for a straightforward CRUD API, being referred to as an example of resource-oriented architecture instead of REST. It's probably better not to get hard stuck on the semantics though.

### Fetching a single resource

Let's expand our application so that it offers a REST interface for operating on individual notes. First, let's create a route for fetching a single resource.

The unique address we will use for an individual note is of the form `notes/10`, where the number a the end refers to the note's unique id number.

We can define parameters for routers in express by using the colon syntax:
![[Pasted image 20240130102753.png]]
Now `app.get('/api/notes/:id', ...)` will handle all HTTP GET requests that are of the form _/api/notes/SOMETHING_, where _SOMETHING_ is an arbitrary string.

The _id_ parameter in the route of a request can be accessed through the [request](http://expressjs.com/en/api.html#req) object:
`const id = request.params.id`
The now familiar `find` method of arrays is used to find the note with an id that matches the parameter. The note is then returned to the sender of the request.

When we visit [http://localhost:3001/api/notes/1](http://localhost:3001/api/notes/1) again in the browser, the console - which is the terminal (in this case) - will display the following:

![terminal displaying 1 then undefined](https://fullstackopen.com/static/7333b6dcc5a6e252178ee0bc4ed16db6/5a190/8.png)

The id parameter from the route is passed to our application but the _find_ method does not find a matching note.

To further our investigation, we also add a console log inside the comparison function passed to the _find_ method. To do this, we have to get rid of the compact arrow function syntax _note => note.id === id_, and use the syntax with an explicit return statement:

```js
app.get('/api/notes/:id', (request, response) => {
  const id = request.params.id
  const note = notes.find(note => {
    console.log(note.id, typeof note.id, id, typeof id, note.id === id)
    return note.id === id
  })
  console.log(note)
  response.json(note)
})
```

When we visit the URL again in the browser, each call to the comparison function prints a few different things to the console. The console output is the following:

1 'number' '1' 'string' false
2 'number' '1' 'string' false
3 'number' '1' 'string' false

The cause of the bug becomes clear. The _id_ variable contains a string '1', whereas the ids of notes are integers. In JavaScript, the "triple equals" comparison === considers all values of different types to not be equal by default, meaning that 1 is not '1'.

Let's fix the issue by changing the id parameter from a string into a [number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number):

```js
app.get('/api/notes/:id', (request, response) => {
  const id = Number(request.params.id)  const note = notes.find(note => note.id === id)
  response.json(note)
})
```

Now fetching an individual resource works.

![api/notes/1 gives a single note as JSON](https://fullstackopen.com/static/aacb793e1b5db50067b3057f79e83253/5a190/9new.png)

However, there's another problem with our application.

If we search for a note with an id that does not exist, the server responds with:

![network tools showing 200 and content-length 0](https://fullstackopen.com/static/71dba69685a59c3d5249303257863366/5a190/10ea.png)

The HTTP status code that is returned is 200, which means that the response succeeded. There is no data sent back with the response, since the value of the _content-length_ header is 0, and the same can be verified from the browser.

The reason for this behavior is that the _note_ variable is set to _undefined_ if no matching note is found. The situation needs to be handled on the server in a better way. If no note is found, the server should respond with the status code [404 not found](https://www.rfc-editor.org/rfc/rfc9110.html#name-404-not-found) instead of 200.

Let's make the following change to our code:
![[Pasted image 20240130104054.png]]

Since no data is attached to the response, we use the [status](http://expressjs.com/en/4x/api.html#res.status) method for setting the status and the [end](http://expressjs.com/en/4x/api.html#res.end) method for responding to the request without sending any data.

The if-condition leverages the fact that all JavaScript objects are [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy), meaning that they evaluate to true in a comparison operation. However, _undefined_ is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) meaning that it will evaluate to false.

Our application works and sends the error status code if no note is found. However, the application doesn't return anything to show to the user, like web applications normally do when we visit a page that does not exist. We do not need to display anything in the browser because REST APIs are interfaces that are intended for programmatic use, and the error status code is all that is needed.

Anyway, it's possible to give a clue about the reason for sending a 404 error by [overriding the default NOT FOUND message](https://stackoverflow.com/questions/14154337/how-to-send-a-custom-http-status-message-in-node-express/36507614#36507614).



### Deleting resources
Deletion happens by making an HTTP DELETE request ot the URL of the resource:

```js
app.delete('/api/notes/:id', (request, response) => {
  const id = Number(request.params.id)
  notes = notes.filter(note => note.id !== id)

  response.status(204).end()
})
```
If deleting the resource is successful, meaning that the note exists and is removed, we respond to the request with the status code [204 no content](https://www.rfc-editor.org/rfc/rfc9110.html#name-204-no-content) and return no data with the response.

There's no consensus on what status code should be returned to a DELETE request if the resource does not exist. The only two options are 204 and 404. For the sake of simplicity, our application will respond with 204 in both cases.



### POST Request
Adding a note happens by making an HTTP POST request to the address http:/localhost:3001/api/notes, and by sending all the information for the new note in the request body in JSON format.

To access the data easily, we need the help of the express json-parser that we can use with the command `app.use(express.json())`

Let's activate the json-parser and implement an initial handler for dealing with the HTTP POST requests:

```js
const express = require('express')
const app = express()

app.use(express.json())
//...

app.post('/api/notes', (request, response) => {  const note = request.body  console.log(note)  response.json(note)})
```
The event handler function can access the data from the _body_ property of the _request_ object.

Without the json-parser, the _body_ property would be undefined. The json-parser takes the JSON data of a request, transforms it into a JavaScript object and then attaches it to the _body_ property of the _request_ object before the route handler is called.

For the time being, the application does not do anything with the received data besides printing it to the console and sending it back in the response.

Before we implement the rest of the application logic, let's verify with Postman that the data is in fact received by the server. In addition to defining the URL and request type in Postman, we also have to define the data sent in the _body_:
### Postman
So how do we test the delete operation? HTTP GET requests are easy to make from the browser. We could write some JavaScript for testing deletion, but writing test code is not always the best solution in every situation.

Many tools exist for making the testing of backends easier. One of these is a command line program [curl](https://curl.haxx.se). However, instead of curl, we will take a look at using [Postman](https://www.postman.com) for testing the application.


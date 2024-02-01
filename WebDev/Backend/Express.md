
Implementing our server code directly with Node's built-in http web server is possible. However ,it is cumbersome, especially once the application grows in size. 

Many libraries have been developed to ease server-side development with Node, by offering a more pleasing interface to work with the built-in http module. These libraries aim to provide a better abstraction for general use cases we usually require to build a backend server. By far the most popular library intended for this purpose is [[Express]].

Express can be defined as a project dependency with the command:
`npm install express`

This also adds it to our `package.json` file:
![[Pasted image 20240126160945.png]]

The source code for the dependency is install in the `node_modules` directory located at the root of the project. 

The versioning model used in npm is called [semantic versioning](https://docs.npmjs.com/getting-started/semantic-versioning).

The caret in the front of _^4.18.2_ means that if and when the dependencies of a project are updated, the version of express that is installed will be at least _4.18.2_. However, the installed version of express can also have a larger _patch_ number (the last number), or a larger _minor_ number (the middle number). The major version of the library indicated by the first _major_ number must be the same.

We can update the dependencies of the project with the command:
![[Pasted image 20240130094239.png]]

If the _major_ number of a dependency does not change, then the newer versions should be [backwards compatible](https://en.wikipedia.org/wiki/Backward_compatibility). This means that if our application happened to use version 4.99.175 of express in the future, then all the code implemented in this part would still have to work without making changes to the code. In contrast, the future 5.0.0 version of express [may contain](https://expressjs.com/en/guide/migrating-5.html) changes that would cause our application to no longer work.


### Simple Express Flow
The following demonstrates a very simple flow to using Express:
![[Pasted image 20240130094856.png]]

Breakdown:
1. At the beginning of our code, we're importing `express`, which this time is a function that is used to create an express application stored in the `app` variable: ![[Pasted image 20240130095108.png]]
2. Next, we define two routes to the application. The first one defines an event handler that is used to handle HTTP GET requests made to the application's /root:
![[Pasted image 20240130095210.png]]
The event handler function accepts two parameters. The first [request](http://expressjs.com/en/4x/api.html#req) parameter contains all of the information of the HTTP request, and the second [response](http://expressjs.com/en/4x/api.html#res) parameter is used to define how the request is responded to.

In our code, the request is answered by using the [send](http://expressjs.com/en/4x/api.html#res.send) method of the _response_ object. Calling the method makes the server respond to the HTTP request by sending a response containing the string `<h1>Hello World!</h1>` that was passed to the _send_ method. Since the parameter is a string, express automatically sets the value of the _Content-Type_ header to be _text/html_. The status code of the response defaults to 200.

We can verify this from the _Network_ tab in developer tools:
![[Pasted image 20240130100142.png]]

3. The second route defines an event handler that handles HTTP GET requests made to the `notes` path of the application:
![[Pasted image 20240130100236.png]]
The request is responded to with the [json](http://expressjs.com/en/4x/api.html#res.json) method of the _response_ object. Calling the method will send the **notes** array that was passed to it as a JSON formatted string. Express automatically sets the _Content-Type_ header with the appropriate value of _application/json_.

![[Pasted image 20240130100435.png]]

Next, let's take a quick look at the data sent in JSON format.

In the earlier version where we were only using Node, we had to transform the data into the JSON format with the `JSON.stringify` method like so:
`response.end(JSON.stringify(notes))`

With express, this is no longer required, because this transformation happens automatically.

It is worth noting that JSON is a string and not a JavaScript object like the value assigned to `notes`. The experiment below illustrate this:
![[Pasted image 20240130100833.png]]


### General Tips
The caret in front of the version number in package.json means that if and when the dependencies of a project are updated, the version of the thing that is installed will be at least the specified number.
![[Pasted image 20240126161249.png]]
Dependencies of a project can be updated with the command:
`npm update`
### npm init
`npm init` initializes the `package.json` file, which holds important information about your project such as:
- Dependencies - dependencies for your project can be found here, and can be installed on projects that you are working on with `npm install`
- Scripts - scripts can be written here to allow the execution of certain actions from the terminal. Generally run by writing `npm` followed by the name of the script

Two ways to run a program directly from the command line:
1. `node index.js` - node followed by the name of the .js file that is named in your package.json file.
2. By creating a script and running `npm` followed by the script name. Ex. `npm start`.

Though either way works, it is customary for npm projects to execute tasks as npm scripts.

### Web Server Module - Building a Simple Web Server

Let's start by editing the `index.js` file as follows:
![[Pasted image 20240126154310.png]]

Once the application is running, the following message is printed to the console:
![[Pasted image 20240126154336.png]]

The application can be viewed in the browser by visiting the address `http://localhost:3001`. The server in its current state will work the same regardless of the latter part of the URL. Ex. `http://localhost:3001/foo/bar` will display the same content.

If port 3001 is already in use by some other application, then the starting server will result in an error message. If this happens, you have two options:
1. Shut down the application using the port (such as an app using json-server).
2. Use a different port for this application.

Let's take a closer look at the first line of code:
![[Pasted image 20240126154822.png]]
In the first row, the application imports Node's build-in web server module.
Node has built-in web server module. 

These days, code that runs in the browser uses ES6 modules. Modules are defined with [[export]] and taken into use with an [[import]].

However, Node.js uses so-called [[CommonJS]] modules. The reason for this is that the Node ecosystem had a need for modules long before JS supported them in the language specification. Node supports now also the use of ES6 modules, but since the support is [not quite perfect](https://nodejs.org/api/esm.html#modules-ecmascript-modules) yet, it's not a bad idea to stick to CommonJS modules.

CommonJS modules function almost exactly like ES6 modules.

The next chunk in our code looks like this:
![[Pasted image 20240126155436.png]]
The code uses the `createServer` method of the http module to create a new web server. An *event handler* is registered to the server that is called every time an HTTP request is made to the server's address `http://localhost:3001`.

The request is responded to with the status code 200, with the `Content-Type` header set to text/plain, and the content of the site to be returned set to `Hello World`.

The last rows bind the http server assigned to the `app` variable, to listen to HTTP requests sent to port 3001:

![[Pasted image 20240126155840.png]]
The primary purpose of the backend server in this part is to offer raw data in JSON format to the frontend. For this reason, let's change our server to return a hardcoded list of notes in the JSON format:

![[Pasted image 20240126160351.png]]

Let's restart the server (you can shut the server down by pressing _Ctrl+C_ in the console) and let's refresh the browser.

The _application/json_ value in the _Content-Type_ header informs the receiver that the data is in the JSON format. The _notes_ array gets transformed into JSON with the _JSON.stringify(notes)_ method.

![[Pasted image 20240126160605.png]]

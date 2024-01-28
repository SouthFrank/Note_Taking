
Implementing our server code directly with Node's built-in http web server is possible. However ,it is cumbersome, especially once the application grows in size. 

Many libraries have been developed to ease server-side development with Node, by offering a more pleasing interface to work with the built-in http module. These libraries aim to provide a better abstraction for general use cases we usually require to build a backend server. By far the most popular library intended for this purpose is [[Express]].

Express can be defined as a project dependency with the command:
`npm install express`

This also adds it to our `package.json` file:
![[Pasted image 20240126160945.png]]

The source code for the dependency is install in the `node_modules` directory located at the root of the project. 
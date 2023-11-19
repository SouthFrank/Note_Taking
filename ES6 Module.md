## Introduction
Separate from the [[module pattern]] that we discussed in other lessons, "modules" is a feature that arrived with ES6. ES6 modules are starting to appear in many code bases around the net and getting them up and running will give us a chance to explore some new parts of the JavaScript ecosystem.

Before we can really use these modules, we're going to have to learn about [[npm]] and [[webpack]], which are both topics that will be very useful beyond these notes. 

Modules themselves are simple to implement, so we're going to take this chance to learn about a few other things.

## JavaScript package managers (npm)
- Starting around 2010, several competing JavaScript package managers emerged to help automate the process of downloading and upgrading libraries from a central repository. [[Bower]] was arguably the most popular in 2013, but eventually was overtaken by [[npm]] around 2015. 
	- It's worth noting that starting around late 2016, [[yarn]] has picked up a lot of traction as an alternative to npm's interface, but it still uses npm packages under the hood.
- npm was originally a package manager made specifically for [[node.js]], a JavaScript runtime designed to run on the server, not the frontend.
	- Using package managers generally involves using a command line, which in the past was never required as a frontend dev. 

## JavaScript module bundlers (webpack)
Most programming languages provide a way to import code from one file to another. As JS was designed to only run in the browser, with no access to the file system of the client's computer (for security reasons), it didn't originally have this feature. So for the longest time, organizing JavaScript code in multiple files required you to load each file with variables shared globally.

In 2009, a project named CommonJS was started with the goal of specifying an ecosystem for JavaScript outside the browser. A big part of CommonJS was its specification for modules, which would finally allow JavaScript to import and export code across files like most programming languages, without resorting to global variables. The most well-known implementation of CommonJS modules is [[node.js]].

node.js as a JavaScript runtime is designed to run on the server. Here's what the earlier example would look like using node.js modules. Instead of loading all of the `moment.min.js` with an HTML script tag, you can load it directly in the JavaScript file as follows:
![[Pasted image 20231119093016.png]]
This is how module loading works in node.js, which is great since node.js is a server side language with access to the computer's file system.

Node.js also knows the location of each npm module path, so instead of having to write `require('./node_module/moment/min/moment.min.js'` you can simply write `require('moment')`.

This is all great for node.js. but if you tried to use the above code in the browser, you'd get an error saying `require` is not define. The browser doesn't have access to the file system, which means loading modules in this way is very tricky (which slows down execution) or asynchronously (which can have timing issues).

This is where a [[module bundler]] comes in. A JavaScript module bundler is a tool that gets around the problem with a build step (which has access to the file system) to create a final output that is browser compatible (which doesn't need access to the file system). In this case, we need a module bundler to find all `require` statements (which is invalid browser JavaScript syntax) and replace them with the actual contents of each required file. The final result is a single bundled JavaScript file (with no require statements)!

Let's take a look at how to use [[webpack]] to get the above `require('moment')` example working in the browser. First we need to install webpack into the project. Webpack itself is an npm package, so we can install it from the command line:
![[Pasted image 20231119100527.png]]
Note that we are installing two packages - webpack and webpack-cli (which enables you to use webpack from the command line). Also note the `--save-dev` argument - this saves it as a development dependency, which means it's a package that you need in your development environment but not on your production server. You can see this reflected in the `package.json` file, which was automatically updated:
![[Pasted image 20231119100703.png]]

## Lesson Overview
#### Explain what npm is and where it was commonly used before being adopted on the frontend.

- npm is the most popular package manager for JavaScript. It allows downloading of packages from a central repository.
- It was originally designed to work with node.js, which was originally designed primarily as a backend tool. However, node.js is now an important part of the web development workflow, even for frontend devs.
#### Describe what `npm init` does and what `package.json` is.

- `npm init` allows you to download packages automatically instead of manually. If you have node.js installed, you already have npm installed.
- You can navigate your command line to the folder you are coding in and enter `npm init`.
	- This will generate a new file name `package.json`. This is a configuration file that npm used to save all project information. With the default contents of `package.json`, it should look something like this:
![[Pasted image 20231118104750.png]]
- The `package.json` file is useful to share with other developers, instead of sharing the whole `node_modules` folder which can get very large.
	- With the `package.json` file, all you have to do to install all required packages is run the command `npm install`.
#### Know how to install packages using npm.

- To install a JavaScript package with npm you use the command (in the command line) `npm install packageName`
	- As of npm 5.0, you no longer need to add --save. npm saves all installed packages as dependencies by defaul.
	- If you want to save a package a development-only dependency, you can so by using the `--save-dev` or `-D` flag.
- When you install a package, two things happen.
	1. The code from the package you installed is added to a folder called `node_modules`.
	2. The `package.json` file is automatically modified to keep track of the project dependencies you have added.
#### Describe what a JavaScript module bundler like webpack is.
- A JavaScript module bundler is a tool that uses a build step (which has access to the file system) to create a final output that is browser compatible (which doesn't need access to the file system).
- A tool that takes multiple JS files and their dependencies, often written in the form of modules, and bundles them together into a single file or a small number of files. The primary goal of a module bundler is to optimize the delivery of JavaScript code to a web browser by reducing the number of HTTP requests required to load a page. 
	- JS modules allow devs to organize their code into reusable and maintainable units. In a web environment, loading many individual files can lead to performance issues due to the overhead of multiple HTTP requests.
	- Module bundlers help address this issues by combining all necessary modules into a single file or a few files. This can reduce the number of network requests and improve the loading time of web pages. Additionally, module bundlers often include features such as code minification and tree shaking, which further optimize the size of the bundled code by removing unused or redundant portions.
		- Side note: [[tree shaking]] is a technique used in JS module bundlers to eliminate dead (unused or unreachable) code from the final bundled output. The term "tree shaking" comes from the concept of shaking a tree to make dead leaves fall, leaving only the necessary ones.
#### Explain what the concepts "entry" and "output" mean as relates to webpack.
#### Briefly explain what a development dependency is.
#### Explain what "transpiling code" means and how it relates to front-end development.
#### Briefly describe what a task runner is an how it's used in front-end development.
#### Describe how to write an npm automation script.
#### Explain one of the main benefits of writing code in modules.
#### Explain "named" exports and "default" exports.

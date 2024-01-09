
#### Module Bundlers
- [[Browserify]] - released in 2011 and pioneered the usage of node.js style require statements on the frontend (which is essentially what enabled npm to become the frontend package manager of choice).
- [[Webpack]] - around 2015, [[webpack]] eventually became the more widely used module bundler (fueled by the popularity of the [[React]] frontend framework, which took full advantage of the webpack's various features).
	- Can handle not only JS, but also other assets like CSS, images, and more. Powerful and flexible configuration system.
- [[Parcel]] - A zero-configuration bundler that simplifies the process of setting up and using a bundler. It supports various types of assets out of the box and requires minimal configuration.
- [[Rollup]] - Known for its focus on creating smaller, more efficient bundles. Rollup is often used for libraries and packages that are intended to be distributed for consumption by other developers.

#### Transpilers

##### JavaScript
- [[Babel]]:
	- Languages transpiled: JavaScript (ECMAScript) to JavaScript.
	- Use Case: Babel is a widely used transpiler for converting modern ECMAScript 6+ (ES6+) code into ES5, which is compatible with all browsers.
- [[TypeScript]]:
	- Languages transpiled: TypeScript to JavaScript
	- Use Case: TypeScript is a superset of JavaScript that adds static typing. It is transpiled into plain JavaScript, making it compatible with all browsers.
- [[CoffeeScript]]:
	- Languages transpiled: CoffeeScript to JavaScript
	- Use Case: CoffeeScript is a language that compiles into JavaScript. It provides a more concise syntax with some additional features and is often used to improve readability.
- [[Elm]]:
	- Languages transpiled: Elm to JavaScript
	- Use Case: Elm is a functional programming language that compiles to JavaScript. It is often used for building web front-end applications.
- [[Flow]]:
	- Languages transpiled: Flow to JavaScript
	- Use Case: Flow is a static type checker for JavaScript. While it's not a full transpiler, it can be used in conjunction with Babel to add static typing to JavaScript.
- [[Closure Compiler]]:
	- Languages transpiled: ECMAScript to optimized JavaScript
	- Use Case: Closure Compiler, developed by Google, is a tool that compiles JavaScript into a more compact and optimized form, helping to improve performance and reduce file size.

##### CSS
- [[Sass]] (Synactically Awesome Stylesheets):
	- Language transpiled: Sass to CSS
	- Use Case: Sass is a preprocessor scripting language that is interpreted or compiled into CSS. It adds features like variables, nested rules, and mixings to CSS.
- [[Less]]:
	- Language transpiled: Less to CSS
	- Use Case: Similar to Sass, Less is a CSS preprocessor that is transpiled into standard CSS. It includes features like variables, nesting, and functions.

#### Task runners
- npm
	- Nowadays the most popular choice for a task runner is using the scripting capabilities built into the npm package manager itself, which doesn't use plugins but instead works with other command line tools directly.
- Grunt
	- In 2013, Grunt was the most popular task runner.
- Gulp
	- Followed shortly after Grunt.

#### Package Managers
- [[npm]]:
	- npm (node package manager), is undoubtedly the most popular package manager right now.
	- It is used for both server-side and client-side (front end) JavaScript projects.
	- Key features: large package registry, dependency management, and script running.
- [[Yarn]]:
	- The second most popular package manager, used as an alternative to npm. It was created by Facebook and is designed to be fast, reliable, and secure. Yarn uses a deterministic dependency resolution algorithm.
	- Key features: Deterministic installs, offline capabilities, and improved performance.
- [[Bower]]:
	- Bower was historically popular for managing front-end components, such as JavaScript libraries and CSS frameworks. However, it is considered somewhat legacy, and its usage has decreased with the rise of npm and Yarn.
	- Key features: Front-end package management, versioning, and asset downloading.

#### Vite
- Vite is a local development server made by the creator of [[Vue.js]], and it is used by default by Vue and for React project templates.
- Has support for TypeScript and JSX.
- Focuses on speed and performance.
- Consists of two major parts:
	- A development server that provides rich feature enhancements over native ES modules: fast Hot Module Replacement (HMR), pre-bundling, support for TypeScript, JSX, and dynamic import.
	- A build command that bundles your code with [[Rollup]], pre-configured to output optimized static assets for production.


#### JSON Server
- A tool used in development that can act as your server.
- Global install:
	- `npm install -g json-server`
- Runs on port 3000 by default
	- Alternate port can be defined using `json-server --port 3001 --watch db.json`
- A global installation is not necessary, it can be run from the root directory of your app using the command npm, `npx json-server --port 3001 --watch db.jso`
- Requires all data to be sent in JSON format. What this means in practice is that the data must be a correctly formatted string and that the quest must contain the `Content-Type` request header with the value `application/json`.
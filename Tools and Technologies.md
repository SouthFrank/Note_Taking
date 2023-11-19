
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
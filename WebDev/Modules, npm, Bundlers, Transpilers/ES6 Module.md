## Introduction
Separate from the [[module pattern]] that we discussed in other lessons, "modules" is a feature that arrived with ES6. ES6 modules are starting to appear in many code bases around the net and getting them up and running will give us a chance to explore some new parts of the JavaScript ecosystem.

Before we can really use these modules, we're going to have to learn about [[npm]] and [[webpack]], which are both topics that will be very useful beyond these notes. 

Modules themselves are simple to implement, so we're going to take this chance to learn about a few other things.

## JavaScript package managers
- Starting around 2010, several competing JavaScript package managers emerged to help automate the process of downloading and upgrading libraries from a central repository. [[Bower]] was arguably the most popular in 2013, but eventually was overtaken by [[npm]] around 2015. 
	- It's worth noting that starting around late 2016, [[yarn]] has picked up a lot of traction as an alternative to npm's interface, but it still uses npm packages under the hood.
- npm was originally a package manager made specifically for [[node.js]], a JavaScript runtime designed to run on the server, not the frontend.
	- Using package managers generally involves using a command line, which in the past was never required as a frontend dev. 
## npm (node package manager)

### Introduction

The node package manager is a command-line tool that gives you access to a gigantic repository of plugins, libraries and tools. npm is the world's largest software registry. Open source developers from every continent use npm to share and borrow packages, and many organizations use npm to manage private development as well.

npm consists of three distinct components:
- the website
- the Command Line Interface (CLI)
- the registry

Use the website to discover packages, set up profiles, and manage other aspects of your npm experience. For example, you can set up organizations to manage access to public or private packages.

The CLI runs from a terminal, and is how most developers interact with npm.

The registry is a large public database of JavaScript software and the meta-information surrounding it.

### Downloading and Installing Packages Locally

You can install a package locally if you want to depend on the package from your own module, using something Node.js `require`. This is `npm install`'s default behavior.

#### Scopes and package visibility
- Unscoped packages are always public.
- [Private packages](https://docs.npmjs.com/about-private-packages) are always scoped.
- Scoped packages are private by default; you must pass a command-line flag when publishing to make them public.
#### Installing an unscoped package
Unscoped packages are always public, which means they can be searched for, downloaded, and installed by anyone. To install a public package, on the command line, run `npm install <package name>`. This will create the `node_modules` directory in your current directory (if one doesn't exist yet) and will download the package to that directory.

#### Installing a scoped package
Scoped public packages can be downloaded and installed by anyone, as long as the scope name is referenced during installion:
`npm install  @scope/package-name`

#### Installing a private package
Private packages can only be downloaded and installed by those who have been granted read access to the package. Since private packages are always scoped, you must reference the scope name during installion:
`npm install @scope/private-package-name`

#### Testing package installation
To confirm that `npm install` worked correctly, in your module directory, check that a `node_modules` directory exists and that it contains a directory for the packages you installed:
`ls node_modules`

#### Installing a package with dist-tags
Like `npm publish`, `npm install <package_name>` will use the latest tag by default. To override this behavior, use `npm install <package_name><@tag>`. For example, to install the `example-package` at the version tagged with `beta`, you would run the following command:
`npm install example-package@beta`

## JavaScript module bundlers (webpack)
Most programming languages provide a way to import code from one file to another. As JS was designed to only run in the browser, with no access to the file system of the client's computer (for security reasons), it didn't originally have this feature. So for the longest time, organizing JavaScript code in multiple files required you to load each file with variables shared globally.

In 2009, a project named CommonJS was started with the goal of specifying an ecosystem for JavaScript outside the browser. A big part of CommonJS was its specification for modules, which would finally allow JavaScript to import and export code across files like most programming languages, without resorting to global variables. The most well-known implementation of CommonJS modules is [[node.js]].

node.js as a JavaScript runtime is designed to run on the server. Here's what the earlier example would look like using node.js modules. Instead of loading all of the `moment.min.js` with an HTML script tag, you can load it directly in the JavaScript file as follows:
![[Pasted image 20231119093016.png]]
This is how module loading works in node.js, which is great since node.js is a server side language with access to the computer's file system.

Node.js also knows the location of each npm module path, so instead of having to write `require('./node_module/moment/min/moment.min.js'` you can simply write `require('moment')`.

This is all great for node.js. but if you tried to use the above code in the browser, you'd get an error saying `require` is not define. The browser doesn't have access to the file system, which means loading modules in this way is very tricky (which slows down execution) or asynchronously (which can have timing issues).

This is where a [[module bundler]] comes in. A JavaScript module bundler is a tool that gets around the problem with a build step (which has access to the file system) to create a final output that is browser compatible (which doesn't need access to the file system). In this case, we need a module bundler to find all `require` statements (which is invalid browser JavaScript syntax) and replace them with the actual contents of each required file. The final result is a single bundled JavaScript file (with no require statements)!

### Webpack Workflow

Let's take a look at how to use [[webpack]] to get the above `require('moment')` example working in the browser. First we need to install webpack into the project. Webpack itself is an npm package, so we can install it from the command line:
![[Pasted image 20231119100527.png]]
Note that we are installing two packages - webpack and webpack-cli (which enables you to use webpack from the command line). Also note the `--save-dev` argument - this saves it as a development dependency, which means it's a package that you need in your development environment but not on your production server. You can see this reflected in the `package.json` file, which was automatically updated:
![[Pasted image 20231119100703.png]]
Now we have webpack and webpack-cli installed as packages in the `node_modules` folder. You can use webpack-cli from the command line as follows:
![[Pasted image 20231119114237.png]]
This command will run the webpack tool that was installed in the `node_modules` folder, start with the index.js file, find any `require` statements, and replace them with the appropriate code to create a single output file (which by default is `dist/main.js`). The `--mode=development` argument is to keep the JavaScript readable for developers, as opposed to a minified output with the argument `--mode=production`.

Now that we have webpack's `dist/main.js` output, we are going to use it instead of `index.js` in the browser, as it contains invalid require statements. This would be reflect in the `index.html` file as follow:
![[Pasted image 20231119114845.png]]
If you refresh the browser, you should see that everything is working as before!

Note that we'll need to run the webpack command each time we change `index.js`. This is tedious, and will get even more tedious as we use webpack's more advanced features (like generating source maps to help debug the original code from the transpiled code). Webpack can read options from a config file in the root directory of the project name `webpack.config.js`, which in our case would look like:
![[Pasted image 20231119115050.png]]
Now each time we change `index.js`, we can run webpack with the command:
![[Pasted image 20231119115119.png]]
We don't need to specify the `index.js` and `--mode=development` options anymore, since webpack is loading those options from the `webpack.config.js` file. This is better, but it's still tedious to enter this command for each code change - we'll make this process smoother in a bit.

- Overall this may not seem like much, but there are some huge advantages to this workflow. We are no longer loading external scripts via global variables. Any new JavaScript libraries will be added using `require` statements in the JavaScript, as opposed to adding new `<script>` tags in the HTML. Having a single JavaScript bundle file is often better for performance. And now that we added a build step, there are some other powerful features we can add to our development workflow!

![[Pasted image 20231119115456.png]]


## Webpack Workflow Tutorial
First, create a directory, initialize npm, install webpack locally, and install the `webpack-cli` (the tool used to run webpack on the command line):
![[Pasted image 20231124104725.png]]
![[Pasted image 20231124104932.png]]
We also need to adjust our `package.json` file in order to make sure we mark our package as `private`, as well as removing the `main` entry. This is to prevent an accidental publish of your code.
![[Pasted image 20231124105130.png]]
In this example, there are implicit dependencies between the `<script>` tags. Our `index.js` file depends on `lodash` being included in the page before it runs. This is because `index.js` never explicitly declared a need for `lodash`; it assumes that the global variable `__` exists.

There are problems with managing JavaScript projects this way:
- It is not immediately apparent that the script depends on an external library.
- If a dependency is missing, or included in the wrong order, the application will not function properly.
- If a dependency is included but not used, the browser will be forced to download unnecessary code.

Let's use `webpack` to manage these scripts instead.
#### Creating a Bundle
First we'll tweak our directory structure slightly, separating the "source" code (`./src`) from our "distribution" code (`./dist`). The "source" code is the code that we'll write and edit. The "distribution" code is the minimized and optimized `output` of our build process that will eventually be loaded in the browser. Tweak the directory structure as follows:

![[Pasted image 20231124105733.png]]
![[Pasted image 20231124105744.png]]
To bundle the `lodash` dependency with `index.js`, we'll need to install the library locally:
`npm install --save lodash`
![[Pasted image 20231124110015.png]]
Now let's import `lodash` in our script in the `src/index.js` file:
![[Pasted image 20231124110136.png]]
Now since we'll be bundling our scripts, we have to update our `index.html` file. Let's remove the lodash `<script>`, as we now `import` it, and modify the other `<script>` tag to load the bundle, instead of the raw `./src` file:
![[Pasted image 20231124110324.png]]
In this setup, `index.js` explicitly requires `lodash` to be present, and binds it as `_` (no global scope pollution). By stating what dependencies a module needs, webpack can use this information to build a dependency graph. It then uses the graph to generate an optimized bundle where scripts will be executed in the correct order.

With that said, let's run `npx webpack`, which will take our script at `src/index.js` as the entry point, and will generate `dist/main.js` as the output. The `npx` command, which ships with Node 8.2/npm 5.2.0 or higher, runs the webpack binary (`./node_modules/.bin/webpack`) of the webpack package we installed in the beginning:
![[Pasted image 20231124110816.png]]
**TIP: Your output may vary, but if the build is successful then you are good to go**

#### Modules
The `import` and `export` statements have been standardized in ES2015. They are supported in most of the browsers at the moment, however there are some browsers that don't recognize the new syntax. But don't worry, webpack does support them out of the box.

Behind the scenes, webpack actually "[[transpiles]]" the code so that older browsers can also run it. If you inspect `dist/main.js`, you might be able to see how webpack does this, it's quite ingenious! Besides `import` and `export`, webpack supports various other module syntaxes as well, see [Module API](https://webpack.js.org/api/module-methods) for more information.

#### Using a Configuration
As of version 4, webpack doesn't require any configuration, but most projects will need a more complex setup, which is why webpack supports a configuration file. This is much more efficient than having to manually type a lot of commands in the terminal, so let's create one:
![[Pasted image 20231124111319.png]]
A configuration file allows far more flexibility than CLI usage. We can specify loader rules, plugins, resolve options and many other enhancements this way.

#### NPM Scripts
Given it's not particularly fun to run a local copy of webpack from the CLI, we can set up a little shortcut. Let's adjust our `package.json` by adding an npm script:
![[Pasted image 20231124111819.png]]
Now the `npm run build` command can be used in place of the `npx` command we used earlier. Note that within `scripts` we can reference locally installed npm packages by name the same way we did with `npx`. This convention is the standard in most npm-based projects because it allows all contributors to use the same set of common scripts.

Now run the following command and see if your script alias works:
![[Pasted image 20231124112039.png]]

#### Conclusion
Now that you have a basic build together you should move on to the next guide [`Asset Management`](https://webpack.js.org/guides/asset-management) to learn how to manage assets like images and fonts with webpack. At this point, your project should look like this:

![[Pasted image 20231124112114.png]]

## Transpiling code for new language features (babel)

Transpiling code means converting the code in one language to code in another similar language. This is an important part of frontend development — since browsers are slow to add new features, new languages were created with experimental features that transpile to browser compatible languages.

For CSS, there's [[Sass]], [[Less]], and [[Stylus]], to name a few. 
For JavaScript, the most popular transpiler for awhile was CoffeeScript (released around 2010), whereas nowadays most people use [[babel]] or [[TypeScript]].

[[CoffeeScript]] is a language focused on improving JavaScript by significantly changing the language - optional parentheses, significant whitespace, etc. 
[[Babel]] is not a new language but a transpiler that transpiles next generation JavaScript with features not yet available to all browsers (ES2015 and beyond) to older more compatible JavaScript (ES5).
[[TypeScript]] is a language that is essentially identical to next generation JavaScript, but also adds optional static typic. Many people choose to use [[babel]] because it's the closest to Vanilla JavaScript.

Let's look at an example of how to use babel with our existing webpack build step. First we'll install babel (which is an npm package) into the project from the command line:
![[Pasted image 20231119162538.png]]
Note that we're installing 3 separate packages as dev dependencies:
1. `@babel/core` is the main part of babel
2. `@babel/preset-env` is a preset defining which new JavaScript features to transpile
3. `@babel-loader` is a package to enable babel to work with webpack

We can configure webpack to use `babel-loader` by editing the `webpack.config.js` file as follows:
![[Pasted image 20231119162758.png]]
This syntax looks confusing, but fortunately it's not something we'll be editing often. Basically, we are telling webpack to look for any .js files (excluding ones in the `node_modules` folder) and apply babel transpilation using `babel-loader` with the `@babel/preset-env` preset. 

Now that everything's set up, we can start writing ES2015 features in our JavaScript. Here's an example of an ES2015 template string in the `index.js` file:
![[Pasted image 20231119164151.png]]
We can also use the ES2015 import statement instead of `require` for loading modules, which is what you'll see in a lot of codebases today:
![[Pasted image 20231119164242.png]]
In this example, the `import` syntax isn't much different from the `require` syntax, but `import` has extra flexibility for more advanced cases. Since we changed `index.js`, we need to run webpack again in the command line:
![[Pasted image 20231119164345.png]]
While this particular example may not be too exciting, the ability to transpile code is a very powerful one.

If we're concerned about performance, we should be [[minifying]] the bundle file, which should be easy enough since we're already incorporating a build step. We also need to re-run the webpack command each time we change the JavaScript, which gets old quickly. So the next thing we'll look at are some convenience tools to solve these issues.

## Using a task runner (npm scripts)
Now that we’re invested in using a build step to work with JavaScript modules, it makes sense to use a task runner, which is a tool that automates different parts of the build process. For frontend development, tasks include minifying code, optimizing images, running tests, etc.

Let's write some npm scripts to make using webpack easier. This involves simply changing the `package.json` file as follows:
![[Pasted image 20231119165134.png]]
Here we've added two new scripts, `build` and `watch`. To run the build script, you can enter in the command line:
![[Pasted image 20231119165216.png]]
This will run webpack (using configuration from the `webpack.config.js` we made earlier) with the `--progress` option to show the percent progress and the `--mode=production` option to minimize the code for production. To run the `watch` script:
![[Pasted image 20231119165351.png]]
This uses the `--watch` option instead to automatically re-run webpack each time any JavaScript file changes, which is great for development.

Note that scripts in `package.json` can run webpack without having to specify the full path, since node.js knows the location of each npm module path. 
We can make things even sweeter by installing webpack-dev-server, a separate tool which provides a simple web server with live reloading. To install it as a development dependency, enter the command:
![[Pasted image 20231119165557.png]]
Then add an npm script to `package.json`:
![[Pasted image 20231119165618.png]]
Now you can start your derv server by running the command:
![[Pasted image 20231119165640.png]]
This will automatically open the `index.html` website in your browser with an address of `localhost:8080` (by default). Any time you change your JavaScript in `index.js`, webpack-dev-server will rebuild its own bundled JavaScript and refresh the browser automatically. This is a useful time saver, as it allows you to keep your focus on the code instead of having to continually switch contexts between the code and the browser to see new changes.

This is only scratching the surface, there are plenty more options with both webpack and webpack-dev-server (which you can read about [here](https://webpack.js.org/guides/development/)). You can of course make npm scripts for running other tasks as well, such as converting Sass to CSS, compressing images, running tests — anything that has a command line tool is fair game.

## ES6 Modules
Now that we understand what webpack is doing it's time to discuss the module syntax. There are only 2 components to it - `import` and `export`.

The import statement is the same thing that you used during the webpack tutorial so it should be familiar:
![[Pasted image 20231126111123.png]]
There are many benefits to writing your code in modules. One of the most compelling is code reuse. If, for instance, you have written some functions that manipulate the DOM in a specific way, putting all of those into their own file as a "module" means that you can copy that file and reuse it very easily!

- With the introduction of ES6 modules, the module pattern (IIFEs) is not needed anymore, though you might still encounter them in the wild. When using ES6 modules, only what is exported can be accessed in other modules by importing. Additionally, any declarations made in a module are not automatically added to the global scope. By using ES6 modules, you can keep different parts of your code cleanly separated, which makes writing and maintaining your code much easier and less error-prone. Keep in mind that you can definitely export constructors, classes, and factory functions from your modules.

To pull it all together, let's write a simple module and then include it in our code. We are going to continue from where the webpack tutorial left off. Before beginning, your file directory should look something like this:
![[Pasted image 20231126111651.png]]

There are two different ways to use exports in your code: named exports and default exports. Which option you use depends on what you are exporting. Take a moment to look at the [MDN documentation about the export declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) and the [MDN documentation about the import declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) which give great examples for the different syntax on import and export.

#### exports

**Named exports**
Every module can have two different types of export, `named export` and `default export`. You can have multiple named exports per module but only one default export. 
![[Pasted image 20231126112559.png]]
After the `export` keyword, you can use let, const, and var declarations, as well as function or class declarations. You can also use the `export{ name1, name2 }` syntax to export a list of names declared elsewhere. Note that `export{}` does not export an empty object - it's a no-op declaration that exports nothing (an empty name list).

Export declarations are not subject to `temporal dead zone` rules. You can declare that module exports `x` before the name `x` itself is declared.
![[Pasted image 20231126112927.png]]
**Default exports**
![[Pasted image 20231126113002.png]]
The `export default` syntax allows any expression.
![[Pasted image 20231126113026.png]]
As a special case, functions and classes are exported as declarations, not expressions, and these declarations can be anonymous. This means functions will be hoisted.
![[Pasted image 20231126113148.png]]

Named exports are useful when you need to export several values. When importing this module, named exports must be referred to by the exact same name (optionally renaming it was `as`), but the default export can be imported with any name. For example:
![[Pasted image 20231126113338.png]]
![[Pasted image 20231126113408.png]]

#### imports

`import` declarations can only be present in modules, and only at the top-level (i.e. not inside blocks, functions, etc.). If an `import` declaration is encountered in non-module contexts (for example, `<script>` tags without `type="module"`, `eval`, `new Function`, which all have "script" or "function body" as parsing goals), a `SyntaxError` is thrown. To load modules in non-module contexts, use the [dynamic import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import) syntax instead.

All imported bindings cannot be in the same scope as any other declaration, including `let`, `const`, `class`, `function`, `var`, and `import` declaration.

`import` declarations are designed to be syntactically rigid (for example, only string literal specifiers, only permitted at the top-level, all bindings must be identifiers), which allows modules to be statically analyzed and linked before getting evaluated. This is the key to making modules asynchronous by nature, powering features like [top-level await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules#top_level_await).

**Forms of import declarations**
There are four forms of `import` declarations:
- Named import: `import ( export1, export2 } from "module-name";`
- Default import: `import defaultExport from "module-name";`
- Namespace import: `import * as name from "module-name";`
- Side effect import: `import "module-name"`

**Name import**
Given a value named `myExport` which has been exported from the module `my-module` either implicitly as `export * from "another.js"` or explicitly using the `export` statement, this inserts `myExport` into the current scope.
![[Pasted image 20231126114317.png]]

**Default import**
Default exports need to be imported with the corresponding default import syntax. This simplest version directly imports the default:
![[Pasted image 20231126114554.png]]
Sin the default export doesn't explicitly specify a name, you can give the identifier any name you like.

It is also possible to specify a default import with the namespace imports or named imports. In such cases, the default import will have to be declared first. For instance:
![[Pasted image 20231126114806.png]]

**Namespace import**
![[Pasted image 20231126114934.png]]

**Side effect import**
![[Pasted image 20231126115047.png]]




## Conclusion
So this is modern JavaScript in a nutshell. We went from plain HTML and JS to using **a package manager** to automatically download 3rd party packages, **a module bundler** to create a single script file, a **transpiler** to use future JavaScript features, and **a task runner** to automate different parts of the build process. Definitely a lot of moving pieces here, especially for beginners. Web development used to be a great entry point for people new to programming precisely because it was so easy to get up and running; nowadays it can be quite daunting, especially because the various tools tend to change rapidly.

Still, it’s not as bad as it seems. Things are settling down, particularly with the adoption of the node ecosystem as a viable way to work with the frontend. It’s nice and consistent to use npm as a package manager, node `require` or `import` statements for modules, and npm scripts for running tasks. This is a vastly simplified workflow compared to even a year or two ago!

Even better for beginners and experienced developers alike is that frameworks these days often come with tools to make the process easier to get started. Ember has [`ember-cli`](https://ember-cli.com/), which was hugely influential on Angular’s [`angular-cli`](https://cli.angular.io/), React’s [`create-react-app`](https://github.com/facebookincubator/create-react-app), Vue’s [`vue-cli`](https://github.com/vuejs/vue-cli), etc. All these tools will set up a project with everything you need — all you need to do is start writing code. However, these tools aren’t magic, they simply set everything up in a consistent and working fashion — you may often get to a point where you need to do some extra configuration with webpack, babel, etc. So it’s still very critical to understand what each piece does as we’ve covered in this article.

Modern JavaScript can definitely be frustrating to work with as it continues to change and evolve at a rapid pace. But even though it may seem at times like re-inventing the wheel, JavaScript’s rapid evolution has helped push innovations such as hot reloading, real-time linting, and time-travel debugging. It’s an exciting time to be a developer, and I hope this information can serve as a roadmap to help you on your journey!
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

Webpack looks for an entry .js file, usually in the `src` directory. It then takes the code, imports, etc. and "outputs" them into a .js file located in the `dist` directory. This is the file that is linked in your html script.
#### Briefly explain what a development dependency is.
- A "development dependency" refers to a software package or library that is necessary for the development and build process of a project but is not required for the runtime execution of the application. These dependencies are tools, libraries, or modules that assist developers during the development phase, such as in building, testing and maintaining a codebase.
- When someone is working on a project, they install both regular dependencies and development dependencies. However, when the application is deployed or run in a production environment, only the regular dependencies are typically installed.

#### Common examples of development dependencies
1. Build Tools:
	- Module bundlers like Webpack, Rollup, or Parcel.
	- Task runners like Gulp or Grunt.
	- Transpilers like Babel (when used for development purposes).
2. Testing Libraries:
    - Testing frameworks like Jest, Mocha, or Jasmine.
    - Assertion libraries like Chai.
3. Linters:
    - Code quality tools like ESLint or TSLint.
4. Mocking Libraries:
    - Libraries for mocking data or APIs during development, such as json-server or Mirage.js.
5. Development Servers:
    - Local development servers like webpack-dev-server or Express.js (when used for development purposes).
6. Documentation Tools:
    - Documentation generators like JSDoc or tools for generating API documentation.
#### Explain what "transpiling code" means and how it relates to front-end development.
- Transpiling code means converting the code in one language to code in another similar language. This is an important part of frontend development - since browsers are slow to add new features, new languages were created with experimental features that transpile to browser compatible languages.
#### Briefly describe what a task runner is an how it's used in front-end development.
- A task runner is a tool that automates different parts of the build process. 
- For frontend development, tasks include minifying code, optimizing images, running tests, etc.
- In 2013, Grunt was the most popular frontend task runner, with Gulp following shortly after. Both rely on plugins that wrap other command line tools. Nowadays the most popular choice seems to be using the scripting capabilities built into the npm package manager itself, which doesn't use plugins but instead works with other command line tools directly.
#### Describe how to write an npm automation script.
- The script has to be added to the `package.json` file, then it can be run from the command line. For example, `npm run build`.
#### Explain one of the main benefits of writing code in modules.
Code reuse! If you have some functions that do something specific, you can put those all into their own file as a "module". It can then be copied and reused very easily.

There are also the same benefits as when using factory functions or the module pattern (the module pattern and ES6 modules are not the same thing; this naming convention is very frustrating).
#### Explain "named" exports and "default" exports.


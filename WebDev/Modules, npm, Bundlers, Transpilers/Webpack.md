Webpack is the go-to tool across the web for bundling and compiling JavaScript code. There are other options but at this time none of them are as popular or widely used as webpack.

While bundling modules is a key feature of webpack, there are other amazing features as well. Another amazing feature is webpack's ability to process and manipulate your code as it bundle. So, for example, if you would like to use [[Sass]] or [[PostCSS]] to write your CSS, webpack can allow you to do that. Webpack can manage your images and compress and optimize them for use on the web. Webpack can minify and uglify your code. 

There are tons of things webpack can do, but to access these functions we need to learn more about loaders and plugins.

**Bundling**

If you give webpack a file as an entry point, it will build a dependencyu graph based on all the imports/exports starting there, before bundling into a single `.js` file in `dist`. If you needed to output multiple bundles (e.g. multiple html pages that each need their own), then each entry point you give Webpack will produce its own output bundle.

If you are only dealing with bundling JS, then this is straightforward. But what if you project includes CSS or assets like images or fonts? For CSS, you can import you `.css` file directly into your JS and for assets like images, they might be used inside your CSS or imported directly into your JS. When you tell Webpack to bundle your files, it will come across these files and try to bundle them together or process any assets like images and copy them into `dist`.

Since these sorts of files are not JS, Webpack will not know how to process them unless you tell it how by including the correct loaders and rules. If you really wanted to, with the right loaders/plugins/rules, you could even do things such as image optimization when you build your project into `dist`. 

## Plugins and Loaders

#### Html-webpack-plugin

Since we would like to keep all of our development work within `src` and leave `dist` for the production build (the code that you will actually deploy), what about handling HTML files?

Similarly to how we will need loaders and rules for CSS and assets, we can use a plugin called `html-webpack-plugin` which will automatically build an HTML file in `dist` for us when we build our project. It will then also automatically add certain things to HTML like our output bundle in a `<script>` tag, or the code to use a favicon if we configured it to use one.

By default, it will create this from a blank template, so the resulting HTML file will essentially be the usual boilerplate with our script and perhaps any other options we add in the configuration. If we had our own `dist/index.html` then it would be overwritten! In order to preserve our own HTML, we can tell it to use a template and provide a path to our own HTML file that is in `src`. 

An example of how to set the template option within your webpack configuration file:
![[Pasted image 20231126163048.png]]

#### Loading CSS
![[Pasted image 20231127114247.png]]
Module loaders can be chained. Each loader in the chain applies transformations to the processed resource. A chain is executed in reverse order. The first loader passes its results (resource with applied transformations) to the next one, and so forth. Finally, webpack expects JavaScript to be returned by the last loader in the chain.

The above order of loaders should be maintained: `style-loader` comes first and followed by `css-loader`. If this convention is not followed, webpack is likely to throw errors.
![[Pasted image 20231127114713.png]]
This enables you to `import './style.css'` into the file that depends on that styling. Now, when that module is run, a `<style>` tag with the stringified css will be inserted into the `<head>` of your html file.

Note that you can, and in most cases should, [minimize css](https://webpack.js.org/plugins/mini-css-extract-plugin/#minimizing-for-production) for better load times in production. On top of that, loaders exist for pretty much any flavor of CSS you can think of – [postcss](https://webpack.js.org/loaders/postcss-loader), [sass](https://webpack.js.org/loaders/sass-loader), and [less](https://webpack.js.org/loaders/less-loader) to name a few.
#### Loading Images
So now we're pulling in our CSS, but what about our images like backgrounds and icons? As of webpack 5, using the built-in [Asset Modules](https://webpack.js.org/guides/asset-modules/) we can easily incorporate those in our system as well:
![[Pasted image 20231127120404.png]]
Now, when you `import MyImage from './my-image.png'`, that image will be processed and added to your `output` directory _and_ the `MyImage` variable will contain the final url of that image after processing. When using the [css-loader](https://webpack.js.org/loaders/css-loader), as shown above, a similar process will occur for `url('./my-image.png')` within your CSS. The loader will recognize this is a local file, and replace the `'./my-image.png'` path with the final path to the image in your `output` directory. The [html-loader](https://webpack.js.org/loaders/html-loader) handles `<img src="./my-image.png" />` in the same manner.

Let's add an image to our project and see how this works, you can use any image you like:


#### Development
**Source Maps**
When webpack bundles your source code, it can be difficult to track down errors and warnings to its original location. In order to make it easier to track down errors and warnings, JS offers [[source maps]], which map your compiled code back to your original source code.

There are a lot of [different options](https://webpack.js.org/configuration/devtool) available when it comes to source maps. Be sure to check them out so you can configure them to your needs.

![[Pasted image 20231127130906.png]]
![[Pasted image 20231127130932.png]]

**Choosing a Development Tool**

It quickly becomes a hassle to manually run `npm run build` every time you want to compile your code.

There are a couple different options available in webpack that help automatically compile your code whenever it changes:
1. webpack's [Watch Mode](https://webpack.js.org/configuration/watch/#watch)
2. [webpack-dev-server](https://github.com/webpack/webpack-dev-server)
3. [webpack-dev-middleware](https://github.com/webpack/webpack-dev-middleware)

![[Pasted image 20231127131203.png]]
![[Pasted image 20231127131225.png]]

![[Pasted image 20231127131303.png]]
![[Pasted image 20231127131336.png]]
![[Pasted image 20231127131442.png]]

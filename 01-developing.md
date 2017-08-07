# Developing

1. [Getting Started](#getting-started)
2. [Automatic Browser Refresh](#automatic-browser-refresh)

## Getting Started

Book: Node 6, trying to do Node 8.

### Setting up the project

```
$ mkdir webpack-demo
$ cd webpack-demo
$ npm init -y
```

The `-y` option generates `package.json` and skip for more control.

### Installing webpack

You could install webpack globally, but it's a good idea to be able to control the webpack version and use it in CI (continuous integration) setups as well.

```
$ npm install webpack --save-dev
```

### Executing webpack

Display the path to the executables:
```
$ npm bin
```

Create a file `app/index.js` with a `console.log('Hello world')` inside and then run:
```
$ node_modules/.bin/webpack app/index.js build/index.js
```

This will run webpack with entry `app/index.js` and output `build/index.js`.

### Directory Structure

* app/
  * index.js
  * component.js
* build/
* package.json
* webpack.config.js

### Setting up assets

app/component.js
```javascript
export default (text = 'Hello world') => {
  const element = document.createElement('div');
  element.innerHTML = text;
  return element;
};
```

app.index.js
```javascript
import component from './component';
document.body.appendChild(component());
```

### Setting up webpack configuration

Webpack and its development server can automatically find `webpack.config.js` file.

We are going to use html-webpack-plugin to generate a index.html file for the application and add the bundled scripts in it to run.

```
$ npm install html-webpack-plugin --save-dev
```

The minimum you need in a webpack.config.js file, is the values for entry and output.

webpack.config.js
```javascript
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

const PATHS = {
  app: path.join(__dirname, 'app'),
  build: path.join(__dirname, 'build')
};

module.exports = {
  entry: {
    app: PATHS.app,
  },
  output: {
    path: PATHS.build,
    filename:  '[name].js',
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: 'Webpack demo',
    }),
  ],
};
```

Now we can just run `node_modules/.bin/webpack` and it will find the `webpack.config.js` file and use its configuration parameters.

Now we have a new `index.html` file in the `build/` folder. If we open it, it will run our component code and we'll see `Hello world` inside a `div`.

### Adding a build shortcut

package.json:
```javascript
"scripts": {
  "build": "webpack"
},
```

Now we can just run with `npm run build`

### HtmlWebpackPlugin extensions

You could replace HtmlWebpackPlugin with your own or:
* [html-webpack-template](https://www.npmjs.com/package/html-webpack-template)
* [html-webpack-template-pug](https://www.npmjs.com/package/html-webpack-template-pug)

There are also some plugin extensions:
* [favicons-webpack-plugin](https://www.npmjs.com/package/favicons-webpack-plugin)
* [script-ext-html-webpack-plugin](https://www.npmjs.com/package/script-ext-html-webpack-plugin)
* [multipage-webpack-plugin](https://www.npmjs.com/package/multipage-webpack-plugin)
* [resource-hints-webpack-plugin](https://www.npmjs.com/package/resource-hints-webpack-plugin)
* [preload-webpack-plugin](https://www.npmjs.com/package/preload-webpack-plugin)

## Automatic Browser Refresh

### Webpack `watch` mode and `webpack-dev-server`

The `webpack --watch` command detects changes to your files and recompiles automatically.

`webpack-dev-server` is built on top of the `watch` mode and 

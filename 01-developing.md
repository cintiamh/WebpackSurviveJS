# Developing

1. [Getting Started](#getting-started)

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

This will run webpack with input `app/index.js` and output `build/index.js`.

### Directory Structure

* app/
  * index.js
  * component.js
* build/
* package.json
* webpack.config.js

### Setting up assets

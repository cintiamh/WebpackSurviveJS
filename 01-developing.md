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

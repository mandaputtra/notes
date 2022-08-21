# Module System

Module is a unit of code, organized to a file or folder. In Node.js we have global scope object called `module`, which hold informations about that specific file. Assigning value to `module.exports` will expose them for inclusion in other file (using it on other file)

```js
// file sum.js
function sum(a, b) {
  return a + b
}

module.exports = sum

// file average.js
function average(total, amount) {
  return total / amount
}

module.exports = { average }

// file main.js
const { average } = require('./average') // named exports
const sum = require('./sum') // default exports

sum(1, 2) 
average(100, 45) 
```

Module object inspection

```js
Module {
  id: '.',
  exports: {},
  parent: null,
  filename: '/Users/jon/Projects/heynode.com_content/index.js',
  loaded: false,
  children: [],
  paths:
   [ '/Users/jon/Projects/heynode.com_content/node_modules',
     '/Users/jon/Projects/node_modules',
     '/Users/jon/node_modules',
     '/Users/node_modules',
     '/node_modules' ] }
```

## Type of module

Node.js has three main types of modules to work with:

- Built-in modules, node.js default module
- Local modules, your own module that you created
- External modules, external module form package manager/git that you listed on package.json

## `import` and `export`

You may have also heard about ESM (EcmaScript Modules), and seen code that uses `import` and `export` keywords when dealing with modules. This is the next generation module system, which is only currently supported behind experimental flags of the latest Node.js releases, or by using a transpiler like Babel to convert the ESM import and export code into regular CommonJS format through adding a build step to the project.


## Reading

- https://docs.npmjs.com/about-packages-and-modules#about-modules
- https://nodejs.org/api/esm.html
- https://docs.npmjs.com/cli/v8/commands/npm-publish

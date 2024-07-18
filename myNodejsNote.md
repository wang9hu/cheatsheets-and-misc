# Node notes
- nodejs comes with REPL: read eval print loop, a command line env to run js

- `npm init -y`

  - npm initialize, create a package.json file
  - `-y`: use default
    <br>

- `npm i -g package-name`

  - `i` is short for `install`
  - `-g` is short for `--global`
  - install a packge globally
    <br>

- `npm i package-name --save`

  - install the package as a development dependency
  - `--save` means the package is saved in `package.json`, which is already the default setting of `npm i package-name`
  - `--save-prod`: means this saves the package in `dependencies`, this is the default
  - `--save-dev`: means this saves the package in `devDependencies`
  - `--save-optional`: means this saves the package in `optionalDependencies`
    <br>

- `npm ls package-name?`

  - `ls` is short for `list`
  - outputs installed packages and their dependencies of the current project as a tree-structure to the stdout
  - if no `package-name`, output all the dependencies
  - `-g`: only display the globally installed packages/dependencies
  - `--prod` or `--dev`: only dependency for `dependencies` or `devDependencies`
  - `--json`: format the packages in the JSON format
    <br>

- `npm test`, `npm start`, `npm restart`, and `npm stop` are all aliases for `npm run xxx`, other `scripts` defined will need to use `npm run xxx` syntax
  <br>

- Execute files in the same directory in node: read contents in filename, and execute them

  - _(cli)_ `$ node filename`
  - enters the Node REPL: `$ node`
    - `.load filename`
    - abort and exit REPL: ctrl+c

- Node module system: how code sharing in different files

  - In Node every file is considered a module and wrapped within a **Module Wrapper function** before executed:

    ```
    (function(exports, require, module, __filename, __dirname) { Module code })
    ```

    - **exports**: [A reference to the module.exports]
      e.g.: `exports.newProp = newPropValue`;
      - Caution: if use `exports = newValue`, it will unbound exports with `module.exports`, and if use `module.exports = newValue`, 
        <br>
    - **require**: [import modules, JSON, and local files]
      e.g.: `const myLocalModule = requre('./path/myLocalModule');`
      - Take from `module.exports`, not `exports`
      - `require(id)`
        - id (string) module name or path
        - Returns: (any type) exported module content (from cache)
      - `main`: When a file is run directly from Node.js, require.main is set to its module `require.main === module`
        - when file run by node `node file.js`, return true
        - when file run by require(`./file.js`), return false
      - `cache`: Modules are cached in this object when they are required. By deleting a key value from this object, the next require will reload the module.
        - once a module is loaded by `require(module)`, all variables declared from this module lexical scope is completed and shared;
        - only by deleting its cached module and require it again
          <br>
    - **module**: [a reference to the object representing the current module.]
      - `Module` {
        - `id: '.',`
        - `path: 'C:\\Users\\Xiao Wang\\Coding\\practice',`
        - `exports: {},`
        - `filename: 'C:\\Users\\Xiao Wang\\Coding\\practice\\index2.js',`
        - `loaded: false`,
        - `children: []`,
        - `paths`:
        ```
        [
          'C:\\Users\\Xiao Wang\\Coding\\practice\\node_modules',
          'C:\\Users\\Xiao Wang\\Coding\\node_modules',
          'C:\\Users\\Xiao Wang\\node_modules',
          'C:\\Users\\node_modules',
          'C:\\node_modules'
          ]
        ```
        }
        <br>
      - `__filemane`: [The file name of the current module.]
        <br>
      - `__dirname`: [The directory name of the current module.]
  <br>

- Continuation-Passing Style 
  - a technique used to represent **asynchronous** computations by passing continuation functions as arguments, often involves using callback functions.
  - Instead of returning a value, a function takes an extra callback function as argument, which will be called 
  ```
  function addAsync(a, b, callback) {
    setTimeout(() => {
      const result = a + b;
      callback(result);
    }, 1000);
  }

  // Using the continuation function
  addAsync(3, 4, (result) => {
    console.log(result); // Prints 7 after 1 second
  });
  ``` 
  - very commonly used before `async/await`, 

- Error-first function
  - a convention way of handling errors in asynchronous functions in node.js.
  - passed in as a continuation function and its first parameter `error` is reserved for an error object.
  ```
  exampleAsyncFunction('value1', 'value2', (error, result) => {
    if (error) {
      console.error('Error:', error.message);
      // Handle the error appropriately
    } else {
      console.log('Result:', result);
      // Continue with the successful result
    }
  });
  ``` 
  - if `error` is not `null` or `undefined`, it indicates an error occurred during that async operation. Or else, the operatio is successful.

### things good to know

- <span>Node version manager</span>: `nvm`
  - install other version: `nvm install latest` or `nvm install vX.Y.Z`
  - make a version default: `nvm alias default vX.Y.Z`
  - use other verison: `nvm use [version]`
    - **Note**: when changing node version, all the globally installed packages are different.
    - It is **not recommanded** to install packages globally
  - all versiona available: `nvm ls`
    <br>
- <span>Node Package eXecute</span>: `npx`

  - execute javascript packages directly without installing.
    <br>

- err handle first callbacks
- post data: stream
- commnad line: set variables in command
  ```
  // in package.json, set up process.env.NODE_ENV
  "scripts": {
    "start": "NODE_ENV=production node server/server.js",
    ...
  }
  ```
- check for ports that are listening:
  `sudo lsof -i -P -n | grep LISTEN`
- kill port:
  `npx kill-port 3000`
  <br>

- Delete all other git branches:
  `git branch | grep -v "develop" | grep -v "master" | grep -v "main" | xargs git branch -D`

### Common JS vs ES6 Module

CJS and ESM are two module systesm in JavaScript that are actively being used.

- <span>CJS</span> was introduced as the default module system for **Node.js**

```
  // importing
  const fs = require("fs");

  // exporting using exports or module.exports, but stick to one only 
  module.exports.someVariable = ...
  exports.someVariable = ...

  // this will disconnect exports entirely
  module.exports = someVariable 

  // this will disconnect with module.exports, DON'T USE THIS!!
  exports = someVariable 
```
  - `exports` and `module.exports` initially refer to the same object, but `require` only takes from `module.exports`
  - CJS was initially specific for Nodejs when browser did not have a module system yet.
  <br>

- <span>ESM</span> was introduced by ECMAScript 2015 (ES6) as the standardized module system for **working in browsers.**

```
  // importing
  import fs, { nonDefaultExport1, nonDefaultExport2 } from "fs"

  // exporting
  export default function() { return "Hi there!";}
  export nonDefaultExport1() { return "Hi there!";}
```

  ESM as the standard in **browser-land**, and CJS as the standard in node-land.
  Frontend frameworks like React or Vue have been using the ESM syntax even before it became a standard in the browser. Though they used tools like Babel to transpile it to CommonJS syntax
  <br>

- CJS is **synchronous**, it will block execution of code until module is fully loaded, which ESM is **asynchronously** imported.
- ESM **can** `import` CJS modules, but CJS **cannot** `require` a ESM.
- Both **CJS** and **ESM** are loaded and evaluated at run time in nodejs with dynamic imports, but **ESM** in compliation are evaluated statically at compile-time before code execution.
- Browsers don't support **CJS**, require bundlers like webpack; **ESM** is supported in modern browsers


<span>Ways to adopt ESM in Node:</span>

- use `.mjs` file extension for ESM files
- use `.js` file and in nearest parent `package.json`, contains a top-level `"type": "module"` (default is `"commonjs"`), this will tell Node that all `.js` files are written with ESM

<span>Tell HTML file that you are using module:</span>

- in `<script></script>` tag, add `type="module"` (probably also add `defer` to wait for script to load)


### Node build-in Modules

- <span>HTTP modules</span>
```
  import http from 'http';
  const PORT = 8000;
  const server = http.createServer((req, res) => {
    //
  })

  server.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`)
  })
```
  - `http.createServer([options][, (req, res) => { ... }])`
    - `res`: 
      - `.write`: 



### Node packages

- #### cross-evn
<br>

- #### msw
  - Mock Service Worker (MSW) is a seamless REST/GraphQL API mocking library for browser and Node.js.
  - mocking HTTP requests at the network level, ideal for **testing API calls**, simulating **different server states** (like errors, loading states, and empty states)
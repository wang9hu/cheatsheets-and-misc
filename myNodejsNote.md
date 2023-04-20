# Node notes

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
      - Caution: if use `exports = newValue`, it will unbound exports with `module.exports`
        <br>
    - **require**: [import modules, JSON, and local files]
      e.g.: `const myLocalModule = requre('./path/myLocalModule');`
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

### things need to address later

- Node version manager: `nvm`
  - install other version: `nvm install latest` or `nvm install vX.Y.Z`
  - make a version default: `nvm alias default vX.Y.Z`
  - use other verison: `nvm use [version]`
  - all versiona available: `nvm ls`
    <br>
- Node Package eXecute: `npx`
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

### Common JS vs ES6 Module

CJS and ESM are two module systesm in JavaScript that are actively being used.

- CJS was introduced as the default module system for Node.js

  ```
  // importing
  const fs = require("fs");

  // exporting
  module.exports = function() { return "Hi there!";}
  ```

  CJS was initially specific for Nodejs when browser did not have a module system yet.
  <br>

- ESM was introduced by ECMAScript 2015 (ES6) as the standardized module system for working in browsers.

  ```
  // importing
  import fs, { nonDefaultExport1, nonDefaultExport2 } from "fs"

  // exporting
  export default function() { return "Hi there!";}
  export nonDefaultExport1() { return "Hi there!";}
  ```

  ESM as the standard in browser-land, and CJS as the standard in node-land.
  Frontend frameworks like React or Vue have been using the ESM syntax even before it became a standard in the browser. Though they used tools like Babel to transpile it to CommonJS syntax
  <br>

- Since most modules were initially written in CommonJS, It is possible to import CJS modules in ESM (`import * as CJS from 'cjs-module'`), but ESM cannot be used in CJS modules.

Ways to adopt ESM in Node:

- use `.mjs` file extension for all ESM files
- use `.js` file and in nearest parent `package.json`, contains a top-level `"type": "module"` (default is `"commonjs"`), this will tell Node that all `.js` files are written with ESM

Tell HTML file that you are using module:

- in `<script></script>` tag, add `type="module"` (probably also add `defer` to wait for script to load)

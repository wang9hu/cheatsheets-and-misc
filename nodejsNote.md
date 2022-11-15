# Node related notes

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

    - **exports**: [A reference to the module.exports] e.g.: exports.newProp = newPropValue;
      - Caution: if use 'exports = newValue', it will unbound exports with module.exports
        <br>
    - **require**: [import modules, JSON, and local files] e.g.: const myLocalModule = requre('./path/myLocalModule');
      - require(id)
        - id <string> module name or path
        - Returns: <any> exported module content (from cache)
      - main: When a file is run directly from Node.js, require.main is set to its module `require.main === module`
        - when file run by node `node file.js`, return true
        - when file run by require('./file.js'), return false
      - cache: Modules are cached in this object when they are required. By deleting a key value from this object, the next require will reload the module.
        - once a module is loaded by `require(module)`, all variables declared from this module lexical scope is completed and shared;
        - only by deleting its cached module and require it again
          <br>
    - **module**: [a reference to the object representing the current module.]
      - Module {
        - id: '.',
        - path: 'C:\\Users\\Xiao Wang\\Coding\\practice',
        - exports: {},
        - filename: 'C:\\Users\\Xiao Wang\\Coding\\practice\\index2.js',
        - loaded: false,
        - children: [],
        - paths: [
          'C:\\Users\\Xiao Wang\\Coding\\practice\\node_modules',
          'C:\\Users\\Xiao Wang\\Coding\\node_modules',
          'C:\\Users\\Xiao Wang\\node_modules',
          'C:\\Users\\node_modules',
          'C:\\node_modules'
          ]
          }
          <br>
    - \_\_filemane: [The file name of the current module.]
      <br>
    - \_\_dirname: [The directory name of the current module.]
      });

  ```

  ```

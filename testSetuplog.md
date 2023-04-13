1. used `jest --init` to setup jest, a `jest.config.js` file is created after this (not sure what this does....)

    - Would you like to use Jest when running "test" script in "package.json"? … yes
    - Would you like to use Typescript for the configuration file? … no
    - Choose the test environment that will be used for testing › node
    - Do you want Jest to add coverage reports? … no
    - Which provider should be used to instrument code for coverage? › babel
    - Automatically clear mock calls, instances, contexts and results before every test? … yes
    <br>
    <br>

1. run `npm install -g jest` globally so that jest can be run directly from the CLI

1. Configure Babel to target your current version of Node by creating a `babel.config.js` file in the root of your project, this file is for project-wide configuration. For file-relative configuration, see [here](https://babeljs.io/docs/en/config-files)
    ```
    module.exports = {
      presets: [['@babel/preset-env', {targets: {node: 'current'}}]],
    };
    ```



1. it is recommanded to define the configuration in a dedicated file, which will be discovered automatically if its name is `jest.config.js|ts|mjs|cjs|json`. [For more Details](https://jestjs.io/docs/configuration)

    1. create a `jest-setup.js` file and a `jest-teardown.js` file for `globalSetup` and `globalTeardown` in `jest` in package.json

    1. add below in `jest.config.js` or `package.json`
      - for jest.config.js
      ```
      module.exports = {
        ...,
        globalSetup: "./jest-setup.js",
        globalTeardown: "./jest-teardown.js",
        ...
      }
      ```
      - for package.json
      ```
      "jest": {
        "globalSetup": "./jest-setup.js",
        "globalTeardown": "./jest-teardown.js"
      },
      ```

1. npm test (which in `package.json` file will run `jest`) will test:
    - any `filename.test.js`
    - files in `__test__` directory
    <br>
    <br>

1. in `package.json` file, if added `--coverage` after `jest`, the a detailed result will show after each test, and this will also create a new directory folder called `coverage`, in which has a dir `lcov-report` folder, in which there is a `index.html` that will have a detailed test results
    - I added the `coverage` dir name in the `.gitignore`
    <br>
    <br>

1. test body format
    ```
    describe ('description of the following tests', () => {
      test('description of the current test', () => {
        // test codes
      })
    })
    ```
    <br>
1. installed `regenerator-runtime`, seen it in the testing unit, have not use it in this project, not sure what it does for now, 

1. installed `@testing-library/jest-dom` using `npm install --save-dev @testing-library/jest-dom` for using handy custom jest matchers 

1. installed `@testing-library/user-event` using `npm install --save-dev @testing-library/user-event` for userEvent (better version of fireEvent)

1. need for `jest-environment-jsdom` with `npm i jest-environment-jsdom --save-dev` if jest >= 28
   - in `jest.config.js` file, set `testEnvironment: "jsdom"`

1. in `jest.config.js` file, set `verbose: true"`

1. in `babel.config.js` file, add `"@babel/preset-react"` to presets
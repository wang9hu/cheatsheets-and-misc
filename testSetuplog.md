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

### testing-library/react:
   1. query methods:
      1. `getBy`: expect an element to be present in DOM\
         - throws error if no match or multiple matches are found
         - `getAllBy`: returns an array of all matching nodes, throw error if no match
         - **Recommended for**: most cases when only one match is present before proceeding with test
      2. `queryBy`: check that an element is not present in DOM
         - return 'null' if element is not found, throw error if multiple matches are found
         - `queryAllBy`: return an array of all matching nodes, return `[]` if no match
         - **Recommended for**: right choice for negative assertions.
      3. `findBy`: find an element that might not be immediately present because of asynchronous operations. `findBy` => `getBy` + `waitfor`
         - return a Promise resolves when a match is found, or reject when no match or multiple matches are found after a default timeout (1000ms)
         - `findAllBy`: returns a Promise resolves to an array of matches, reject if no match after a default timeout (1000ms)
         - **Recommended for**: testing element appear as a result of asynchronous actions, like data fetching
  <br>

   1. Guilding Principles:
      1. If it relates to rendering components, then it should deal with DOM nodes her than component instances, and it should not encourage dealing with component instances.
      2. It should be generally useful for testing the application components in  way the user would use it. We are making some trade-offs here because we're using a computer and often a simulated browser environment, but in general, utilities should encourage tests that use the components the way they're intended to be used.
      3. Utility implementations and APIs should be simple and flexible.
  <br>
   1. query targets:
      1. `byRole`: by its **accessibility** role, one of the most preferred selectors because it encourages accessibility practices, useful for selecting elements that have **explicit roles** (e.g., button, link, checkbox) in the UI. It closely aligns with how users **identify elements** on the page.
   
      2. `byLabelText`:  by its label text, which is useful for form fields.
   
      3. `byPlaceholderText`:  input or textarea element by its placeholder value.
   
      4. `byText`: by text content, suitable for selecting buttons, links, paragraphs, and other elements that are **identified by their text content**.
   
      5. `byDisplayValue`:  input, textarea, or select element by its **current value**, useful for asserting the value of form elements, especially when you want to check that **a form field has been populated with the expected initial value** or **has changed to a new value** after user interactions.
   
      6. `byAltText`: particularly useful for finding an `<img>`, but can also be used for other elements like `<input>` of type image) by its alt attribute.
   
      7. `byTitle`:  by `title` attribute or svg `title` tag. The title attribute is commonly used to provide additional information about an element, often displayed as a tooltip when the user hovers over the element.
   
      8. `byTestId`: by a test ID (must be given to the element beforehand like `data-testid="submit-button"`), useful when you need to select elements that are difficult to query by text or role, or when you're working with a component that doesn't render any user-facing text, not encouraging best practices for accessibility or semantic HTML. It's a **"last resort"** selector for when other queries won't work.
   <br>
    1. User Interaction `userEvent`
       1. setup: recommended invoking `userEvent.setup()` before the component is rendered. 

### jest 
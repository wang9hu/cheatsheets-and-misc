# React notes

- [Docs](https://react.dev/)
- A component is essentially a function
- component:

  - splite UI into independent, reusable pieces
  - a component represent a part of DOM
  - component can have **DOM** elements
  - component can have other component inside
  - need to `npm install react` and import before use

    <br>

- [React Component](#react-component)
  1. [Component Class](#component-class)
  2. [Functional Component](#functional-component)
- [React Re-render](#react-re-render)
- [React conventions](#react-conventions)
- [Create-React-App](#create-react-app)
- [Redux](#redux)
- [Webpack](#webpack)

## React Component

- **JSX**: javascript XML (file name): precompiled syntax exntension to JS, React 'element' can be rendered into HTML element on DOM by JSX

  - e.g., `<h1>Hello, {this.props.anykeylabel}</h1>`
  - could have js inside of DOM element, wrapped in `{}`
    - `<h1>{2 + 2}</h1>`
    - `<p{user.firstName}`
    - `{formatName(user)}`
  - JSX attribute: key value pair: used to pass in data
    - for component attributes, could use `'for string'` or `{js-expression}`, one or another
    - in child component, use `this.props.childVariable`
    - in parent component, use `childVariable = {js-expression}`
  - JSX can interpret an array of JSX statements and take each individule out e.g., `{boxes}`
    <br>

- **Virtual DOM**: representing DOM elements purely in a lightweight JS form.
  - use **React-DOM** library,
  - achieve fast render time
  - React processes changes very quickly, only rendering to the real DOM when and where needed.

### Component Class:

Write these first when starting a new class component file:

```
import { Component } from 'react';

class MyComponent extends Component {
  render() {
    return ()
  }
}

export default MyComponent;
```

- class component must `extends React.Component` in its declaration
- class component have **reserved** keyword `props` specifically for passed-in data, and data can be accessed by `this.props.name`
- if `constructor`, **first** need to use `super()` or `super(props)` if `props`
- in class, `render() {}` is a special method and it will show whatever is being returned on the DOM. **Re-render** will only execute `render()` each time.
  <br>

- child component can set parameters on `{this.props}` object in the return DOM element statement, e.g., `return <h1>Hello, {this.props.childComponentlaber}</h1>;`
- parent component can use `<childComponent childComponentlaber = data />` to assign data value to the parameter in the parent component
  <br>

- Class component with constructor and `this.state` could use `{this.state.propertyName}` to access data in its own state
  <br>

- **Methods/variables**:
  - if created in constructor: they will be instance methods/variables (usually just `this.state`)
  - If created outside of constructor: starting with React v16.3, these methods are automatically bound to the instance of the component, no need to explicitly bind them using `.bind()`. When being invoked in `render()`, use `this.methodName` or destructing it first `const { methodName } = this`
  - **Do Not** create any methods in `render(){}`
    <br>
- may need other library (npm & import)
  <br>

- **State**: top down, uni-directional data flow, used to pass data

  - accessible and easily maintained
  - **State** maintained in top level components (as an obj called `State`) and passed down (through `props`) to child component
  - `props` never go upstream or to sibling component.
  - values in props are **immutable**
  - use `setState()` in order to update **State**:
    `setState(nextState, callback?)`

    - `nextState`: either an object or a function
      - if object, it is **shallow merged**, it will look for the keys that passed in and update its value in state.
      - if function, it is an **updater**, having two optional arguments: `state` and `props`
    - `callback`: _optional_, invoke after update is commited
    - <span>Never</span> manually set `state`.
    - only use `setState()` where `state` is defined in component
    - `setState()` will only update what is passed in, the rest stay the same

      ```
      // in constructor:
      this.state = {
        name: 'Ken',
        sex: 'male'
      }

      // invoking setState()
      this.setState({name: 'Andy'}) // sex is stll 'male' after update
      ```

  - Any changes to the state will trigger an update, or "re-render", of components that depends on it.
    <br>

- **Life cycle component**: if the function definition is given in the component class
  - `componentDidMount(){ /.../ }`: this will run after the **first time** component is rendered on the DOM
  - `componentDidUpdate(prevProps, prevState, snapshot?){ /.../ }`: this will run **after updating** is complete, but not for the initial rendering
  - `componentWillUnmount( /.../ )`: this will run **before the removal** of rendered Box from DOM
    <br>

##### **[Back to top](#react-notes)**

 <br>

---

### Functional Component

Mostly in arrow function form, and should be a pure function (no outside effect):

```
const MyComponent = () => {
  return ()
}
```

- Pros:
  - <span>No `this`!!</span>: No need to use `this` keyword! You don't have to deal with `state` / `methods`, and your `props` are passed in as a parameter.
  - <span>Less boilerplate</span>. As your component is simply a function, free of the constraints of a React component class, the amount of boilerplate in creating a stateless functional component is greatly reduced. This makes it so the resulting code for you component is concise and and clear.
  - Clearly separates your concerns. This is important when you're separating your application into container and presentational components.
  - <span>React Hooks</span>: functions that allow functional components the ability to do things that were typically only reserved for class components.
- Cons:

  - No access to component lifecycle methods (ie `ComponentDidMount`), but react hooks can compensate that
    <br>

- **Higher-Order Components**
  - a higher-order component is a function that takes a component and returns a new component.

<br>

#### React Hooks

- Two rules:

  1. Only call hooks at the top level, must **NOT** be calling them within _loops_, _conditions_, and _nested functions_.
     - Reason: to make sure hooks are called in the same order for every render. The call order is essential for Hooks to work correctly.
  1. Only call hooks from **React functional components** or other hooks
     <br>

- **<span>useState</span>**: the most common way to manage state in React functional components

  - `const [state, setState] = useState(initialState)`
    <br>

  - `initialState`: the value you want the state to be initially
  - **return**: state and the function that can changed the state
    <br>

  - `state`: The current state.
  - `setState`: `setState(nextState/updater)` set function that updates the `state` to a different value and trigger a re-render. Will match the `initialState` during the first render.
    - `nextState`: The value that you want the state to be next.
    - `updater`: a pure function that take the current state as its only argument, and return the next state: `setState(prev => prev + 1)`
    **Note**:
      - If the `setState()` uses `state` in its `nextState` expression, multiple calls on it will not have accumulate effects on the final state value. However, `prev` in updater is up to date and will have accumulate effects on the final `state`
        ```
        // below one click will only make count to 2;
        const [count, setCount] = useState(1);
        const handleClick = () => {
          setCount(count + 1); // here count is not up to date
          setCount(count + 1);
          setCount(count + 1);
        }

        // below one click will make count to 4;
        const [count, setCount] = useState(1);
        const handleClick = () => {
          setCount(prev => prev + 1); // here prev is up to date
          setCount(prev => prev + 1);
          setCount(prev => prev + 1);
        }
        ``` 
      - If the next state is the <span>same reference</span> or <span>same primitive value</span> from current state, React will <span>skip re-rendering</span>. Make sure the passed-in **Reference is Different** from the original state reference (_use a new reference or use spread syntax_)
    <br>

  ```
  const [state, updateState] = React.useState('initial state');

  console.log(state); // 'initial state'
  console.log(updateState); // 'Function(){}' that can be used to update that state, it accepts a new state value and enqueues a re-render of the component.

  updateState('next state'); // update the state
  ```

  <br>

- **<span>useEffect</span>**: Equivalent of lifecycle methods in React class components

  - `useEffect(setup, dependencies?)`
    <br>

  - `setup`: a setup function with setup code that connects to external system
    - **return**: _optional_ a cleanup function that will run when this component unmounts
  - `dependencies`:
    - if no `[dependencies]`, will run `setup` after initial and each update
    - if `[dependencies]`, only run `setup` if `dependencies` changed
    - if `[]` (`dependencies` omitted), only run `setup` after the initial render
  - **return**: `undefined`
    <br>

  ```
  React.useEffect(() => {
    console.log('component updated');
  },[dependencies])
  ```

  **Common use case**:

  - `useEffect` let you “step outside” of React and synchronize your components with some **external system** like a non-React widget, network, or the browser DOM. If there is no external system involved (for example, if you want to update a component’s state when some props or state change), you shouldn’t need an Effect.
    <br>

- **<span>useMemo</span>**: cache the **result** of a calculation between re-renders.

  - `const cachedValue = useMemo(calculateValueFn, dependencies)`
    <br>

  - `calculateValueFn`: the function that **calculating the value**, should take **no input** and return a value.
  - `dependencies`: the array of dependencies that triggered the useMemo
  - **return**: the calculated value and cache it in `cachedValue`. Will return previous `cachedValue` if `dependencies` are the same for rerender
  - On the initial render, `useMemo` returns the result of calling `calculateValueFn` with no arguments.
    <br>

    **Common use cases:**

  1. make a slow function wrap inside useMemo so that doesn't re-compute for every re-render
  2. make sure the reference of an object or an array is exactly the same as it was in the last rendered
     <br>

- **<span>useCallback</span>**: cache a **function** definition between re-renders.

  - `const cachedFn = useCallback(fn, dependencies)`
    <br>
  - just like `useMemo`, but it return the first paramenter, which is the **entire function**, instead of returning the calculated value of the function, and the function could have inputs
  - `useCallback(myFunction, dependencies)` = `useMemo(()=>myFunction, dependencies)`
    <br>

  ```
  const [number, setNumber] = useState(1);

  // Upon re-render, below will reassign to a new getItems function
  const getItems = () => {
    return [number, number + 1, number + 2]
  }

  // Upon re-render, below will not re-create getItems function if number doesn't change
  const getItems = React.useCallback(() => {
    return [number, number + 1, number + 2]
  }, [number])
  ```

  <br>

  **Common use case:**

  1. make sure the reference of an function is exactly the same as it was in the last rendered, such as passing function to child component
  2. for some reason creating a function is really slow for each re-render (rarely)
     <br>

- **<span>useContext</span>**: lets you read and subscribe to context from your component

  - Context lets the **parent component** make some information available to **any child components** in the tree below it (no matter how deep) without passing it explicitly through props.
    <br>

  1. **SomeContext** is created by `React.createContext` function

     ```
     // call createContext to create a context
     import { createContext } from 'react';

     // and export it if in seperate contextcreator file
     export const SomeContext = createContext(defaultValue)
     ```

     - if no defaultValue, specify `null` as input
     - **return**: a context object that doesn't hold any information, it represents which context other components read or provide.
     - This could be done in _contextcreator_ file, or integrated in highest parent component
       <br>

  2. In parent component, import the created **SomeContext** from _contextcreator_ file

     - usually use other hooks to create some **state** for context
     - in the component return, wrap children component with `<Somecontext.provider>` tag
     - inside `<Somecontext.provider>`, pass the **state** as `value` attribute
     - now all children component within have access to **state**

     ```
     import { useState } from 'react';
     import { SomeContext } from '[path to contextCreator file]';
     import Child from '[path to ChildComp file]';

     function ParentComp(props) {
       const [someState, setSomeState] = useState(someValue)

       return (
         <SomeContext.Provider value={[someState, setSomeState]}>
           <Child>
         </SomeContext.Provider value={someState}>
       )
     }
     ```

     <br>

  3. In child component, import `useContext` hook and **Somecontext**

     - invoke `useContext` and pass **Somecontext** as input
     - assign the return value with variables in the same format of the **state** from `<Somecontext.provider>`
     - _Note_: when assign the return value of `useContext()` to variables in child component, this child component will re-render whenever **SomeContext** changes, whether or not variables are used does not matter.

     ```
     // In child component
     import { useContext } from 'react';
     import { SomeContext } from '[path to contextCreator file]';

     function Child(props) {
       const [someState, setSomeState] = useContext(SomeContext);
       return (
         <>
           {...}
         </>
       )
     }
     ```

     <br>

- **<span>useReducer</span>**: lets you add a **reducer** to your component.

  - `const [state, dispatch] = useReducer(reducer, initialArg, init?)`
    <br>
  - `reducer`: a function that specifies how the state gets updated.
  - `initialArg`: the input for `init`.
  - `init`: _optional_ the initializer that should return the `initialState`.
  - `InitialState = init ? init(initialArg) : initialArg`
  - **return**: the `state` and the `dispatch` function in an array
    - `state`: The current state
    - `dispatch`: update state and <span>trigger</span> a re-render: `dispatch(action)`
      - `action`: an object identifying the action performed by user. By convention, an action is usually an object with a `type` property with other optional properties containing the <span>minimal information</span> about what happened. `e.g., { type: 'what_happened, /* other fields? */ }`
      - **return**: no return value
        <br>
  - <span>Reducer </span>

    ```
    function yourReducer(state, action) {
      // return next state for the React to set
    }
    ```

    - reducer is a <span>pure</span> function, meaning itself makes no impact to its environment when executing.
    - Takes in two arguments: `state` and `action`
    - **return**: the updated state, must be <span>different reference</span>
    - Conventionally use **switch statement** inside reducers, and wrap each `case` into `{`and`}`, and `return` inside of each `case`
      <br>

  - <span>VS</span> `useState`:
    - **Code size**: `useState` have less setup code, but `useReducer` can help cut down on the code if many event handlers behave similarly
    - **Readability**: `useState` is very easy to read when state updates are simple, while `useReducer` have better organized event handler logic
    - **Debugging**: `useState` is difficult to debug from, while `useReducer` could have console log for each case to pinpoint which action is causing the bug
    - **Testing**: reducer is a pure function and can be export and test separately.
    - **Personal preference**: `useState` and `useReducer` are essentially the same.

<br>

- **<span>useRef</span>**: reference a value that’s not needed for rendering.

  - `const ref = useRef(initialValue);`
    <br>

  - return: an object with a single property: `{ current: initialValue }`
  - `initialValue`: the value ref object's current property to be initialled. This value is ignored after ref initialization.
  - change ref value: `ref.current = newValue`, changing it does not trigger a re-render, so refs are not appropriate for storing information you want to display on the screen
    <br>

  **Common use cases**:

  - It’s particularly common to use a `ref` to <span>manipulate the DOM</span>. React has built-in support for this:
    1. Initial `ref` to `null`
       ```
       const inputRef = useRef(null);
       ```
    2. Then pass `ref` object as the `ref` attribute to the JSX of the DOM node you want to manipulate:
       ```
       return (
        <>
          ...
          <input ref={inputRef} />;
          ...
        </>
       )
       ```
    3. After React creates the DOM node and puts it on the screen, React will set the `current` property of your `ref` object to that DOM node: `inputRef.current.focus();`
    4. React will set the current property back to `null` when the node is removed from the screen.

  <br>

- **<span>memo</span>**: `React.memo()` is like `useMemeo()` but for components. It lets you skip re-rendering a component when its `props` are unchanged.
  `const MemoizedComponent = memo(SomeComponent[, arePropsEqual])`

  - `SomeComponent`: The component that you want to memoize.
  - `arePropsEqual`: (optional) A function that accepts two arguments: the component’s previous props, and its new props.
    - return `true` if the old and new props are equal
    - By default, React will compare each prop with `Object.is(prevProps, newProps)`.
  - **return**: a new React component behaves the same as the component provided to `memo`
  - _Note_: the returned new component will still re-render when state or context inside changes

    ```
    function App() {
      const exampleData = {test: "Oui Monsieur"};
      const memoizedData = useMemo(() => exampleData,[]);

      const stringFunction = (s) => s.split("").reverse().join("");
      const memoizedCB = useCallback(stringFunction, []);

      return (
        <div className="App">
          <main>
            {/* below two will re-render when App re-render*/}
            <MemoPropsCountComponent data={exampleData} stringFunction={stringFunction} />
            <MemoPropsCountComponent data={memoizedData} stringFunction={stringFunction} />
            {/* below will only render once */}
            <MemoPropsCountComponent data={memoizedData} stringFunction={memoizedCB} />
          </main>
        </div>
      );
    }

    const MemoPropsCountComponent = React.memo((props) => {
      const otherCountRef = useRef(0);
      const testString = 'hello';
      useEffect(() => {
        otherCountRef.current++;
      });
      return (
        <div className="counter">
          <p>Current count: {otherCountRef.current} </p>
          <p> Function:  {props.stringFunction(testString)} </p>
          <p> Data: {JSON.stringify(props.data)} </p>
        </div>
      );
    });
    ```

  **Common use case**:

  - Use it when you do not want child component re-render when its parent is being re-rendered unless its props have changed.
  - Combine with `useMemo`, `useCallback` in parent component to ensure on `props` not changing accidentally
    <br>

##### **[Back to top](#react-notes)**

 <br>

---

## React Re-render

Initial render: when a component first appears on the screen
<br>

Render-triggers:

1. **<span>props changed</span>** (passed in `props`)
2. **<span>Internal state change</span>** (`useState`, `useContext`, `setState`...)
3. **<span>Parent component rerendered</span>** (unless `React.memo()` is called for a component)
   <br>

Virtual DOM: a JavaScript representation of the real DOM tree

##### **[Back to top](#react-notes)**

 <br>

---

## React conventions:

- <span>Key</span> Attribute: when use `filter()` and `map()` to process lists of JSX elements, it is conventional to assign a `key` attribute to each direct JSX element.

  - React is the only thing that requires this `key` attribute
  - Works like a name for each item, the `key` lets React identify the item throughout its lifetime. If not given, react would assign index to key, which is not tighly binded with each item and would cause errors due to data array manipulation
    <br>
  - Sources of keys: (bind key value with each item)
    - **Data from database**: use unique keys/ID from database
    - **Logically generated**: (when adding new items) use incrementing counter, `crypto.randomwUUID()` or a package like `uuid` to create keys
      <br>
  - Rules of keys:
    - Keys must be **unique** among siblings
    - Keys must **not change**
    - Keys usually at the **top level** of each JSX element
      <br>

- <span>React.createElement()</span>: create a React element. Serves as an alternative to writing JSX
  `const element = createElement(type, props, ...children)`

  - `type`: must be a valid React component, could be a tag name (`div`) or a React component(class or functional or special component like `Fragment`)
  - `props`: must either be an object or `null`.
  - Only use this when initializing the app from a file that is **NOT** JSX
    <br>

- <span>Components</span>:

  - `<Fragment>`: often used via `<>...</>` syntax, for grouping elements without a wrapper node.
    - `key`:_optional_ only available to `<Fragment>...</Fragment>` not `<>...</>`, usually need to do this when **Rendering a list of Fragments**
    - Usage: when rendering, react will remove the fragment tag and directly render its children on page.
      <br>

- <span>react-dom</span>: for building up DOM element for browser

  - <span>Before</span> ReactV18: `ReactDOM.render(component, htmlElement)`

    ```
    import ReactDOM from 'react-dom';

    ReactDOM.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>,
      document.getElementById('root')
    )
    ```

  - <span>After</span> ReactV18: create a root first use `createRoot(htmlElement)`

    ```
    import { createRoot } from 'react-dom/client'

    const container = document.getElementById('root');
    const root = createRoot(container)
    root.render(
      <React.StrictMode>
        <App />
      </React.StrictMode>
    )
    ```

    <br>

- <span>react-router-dom</span>: React Router enables "client side routing".

  - Client side routing allows your app to update the URL from a link click without making another request for another document from the server.
  - This enables faster user experiences because the browser doesn't need to request an entirely new document or re-evaluate CSS and JavaScript assets for the next page. It also enables more dynamic user experiences with things like animation.
    <br>

  ```
  import { Routes, Route } from "react-router-dom";
  import Home from './home';
  import Cart from './cart';

  const Shop = () => {
    return (
      <h1>I am the shop page</h1>
    )
  }


  const App = () => {
    return (
      <Routes>
        <Route path='/cart' element={<Cart />} />
        <Route path='/' element={<Home />}>
          <Route path='shop' element={<Shop />} />
        </Route>
      </Routes>
    )
  }

  export default App;
  ```

  - `<Routes>...</Routes>`:
    - `<Route element={<ComponentName />}/?>`: 
      - `index`: _bool_ if matching the parent url exactly, render this as default
      - Before React Router V6, use `component={...}` instead of `element={...}`
      <br>
      
  - **Nested routing: \<Outlet />**:

    - In `Route`: use `<Outlet />` representing passed-in nested component

    ```
    import { Routes, Route, Outlet } from "react-router-dom";
    import Home from "./routes/home";

    const Navigation = () => {
      return (
        <>
          <div>
            <h1>I am navigation bar</h1>
          </div>
          <Outlet />
        </>
      )
    }

    const Shop = () => {
      return <h1>I am the shop page</h1>
    }

    const App = () => {
      return (
        <Routes>
          <Route path='/' element={<Navigation />}>
            <Route path='home' element={<Home />} />
            <Route path='shop' element={<Shop />} />
          </Route>
        </Routes>
      )
    }

    export default App;
    ```

    <br>

  - `<Link to=... /?>`: works like anchor tag, but for React routers.

    - `to`: url relative to parent route, which means that it builds upon the URL path that was matched by the route that rendered that `<Link>`.

    <br>

##### **[Back to top](#react-notes)**

<br>

---

## Create-React-App

a packge created by facebook

- `npx create-react-app my-app-name`: create react project barebones with all the necessary files to run a SPA
- `react`: the engine that runs how does the app get built
- `react-dom`: directed towards web related application
  - `react-native`: for mobile application
- `react-scripts`:

#### In index.js

```
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementByID('root')
)
```

- `<React.StrictMode>`: enables followings
  - re-render an extra time to find bugs caused by **impure rendering**
  - re-run Effects an extra time to find bugs caused by missing **Effect cleanup**
  - check for usage of **deprecated APIs**
    <br>

##### **[Back to top](#react-notes)**

 <br>

---

## Redux:

- Having a store to save data for the component tree, and inject data to where it is needed, solve prop drilling problem
- Redux is an **opinionated** (specific syntax role, boilerplate, setup) state management library
- Based on **Flux** architechture: emphasize on <span>unidirectional</span> data flow
- **Won't use it if not need it**
- Redux itself is <span>synchorous</span>, any asynchronous process are done by other middleware like **redux-thunk**
- Observer pattern: the subject(an object), maintains a list of dependents that have subscribed to notifications of any updates(observers / listener), notifies them when state changes. Primarily in **event-driven** applications. (both React and Redux are based on Flux arch)

  <br>

  <span>Pros</span>:

  - 'Simplified' access to state across complex app
  - Better debugging: time travel
  - Simplified testing
  - A single source of truth (Redux Store)
    <br>

  Terms in redux:

  - **Action Creator**: function that creates action
    ```
    export const actionCreator = () => action;
    ```
  - **Action**: object containing action type and optional property, both names must matches with `reducer`.

    ```
    {
      type: actionType
      payload: actionPayload
    }
    ```

  - **Dispatcher**: function (send action to reducers)
  - **Reducer**: function (apply actions to state, update data, return new state), use reducer is the only way to change redux state.

    ```
    const reducer = (state = initialState, action) => {
      switch (action.type) {
        case type1: {
          // do something

          return {
            ...state,
            modifiedProp: modifiedValue
          }
        }

        case type2: {}

        ...

        default: {
          return state;
        }
      }
    }
    ```

    - **Never** mutate the original state, make a copy of it and make changes on the copy and return the copy
    - all fire when dispacth is invoked
    - initialized store

  - **Store**(s): object (nested, initialized and updated by reducers)
  - **views**: UI

  <br>

    <br>

- <span>Create reducer</span>:

  - create an obj to store initial state value
  - create a function taking two parameters: state and action
    - state default to initial state obj
  - Create a `switch` statement that checks the `action.type` and performs the logic to create the new state object
  - Return the new state. This will update the state in Redux and re-render subscribed React components.
    <br>

    ```
    // dispatch is a function in react-redux


    const initialState = {count : 0}

    function counterReducer (state = initialState, action) {
      switch (action.type) {
        case CHANGE_COUNT:
          return Object.assign({}, state, {key: action.payload});
        default:
          return state;
      };
    };
    ```

    <br>

- <span>Create store</span>:

  ```
  import { createStore } from 'redux';
  import { composeWithDevTools } from 'redux-devtools-extension';
  import reducers from './reducers';

  // adding composeWithDevTools here to get easy access to the Redux dev tools
  const store = createStore(
    reducers,
    composeWithDevTools()
  );

  export default store;
  ```

  - combine reducers into single function/object using `combineReducers` ( from redux )

    - import reducers from other files

    ```
    // reducers.js
    import { combineReducers } from 'redux';

    // import all reducers here
    import reducer1 from './reducer1';
    import reducer2 from './reducer2';


    // combine reducers
    const reducers = combineReducers({
      reducerOne: reducer1,
      reducerTwo: reducer2,
    });

    // make the combined reducers available for import
    export default reducers;
    ```

  - import the object returned by `combineReducers` and pass it into the `createStore`( from redux ) method from redux to create your store
    <br>

- <span>Make store available to React</span>:

  ```
  import { Provider } from 'react-redux';
  import store from './store';
  ...
  <Provider store={store}>
    <App />
  </Provider>
  ```

  - Import `Provider` from react-redux, the store from store.js, and your top level component.
  - Wrap your top level component in the `Provider` (from react-redux) component
  - Pass the store as a attribute to the `Provider` component
    <br>

- <span>Access store from within components</span>:

  - `mapStateToProps`:

    ```
    const mapStateToProps = (state) => ({
      // find the intended property
      propName: state.prop;
      ...
    })
    ```

    - `mapStateToProps` receives `state`, return an obj listing any properties of state that the component want to subscribe to.
    - keys in return obj will be passed on as props to the component they are connected to
    - access props property use `this.props.key`
      <br>

  - `mapDispatchToProps`: inject actions to props

    ```
    const mapDispatchToProps = (dispatch) => ({
      // actionCreator will generate an action based on the input value
      actionName: ([input]) => dispatch(actionCreator([input]))
      ...
    })
    ```

    - `dispatch` : a function, passed in `mapDispatchToProps` as input parameter and accept action

      ```
      dispatch ({ type: CHANGE_count, payload: 5 });
      ```

    - `mapDispatchToProps` can be object with handlers or function that return the object containing the handles
      - `mapDispatchToProps` receives dispatch as a argument and return an obj containing event handlers
      - returned obj consist of event handlers as keys and function definition as value.
    - event handler can pass dispatches to reducer
    - when invoke, these event handlers will dispatch actions, by invoking action creator which will return action objects, which are passed into dispatch
    - access event handler use `this.props.eventhandler`
      <br>

  - `connect`: connect store with class component
    ```
    import { connect } from 'react-redux';
    ...
    export default connect([mapStateToProps], [mapDispatchToProps])(ComponetName)
    ```
    - This ties our component to the redux store.
    - receives `mapStateToProps` and `mapDispatchToProps` as input (both optional) and return a function that takes component as input
    - if `mapDispatchToProps` is null, then inject `dispatch` methods to `props`.
      <br>

- <span>Write action creators</span>:

  - Create a file and export constant variables that represent all of the ways we want to change state. These will be the values passed as the type properties in your action objects.
  - All processing of side effects (ajax calls) should be handled in Action Creators. Once all the data necessary to facilitate the state change is derived, the value should be passed as the payload in your action objects. ○ In order to implement asynchronous functionality in Redux, you’ll need to employ middleware like redux-thunk or redux-saga
  - Each Action Creator should return an action object (which will be passed to dispatch, which will invoke your reducers)

    <br>

- <span>put on UI</span>:

  - use render(components, HTMLelement) (from react-dom)
    <br>
  - presentational component vs container component
    - if component is connected to the store
      <br>
  - use Hooks as a more popular method instead of `mapStateToProps`

<span>Class vs Functional</span>

- Class: use `connect`, `mapStateToProps`, `mapDispatchToProps`, `porps.dispatch`,
- Functional: use `useSelector` (over `useStore`), `useDispatch`
  <br>

<span>Redux-thunk</span>
Thunk is a redux middleware, and it adds asynchronous to redux by interacting with a Redux store's `dispatch` and `getState` methods.

- **Thunk function**:

##### **[Back to top](#react-notes)**

 <br>

---

## Webpack

Module/Code bundler

- reason to use:

  - **uglifying** and **minifying**: save resources
  - can use Modularity, which prevents global namespace polluting, and converts to one file ( bundle.js ) when uploading
  - can use newest tech for building: e.g., can transfer JSX to JS, Html, and CSS

- Modules: <span>Common JS (CJS) vs ES6 modules (ESM)</span>

  - CJS: `require` & `module.exports`
    - Node.js modules:
      - three types: **Modules you write**, **build-in**, **community npm**
      - all based on `require` and `module.exports`
  - ESM: `import` & `export`

    - mostly use in frontend ( <span>React</span> application)
    - can `export` multiple things
    - also has `export default`:

    ```
    // fruits.js
    export default Apple = props => {};
    export const Banana = props => {};
    export const Cherry = props => {};

    // fruit_stand.js
    import fruitOne from 'fruits; // fruitOne is Apple
    import fruitOne, * as myModule from 'fruits'; // fruitOne is still Apple, myModule is { Apple, Banana, Cherry }
    import fruitOne, { Cherry } from 'fruits'; // Cherry is Cherry
    ```

- webpack bundling starts in the terminal and gives an entry point

  - `npm run bundle`
  - `dist/main.js`
  - webpack loaders
    - babel-loaders: for transpiling JS code
    - css-loaders: for modulaized CSS
  - webpack plugins: do things loaders cannot do
    - minifying code: stripping whitespaces
    - uglifying code: code download faster
  - webpack-dev-server

    - live-reloading
    - won't create bundle.js, instead save it in memory
    - in development, usually utilize two server:
      - webpack-dev-server: localhost:8080
      - express server: localhost:3000

  - node react set up:
    - commands: (could repalce `-D` for `--save-dev`)
      ```
      npm install react
      npm install react-dom
      npm install webpack --save-dev
      npm install webpack-cli --save-dev
      npm install webpack-dev-server --save-dev
      npm install @babel/core --save-dev
      npm install babel-loader --save-dev
      npm install @babel/preset-react --save-dev
      npm install @babel/preset-env --save-dev
      npm install html-webpack-plugin --save-dev
      ```
    - script:
      ```
       "dependencies": {
          "react": "^18.2.0",
          "react-dom": "^18.2.0"
        },
        "devDependencies": {
          "@babel/core": "^7.20.12",
          "@babel/preset-env": "^7.20.2",
          "@babel/preset-react": "^7.18.6",
          "babel-loader": "^9.1.2",
          "html-webpack-plugin": "^5.5.0",
          "webpack": "^5.75.0",
          "webpack-cli": "^5.0.1",
          "webpack-dev-server": "^4.11.1"
        }
      ```

## React

- [Docs](https://reactjs.org/docs/getting-started.html)
- component is essentially function
- component:

  - splite UI into independent, reusable pieces
  - a component represent a part of DOM
  - component can have **DOM** elements
  - component can have other component inside
  - need to npm install react and import before use
  - use class to create React component
  - class need to `extends React.Component`
    <br>

### Component Class:

- in class, `render() {}` is a special method and it will show whatever is being returned on the DOM
  <br>
- child component can set parameters on `{this.props}` object in the return DOM element statement, e.g., `return <h1>Hello, {this.props.childComponentlaber}</h1>;`
- parent component can use `<childComponent childComponentlaber = data />` to assign data value to the parameter in the parent component
  <br>
- Class component with constructor and `this.state` could use `{this.state.propertyName}` to access data in its own state
  <br>
- Methods can be defined inside of
- may need other library (npm & import)
  <br>

- **JSX**: javascript XML (file name): precompiled syntax exntension to JS, React 'element' can be rendered into HTML element on DOM by JSX
  - e.g., `<h1>Hello, {this.props.anykeylabel}</h1>`
  - could have js inside of DOM element, wrapped in `{}`
    - `<h1>{2 + 2}</h1>`
    - `<p{user.firstName}`
    - `{formatName(user)}`
  - JSX attribute: key value pair: used to pass in data
    - for component attributes, could use `'for string'` or `{js expression}`, one or another
    - in child component, use `this.props.childVariable`
    - in parent component, use `childVariable = {js exoression}`
  - JSX can interpret an array of JSX statements and take each individule out e.g., `{boxes}`
    <br>
- **State**: top down, uni-directional data flow, used to pass data
  - accessible and easily maintained
  - **State** maintained in top level components (as an obj called `State`) and passed down (through `props`) to child component
  - `props` never go upstream or to sibling component.
  - values in props are **immutable**
  - use `setState()` in order to update **State**, **never** manually set `state`.
  - only use `setState()` where `state` is defined
  - `setState()` will only update what is passed in, the rest stay the same
  - Any changes to the state will trigger an update, or "re-render", of components that depends on it.
    <br>
- virtual DOM: representing DOM elements purely in a lightweight JS form.
  - use **React-DOM** library,
  - achieve fast render time
  - React processes changes very quickly, only rendering to the real DOM when and where needed.

### ReactComponent: Class vs Function Declaration vs ES6 Function Expression

- **Class**:
  - **Life cycle component**: if the function definition is given in the component class
    - `componentDidMount(){ /.../ }`: this will run the **first time** component is rendered on the DOM
    - `componentDidUpdate(){ /.../ }`: this will run **after updating** is complete, but not for the initial rendering
    - `componentWillUnmount( /.../ )`: this will run **before the removal** of rendered Box from DOM
  - **Can have state**
    <br>
- **Stateless Functional Component**

  - Pros:
    - No need to use `this` keyword! You don't have to deal with `state` / `methods`, and your `props` are passed in as a parameter.
    - Less boilerplate. As your component is simply a function, free of the constraints of a React component class, the amount of boilerplate in creating a stateless functional component is greatly reduced. This makes it so the resulting code for you component is concise and and clear.
    - Clearly separates your concerns. This is important when you're separating your application into container and presentational components.
  - Cons
    - No access to component lifecycle methods (ie `ComponentDidMount`).
      <br>

- **Higher-Order Components**
  - a higher-order component is a function that takes a component and returns a new component.

**React Hooks**: functions that allow functional components the ability to do things that were typically only reserved for class components.
<br>

### React Hooks

- ==useState==: state and the function that can changed the state
  - make sure the passed-in ==reference is different== from the original state reference
  - use a new reference or use spread syntax
  ```
  const [state, updateState] = React.useState('initial state');
  console.log(state); // 'initial state'
  console.log(updateState); // 'Function(){}' that can be used to update that state, it accepts a new state value and enqueues a re-render of the component.
  updateState('next state'); // update the state
  ```
- ==useEffect==: Equivalent of lifecycle methods

  - Needs to do something **after render** (initial or update).
  - `[dependencies]`, only run if dependencies changed
  - if `[dependencie]` omitted, only run for the initial render

  ```
  React.useEffect(() => {
    console.log('component updated');
  },[dependencies])
  ```

- ==useMemo==: cache the result of a calculation between re-renders.

  - first parameter is the function that calculating the value, should take no input and return a value
  - second parameter is the array of dependencies that triggered the useMemo
  - useMemo will return previous value if dependencies are the same for rerender

  ```
  const cachedValue = React.useMemo(calculateValue, [dependicies])

  ```

  useMemo hook common cases:

  1. make a slow function wrap inside useMemo so that doesn't re-compute for every re-render
  1. make sure the reference of an object or an array is exactly the same as it was in the last rendered
     <br>

- ==useCallback==: cache a function definition between re-renders.

  - just like useMemo, but it return the first paramenter, which is the entire function, instead of the return value of the function, and the function could have input

  ```
  const [number, setNumber] = useState(1);

  // below will reassign to getItems function for other unrelated re-render
  const getItems = () => {
    return [number, number + 1, number + 2]
  }

  // below will not recreate getItems function for re-render if number doesn't change
  const getItems = React.useCallback(() => {
    return [number, number + 1, number + 2]
  }, [number])
  ```

  useCallback hook common case:

  1. make sure the reference of an function is exactly the same as it was in the last rendered, such as passing function to child component
  1. for some reason creating a function is really slow for each re-render (rarely)
     <br>

- ==useContext==: lets you read and subscribe to context from your component

  - Context lets the parent component make some information available to **any** component in the tree below it—no matter how deep—without passing it explicitly through props.
  - The context is created by `createContext` function (`React.createContext()`)
    - if no defaultValue, specify `null`
    - return a context object that doesn't hold any information, it represents which context other components read or provide.

  ```
  // In contextcreator file (could also integrated in parent component file)
  // call createContext to create a context and export it
  import { createContext } from 'react';

  export const SomeContext = createContext(defaultValue)

  ------------------------------------------------------------------------------------------------------------

  // In parent component 
  import { useState } from 'react';
  import { SomeContext } from '[path to contextCreator file]';
  import Child from '[path to ChildComp file]';

  function ParentComp(props) {
    const [someState, setSomeState] = useState(someValue)       // where state is created, usually from other hooks
    return (
      <SomeContext.Provider value={[someState, setSomeState]}>   // where state is provided to all child 
        <Child>                                                  // compnents, can be any value (array, obj)
      </SomeContext.Provider value={someState}>
    )
  }

  ------------------------------------------------------------------------------------------------------------

  // In child component 
  import { useContext } from 'react';
  import { SomeContext } from '[path to contextCreator file]';

  function Child(props) {
    const [someState, setSomeState] = useContext(SomeContext);                    // where state is being used 
    return (
      <>
        {...}
      </>
    )
  }
  ```
<br>

- useReducer

<br>

- ==useRef==: reference a value that’s not needed for rendering.
  ```
  const ref = useRef(initialValue);
  ```
  - return: an object with a single property: `{ current: initialValue }`
  - `initialValue`: the value ref object's current property to be initialled. This value is ignored after ref initialization.
  - change ref value: `ref.current = newValue`, changing it does not trigger a re-render, so refs are not appropriate for storing information you want to display on the screen
  - It’s particularly common to use a ref to ==manipulate the DOM==. React has built-in support for this.
    - first initial ref to null `const inputRef = useRef(null);`
    - Then pass your ref object as the ref attribute to the JSX of the DOM node you want to manipulate: `return <input ref={inputRef} />;`
    - After React creates the DOM node and puts it on the screen, React will set the `current` property of your ref object to that DOM node: `inputRef.current.focus();`
    - React will set the current property back to null when the node is removed from the screen.
  

  <br>

  React Problem: props drilling

### When does rerender trigger

Initial render: when a component first appears on the screen

1. The props passed in component changed
1. Internal state change (useState)
1. Parent component rerendered (unless React.memo() is called for a component)

## Redux:

- having a store to save data for the component tree, and inject data to where it is needed, solve prop drilling problem
- redux is an **opinionated** (specific syntax role, boilerplate, setup) state management library
- based on **Flux** architechture: emphasize on ==unidirectional== data flow
- **Won't use it if not need it**
  <br>
  pros:

- 'simplified' access to state across complex app
- better debugging: time travel
- simplified testing
- a single source of truth (Redux Store)
  <br>
  vocabulary in redux:

  - **Action Creator**: function (create action)
  - **Action**: object {type(reserved key):....[, payload(**not** reserved key): ....]}
  - **Dispatcher**: function (send action to reducers)
  - **Reducer**: function (apply action to state, update data, return new state)
    - `f(state = initialState, action) = new state`
      - cannot mutate the original state, make a copy of it and make changes on the copy and return the copy
    - all fire when dispacth is invoked
    - initialized store
  - **Store**(s): object (nested, initialized and updated by reducers)
  - **views**: UI

    <br>

- observer pattern: the subject(an object), mainetains a list of dependents that have subscribed to notifications of any updates(observers / listener), notifies them when stae changes. Primarily in **event-driven** applications. (both React and Redux are based on Flux arch)
  <br>

  <br>

  - `dispatch` : a function, passed in mapDispatchToProps as input parameter and accept action

  ```
  const mapDispatchToProps = dispatch => ({
    addMarket: (location) => dispatch(actions.addMarketActionCreator(location)),
    addCard : (id) => dispatch(actions.addCardActionCreator(id)),
    deleteCard : (id) => dispatch(actions.deleteCardActionCreator(id)),
  });
  ```

    <br>

Create reducer:

- create an obj to store initial state value
- create a function taking two parameters: state and action
  - state default to initial state obj
- Create a switch statement that checks the `action.type` and performs the logic to create the new state object
- Return the new state. This will update the state in Redux and re-render subscribed React components.
  <br>

  ```
  // dispatch is a function in react-redux
  dispatch ({ type: CHANGE_count, payload: 5 });

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

Create store:

- combine reducers into single function/object using `combineReducers` ( from redux )
  - import reducers from other files
- import the object returned by `combineReducers` and pass it into the `createStore`( from redux ) method from redux to create your store
  <br>

Make store available to React:

- Import `Provider` from react-redux, the store from store.js, and your top level component.
- Wrap your top level component in the `Provider` (from react-redux) component
- Pass the store as a attribute to the `Provider` component
  <br>

Access store from within components:

- `mapStateToProps`:

  - `mapStateToProps` receives `state`, return an obj listing any properties of state that the component want to subscribe to.
  - keys in return obj will be passed on as props to the component they are connected to
  - access props property use `this.props.key`

    <br>

- `mapDispatchToProps`:

  - `mapDispatchToProps` receives dispatch as a argument and return an obj containing event handlers
  - returned obj consist of event handlers as keys and function definition as value.
  - event handler can pass dispatches to reducer
  - when invoke, these event handlers will dispatch actions, by invoking action creator which will return action objects, which are passed into dispatch
  - access event handler use `this.props.eventhandler`
    <br>

- `connect` (from react-redux):
  `
  - This ties our component to the redux store.
  - receives `mapStateToProps` and `mapDispatchToProps` as input ans return a function that takes component as input
  - `export default connect(mapStateToProps, mapDispatchToProps)(Component)`
    <br>

Write action creators:

- Create a file and export constant variables that represent all of the ways we want to change state. These will be the values passed as the type properties in your action objects.
- All processing of side effects (ajax calls) should be handled in Action Creators. Once all the data necessary to facilitate the state change is derived, the value should be passed as the payload in your action objects. ○ In order to implement asynchronous functionality in Redux, you’ll need to employ middleware like redux-thunk or redux-saga
- Each Action Creator should return an action object (which will be passed to dispatch, which will invoke your reducers)

  <br>

put on UI:

- use render(components, HTMLelement) (from react-dom)
  <br>
- presentational component vs container component
  - if component is connected to the store
    <br>
- use Hooks as a more popular method instead of `mapStateToProps`

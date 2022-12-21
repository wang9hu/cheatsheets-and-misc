React

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

  Component Class:

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

- JSX: javascript XML (file name): precompiled syntax exntension to JS, React 'element' can be rendered into HTML element on DOM by JSX
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
- State: top down, uni-directional data flow, used to pass data
  - accessible and easily maintained
  - **State** maintained in top level components (as an obj called `State`) and passed down (through `props`) to child component
  - `props` never go upstream or to sibling component.
  - values in props are **immutable**
  - use `setState()` in order to update **State**, **never** manually set `state`.
  - only use `setState()` where `state` is defined
  - Any changes to the state will trigger an update, or "re-render", of components that depends on it.
    <br>
- virtual DOM: representing DOM elements purely in a lightweight JS form.
  - use **React-DOM** library,
  - achieve fast render time
  - React processes changes very quickly, only rendering to the real DOM when and where needed.

ReactComponent: Class vs Function Declaration vs ES6 Function Expression

- Class:
  - **Life cycle component**: if the function definition is given in the component class
    - `componentDidMount(){ /.../ }`: this will run the **first time** component is rendered on the DOM
    - `componentDidUpdate(){ /.../ }`: this will run **after updating** is complete, but not for the initial rendering
    - `componentWillUnmount( /.../ )`: this will run **before the removal** of rendered Box from DOM
  - **Can have state**
    <br>
- Stateless Functional Component
  - Pros:
    - No need to use `this` keyword! You don't have to deal with `state` / `methods`, and your `props` are passed in as a parameter.
    - Less boilerplate. As your component is simply a function, free of the constraints of a React component class, the amount of boilerplate in creating a stateless functional component is greatly reduced. This makes it so the resulting code for you component is concise and and clear.
    - Clearly separates your concerns. This is important when you're separating your application into container and presentational components.
  - Cons
    - No access to component lifecycle methods (ie `ComponentDidMount`).
      <br>

React Hooks: functions that allow functional components the ability to do things that were typically only reserved for class components.
<br>
**Basic hooks**:

- useState: state
  ```
  const [state, updateState] = React.useState('initial state');
  console.log(state); // 'initial state'
  console.log(updateState); // 'Function(){}' that can be used to update that state, it accepts a new state value and enqueues a re-render of the component.
  updateState('next state'); // update the state
  ```
- useEffect: Equivalent of lifecycle methods:

  ```
  React.useEffect(() => {
    console.log('component updated');
  })
  ```

  <br>

  React Problem: props drilling

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
    - f(cur state, action) = new state
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

  - This ties our component to the redux store.
  - receives `mapStateToProps` and `mapDispatchToProps` as input ans return a function that takes component as input
  - `export default connect(mapStateToProps, mapDispatchToProps)(Component)`
    <br>

Write action createors:

- Create a file and export constant variables that represent all of the ways we want to change state. These will be the values passed as the type properties in your action objects.
- All processing of side effects (ajax calls) should be handled in Action Creators. Once all the data necessary to facilitate the state change is derived, the value should be passed as the payload in your action objects. ○ In order to implement asynchronous functionality in Redux, you’ll need to employ middleware like redux-thunk or redux-saga
- Each Action Creator should return an action object (which will be passed to dispatch, which will invoke your reducers)

  <br>

put on UI:

- use render(components, HTMLelement) (from react-dom)

- presentational component vs container component
  - if component is connected to the store

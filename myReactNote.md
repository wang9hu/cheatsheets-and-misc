React

- [Docs](https://reactjs.org/docs/getting-started.html)
- component is essentially function
- component:
  - splite UI into independent, reusable pieces
  - a component represent a part of DOM
  - component can have DOM elements
  - component can have other component inside
  - need to npm install react and import before use
  - use class to create React component
  - class need to `extends React.Component`
  - in class, `render() {}` is a special method and it will show whatever is being returned on the DOM
  - set parameter in child component on `{this.props}` object in the return DOM element statement, e.g., `return <h1>Hello, {this.props.anykeylabel}</h1>;`
  - use `<childComponent anykeylaber = data />` to assign parameter with data in the parent component
  - may need other library (npm & import)
    <br>
- JSX: javascript XML (file name): precompiled syntax exntension to JS, React 'element' can be rendered into HTML element on DOM by JSX
  - e.g., `<h1>Hello, {this.props.anykeylabel}</h1>`
  - could have js inside of DOM element, wrapped in {}
  - JSX attribute: key value pair: used to pass in data
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
  - life cycle component
  - have state
- Stateless Functional Component
  - Pros:
    - No need to use this this keyword! You don't have to deal with state / methods, and your props are passed in as a parameter.
    - Less boilerplate. As your component is simply a function, free of the constraints of a React component class, the amount of boilerplate in creating a stateless functional component is greatly reduced. This makes it so the resulting code for you component is concise and and clear.
    - Clearly separates your concerns. This is important when you're separating your application into container and presentational components.
  - Cons
    - No access to component lifecycle methods (ie ComponentDidMount).
-

React Hooks: functions that allow functional components the ability to
do things that were typically only reserved for class components.

- useState: state
  ```
  const [state, updateState] = React.useState('initial state');
  console.log(state); // 'initial state'
  console.log(updateState); // 'Function(){}' that can be used to update that state, it accepts a new state value and enqueues a re-render of the component.
  updateState('next state'); // update the state
  ```
- useEffect: Equivalent of lifecycle methods:
  - componentDidMount
  - componentDidUpdate
  - componentWillUnmount
  ```
  Reach.useEffect(() => {
     console.log('component updated');
  })
  ```

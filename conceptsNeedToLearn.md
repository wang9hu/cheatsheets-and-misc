1. type coersion
   <br>
1. set
   <br>
1. map
   <br>
1. linkedlist
   - singly
   - doubly
1. hash table
   <br>
1. binary search tree
   - can't have duplicate values
     <br>
1. benefit of recursion
   <br>
1. DRY principle: don't repeat yourself
   <br>
1. Class variable declaration: where should it be and why it cannot be in class definition scope outside of constructor
   <br>
1. So in normal constructor function, we use `this.newProp = ....` to declare the variables inside of the object that is constructed by this constructor.

So, in the class constructor, `this.FunctionName = this.method.bind(this)`, works similarly, the first `this.FunctionName` is sort of like declaring a variable for the component constructed by this class, but we don't actually use it as a component property, we just declare it so that we can still access it inside of class definition but outside of class constructor. The second `this` is referring to the class itself, so `this.method` is the method that is defined in the class definition but outside of constructor. The third `this` is, again, referring to the component that is about to be constructed by the class. (for now we haven't use the properties outside of the class definition after component is constructed)
Overall this statement means that you are binding the component (that is going to be constructed by the class) to the method (that is declared in the class), and assign the 'binded function' to be as another property of the component.

```
// define a Class called ClassName
class ClassName {
   constructor() {
      this.name = 'xiao';

      // the two methods below are both from the same 'consoleThis' method, the difference is that one binds with 'this'
      this.consoleNoBindThis = this.consoleThis;
      this.consoleBindThis = this.consoleThis.bind(this);
   }

   consoleThis() {
      console.log(this)
   }
}

// create a ClassName instance
const classInstance = new ClassName();

// if invoke directly from ClassName instance, both methods works the same
classInstance.consoleNoBindThis(); // ClassName { name: 'xiao', consoleBindThis : ƒ, consoleNoBindThis : ƒ }
classInstance.consoleBindThis(); // ClassName { name: 'xiao', consoleBindThis : ƒ, consoleNoBindThis : ƒ }

// reassign both instance methods to global variables
const newConsoleNoBindThis = classInstance.consoleNoBindThis;
const newConsoleBindThis = classInstance.consoleBindThis;

// the one doesn't bind with 'this' will give 'undefined', and the one bind with 'this' still work the same as before
newConsoleNoBindThis(); // undefined
newConsoleBindThis(); // ClassName { name: 'xiao', consoleBindThis : ƒ, consoleNoBindThis : ƒ }
```

<br>
- use import and export to split code in different jsx files
<br>
- {boolean evaluate statement && (<component to be renderred/>)}
<br>

## Sass

- variables
- functions

## CSS

- grid-template-column: repeat(autofill, .....)

## SQL

- composite key

## Authentication

- encryption vs hashing
- Bcrypt: a hashing algorithm
  - salt: random add-on characters
  - work factor: how many times hash function is going to run

## Authorization

- Clearly define which users are allowed to access which resources.
- Ensure these rules are consistently enforced throughout your
  application.
- Always follow the **principle of least privilege** when deciding what users should have access to

## Cookie:

a small string created by the server and stored in the browser/database

- each domain has its own 'cookie storage'
- ~50 cookies per domain, ~3000 total in browser
- Any cookies stored for a specific domain are sent with every HTTP request to that domain’s server.
  <br>
  types of cookies:(one, more or none)the server set up cookies metadata when creating the cookie
- Persistent (tracking cookie)
- Secure
- HttpOnly

## localStorage

- Use the HTML5 localStorage object as an alternative to cookies.
- It is stored on the browser’s window object
- Each domain has its own storage.
- Stores strings, but you get 5 MB of storage per domain.
- Values persist forever.

## sessionStorage

- similar to localStorage
- do not persist. will clear out when tab instance closes

## JSON Web Token (JWT [jot])

- Token authentication is an approach used in place of session authentication to lower the load on your server.
- JWT defines a compact and self-contained way for transmitting information between parties as a JSON object that are integrity protected through a signature.
- JWT allow use to avoid continually querying a database to authorize users, created by the server and send back to browser,
  - payload: contains user information as JSON object
  - signature: used to confirm the validity of the payload, essentially a one-way hash of payload plus a secret stored on the server

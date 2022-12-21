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

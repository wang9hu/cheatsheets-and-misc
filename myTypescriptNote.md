# TypeScript

- [TypeScript](#typescript)
  - [Types](#types)
    - [TypeScript basic types](#typescript-basic-types)
    - [TypeScript new primitive types](#typescript-new-primitive-types)
    - [Enum](#enum)
    - [Arrays](#arrays)
    - [Tuple](#tuple)
    - [Type Alias](#type-alias)
    - [Interfaces](#interfaces)
    - [Union Type](#union-type)
    - [Intersection Type](#intersection-type)
    - [Literal Type](#literal-type)
    - [Object](#object)
    - [Functions](#functions)
    - [Class](#class)
    - [Type Manipulation](#type-manipulation)
      - [Generics](#generics)
      - [The `keyof` type operator](#the-keyof-type-operator)
      - [The `typeof` type operator](#the-typeof-type-operator)
      - [The Indexed Type operator](#the-indexed-type-operator)
      - [The Conditional Types](#the-conditional-types)
      - [The Mapped Types](#the-mapped-types)
      - [Template Literal Types](#template-literal-types)
    - [Untility TYpes](#untility-types)
  - [Concepts](#concepts)
      - [Type assertion](#type-assertion)
      - [types.d.ts](#typesdts)
      - [import type](#import-type)
  - [Topics to check later](#topics-to-check-later)

<br>

**Benefits**:

- Static typing
  - statically-typed language: C++, C#, Java, Golang...
  - dynamically-typed language: Javascript, Python, Ruby...
- Code completion
- Refactoring
- Shorthand notation

**Drawbacks**:

- Compilation
  - Transpilation: .ts -> Compiler -> .js
- Discipline in coding (good for medium to large projects)
  <br>

**Environment setup:**

- terminal:
  - `npm i -g typescript` // install typescript
  - `tsc -v` // check typescript version
  - `tsc filename.ts` // to transpile filename.ts and create a filename.js
  - `tsc` // compile all the ts file
- `.ts`:
  - let variable: type = value;
    - `let age: number = 20`;
- `.d.ts`: type declaration files, only contain type information used for type checking.
  <br>

- **Configure typescript compiler**:
  - in terminal: `tsc --init` // create a tsconfig.json file, in it:
    - Language and Environment sesson:
      - `"target": "ES2016"` // version of JS complier is going to generate, can be changed depends where the application is going to run
        <br>
    - Module Session:
      - `"module" : "commonjs"` //
        - `"rootDir": "./src"` // specifies the directory that contains source files (ts files), current dir is where tsconfig.json is.
          <br>
    - Emit Session:
      - `"outDir": "./dist"` // directory that contains the generated js files
      - `"removeComments": true` // if true, compiler will remove all the comments in ts when compiling.
      - `"noEmitOnError": true` // if true, compiler will not generate js file if any error during compiling.
        <br>
    - Type Checking Session:
      - `"noImplicitAny": true` // if true, typescript will not allow implicit `any` type
        <br>
      - `"noUnusedParameters": true` // if true, typescript will warn if there is any unused parameters in function.
      - `"noImplicitReturns": true` // if true, typescript will warn if function have no explicit return.
      - `"noUnusedLocals": true` // if true, typescript will warn if function have a unused variable
        <br>
      - `"strictNullChecks": true` // if `"strict": true`, this will be true. If overwrite it with `false`, `null` and `undefined` will not be checked for types

<br>

- If only use `let` without assignment, variable will have the type of `any`, (<span>Not recommanded</span>).

- when using parameters in a function, if not explicitly annotate the type, and typescirpt will generate a error.
  - Two ways to solve this: give parameters `any` type or turn `noImplicityAny` to `false` in tsconfig.json
  <br>

## Types

### TypeScript basic types 
`number`, `string`, `boolean`, `null` and `undefined`

- No type notation is needed cause compiler will figure it out based on the value (**implicit** type assignment)

  ```
  // below is explicit types
  let num: number = 5;
  let course: string = 'TypeScript';
  let is_done: boolean = 'true';

  // below is implicit types
  let num = 5;
  let course = 'TypeScript';
  let is_done = 'true';
  ```
- Number(`number`): large number can be seperated using `_`: 
  `let num: number = 123_456_789;`


### TypeScript new primitive types 
`any`, `unknown`, `never`, `void`, `object`, `Function`

- `any`: if not assigned any type, it will be `any` type, meaning it could be **anything**, so TS will give no error or warning on any operation of that variable, it **disables type checking** for that variable. This is useful when you don’t want to write out a long type just to convince TypeScript that a particular line of code is okay.

- `unknown`: unlike `any`, TS restricts any operations on `unknown` variable, useful when **multiple types are accepted** for one variable, and use **conditional check** to narrow it down for one particular type.
  ```
  let val: unknown = 1;

  // Errors: below would have type checking error
  val++;
  val.toUpperCase();
  val.map(callback);
  val.foobar = 2;
  tomorrow(val);

  // below works fine
  if (typeof val === 'number') val++;
  if (typeof val === 'string') val.toUpperCase();
  if (Array.isArray(val)) val.map(callback);
  if (val && 
      typeof val === 'object' && 
      'foobar' in val && 
      typeof val.foobar === 'number'
  ) val.foobar = 2;
  if (val instanceof Date) tomorrow(val); // assuming tomorrow accept a Date type as input
  ```
- `never`: no meaningful value can assign to a `never` type of variable. Useful in two ways: 
  1. customizing a type, a `never` type shows up on the variable indicating there is a mistake; 
      ```
      // both types below are in never type
      type A = number & string;
      type B = boolean & null;
      ```
  1. conditional filtering types, use a `never` type to check if the target variable exhausts all possible types.
      ```
      type User = 'standard' | 'admin';

      // will have type checking error if User have "| 'owner'" appended.
      function login(user: User) {
        switch (user) {
          case: 'standard':
            return true;
          case: 'admin':
            return true;
          default: 
          // if 'owner' in User, then user below will have type 'owner' instead of 'never', so a missing case can be found.
            const _unreachable: never = user; 
            throw 'wrong user type';
        }
      }
      ```
      <br>
- `void`: represents the return value of functions which don’t return a value. 
  - It’s the inferred type any time a function doesn’t have any return statements, or doesn’t return any explicit value from those return statements
  ```
  function noop() {
    return;
  }
  const res = noop(); // res has type void
  ```
  - Not same as `undefined` in TS, if implementated in function signature, the return value will retain type `void` no matter what type it originally is
  ```
  type voidFunc = () => void;
  const f1: voidFunc = () => {
    return true;
  };
  const f2: voidFunc = () => 'a';
  const f3: voidFunc = function () {
    return 3;
  };

  const v1 = f1(); // v1 has value of true, but void type
  if (v1) ...// this will error due to "An expression of type 'void' cannot be tested for truthiness."

  const v2 = f2(); // v2 has value of 'a', but void type
  v2.length // this will error due to "Property 'length' does not exist on type 'void'."

  const v3 = f3(); // v1 has value of 3, but void type
  v3 + 1; // this will error due to "Operator '+' cannot be applied to types 'void' and 'number'."
  ```
  <br>

  - If literal function definition has a `void` return type, that function must not return anything.
  ```
  // below will give error
  function f2(): void {
    return true; 
  }
  ```
  <br>

### Enum 
  
`enum`: associate a set of **named constants** with **values**, and make it a type for a variable that could be one of the values.
- use comma to seperate different name;
  ```
  enum ExampleType { 
    keyword1, 
    keyword2, 
    keyword3 = 7, 
    keyword4, 
    keyword5 = 'a', 
    keyword6 = '123'.length
  }
  ```
  - By default, number starts with `0` and increase from there
  - can be assigned with other values or expression (**evaluted to be either number or string**), but if value is not `number`, the keywords after it must also have initializor.
  - `ExampleType.keyword#` from 1 to 6: `0`, `1`, `7`, `8`, `a` and `3`

    ```
    // after compilation, it just did this
    "use strict";
    var ExampleType;
    (function (ExampleType) {
        ExampleType[ExampleType["keyword1"] = 0] = "keyword1";
        ExampleType[ExampleType["keyword2"] = 1] = "keyword2";
        ExampleType[ExampleType["keyword3"] = 7] = "keyword3";
        ExampleType[ExampleType["keyword4"] = 8] = "keyword4";
        ExampleType["keyword5"] = "a";
        ExampleType[ExampleType["keyword6"] = '123'.length] = "keyword6";
    })(ExampleType || (ExampleType = {}));

    console.log(ExampleType); 
    // console it out, will get below
    {
      "0": "keyword1",
      "1": "keyword2",
      "3": "keyword6",
      "7": "keyword3",
      "8": "keyword4",
      "keyword1": 0,
      "keyword2": 1,
      "keyword3": 7,
      "keyword4": 8,
      "keyword5": "a",
      "keyword6": 3,
    } 
    ```
- problems about `enum`:
  1. for string type `enum`, assigning with the same string from the type would still give errors on type checking 
    ```
    enum Fruit {
      X = 'apple',
      Y = 'banana',
    }

    // a is fine but b would give error
    const a: Fruit = Fruit.X;
    const b: Fruit = 'apple';
    ```
  2. for number type `enum`, assigning with numbers out of the type scope would not give errors (This is fixed on typescript version 5.2)
- In modern TypeScript, you may not need an `enum` when an object with `as const` type assertion could suffice:
  <br>

### Arrays

- TS can annotate the array element type (two ways)
  - `let numbers: number[] = [1, 2, 3]`
  - `let numbers: Array<number> = [1, 2, 3]`
- add `readonly` to prevent arrays from being changed:
  - `let numbers: readonly number[] = [1, 2, 3]`
- if assigned value is an array of same types, then the type annotation of the variable can be omitted: `let numbers = [1, 2, 3]`
- if declare an empty array, it is better to apply a type annotation: `let numbers: number[] = []`
- and for typed array methods (like `forEach`), in its arrow function, typescript can show all the properties and methods of that type objects.

<br>

### Tuple

- a tuple is a typed array with pre-defined length and types:
  `let user: [number, string] = [33, 'age']`

  <br>

### Type Alias
 A name for any customized type, can be used for primitives and complex types

```
type Employee = {
  readonly id: number;
  name: string;
  fax?: string;
  retire: (date: Date) => void;
}
```

<br>

### Interfaces

- Share a lot usage like type alias, but have two distinctions:
  - Interfaces can only apply to **object types**
  - Interfaces can **extend** other interface's definition, while type alias can not.

```
interface Rectangle {
  height: number;
  width: number;
}

interface ColoredRectangle extends Rectangle {
  color: string
}
```

<br>

### Union Type
one or another
use `|` between types

```
function kgToLbs (weigth: number | string): number {
  // Narrowing
  if (typeof weight === 'number') return weight.[...] // will have all methdos for number object
  else return parseInt(weight) * 2.2
}

const numAndStr: (number | string)[] = [1, 'apple', 2, 'banana']
```
  - **Discriminated Union (or tagged union)**: a special type of union, there is an **identical** property in each variant as the **discriminant** (shared discriminative property), may has an  leading `|` (optional), useful in type checking and exhaustiveness checking. Also works great with `switch`

    ```
    {
      interface Circle {
        kind: "circle";
        radius: number;
      }

      interface Square {
        kind: "square";
        sideLength: number;
      }

      interface Triangle {
        kind: "triangle";
        base: number;
        height: number;
      }

      type Shape = Circle | Square | Triangle;

      /* -------------- or just below --------------- */


      type Shape = 
        | { kind: "circle", radius: number }
        | { kind: "square", sideLength: number }
        | { kind: "triangle", base: number, height: number }

    }

    function calculateArea(shape: Shape): number {
      switch (shape.kind) {
          case "circle":
              return Math.PI * Math.pow(shape.radius, 2);
          case "square":
              return shape.sideLength * shape.sideLength;
          case "triangle":
              return (shape.base * shape.height) / 2;
      }
    }
    ```

    - **Downside**: discriminant *must* be **literal types**, will not work on generic types

    ```
    type LoadingLocationState = {
      state: string
    }

    type SuccessLocationState = {
      state: number
      coords: { lat: number; lon: number }
    }

    type LocationState = LoadingLocationState | SuccessLocationState

    /*------- below couldn't rule out SuccessLocationStatte *---------/
    function printLocation(location: LocationState) {
      if (typeof location.state === 'string') {
        console.log(location)
      }
    }
    ```

<br>

### Intersection Type 
one and another
use `&` between types

```
type Draggable = {
  drag: () => void
};

type Resizable = {
  resize: () => void
};

type UIWidget = Draggable & Resizable;

let textBox: UIWidget = {
  drag: () => {},
  resize: () => {}
};
```

<br>

### Literal Type
exact, specific value as types

```
type Quantity = 50 | 100;
let quantity: Quantity = 100;

// practical use
type Metric = 'cm' | 'inch';
```

<br>

### Object

- when annotate type of an object, add a `?` after property indicating this property may not be shown in the object, or annotate normally and temporarily assign a empty string to it.
<br>
- properties without `?` must match the Object literal
<br>
- `readonly` can also apply to properties by adding in the front to make it unchangable

```
let emplyee: {
  readonly id: number;
  name: string;
  fax?: string;
  retire: (date: Date) => void;
} = {
  id: 1,
  name: '',
  retire: (date: Date) => {
    console.log(date)
  }
}
employee.name = 'xiao';
employee.fax = '123-456-7890';
```
<br>

- **Index Signatures** `{ [index: number]: string; }`: use this when the names of a type's properties are not known, but the shape of the values are known ahead of time.
  ```
  interface StringArray {
    [index: number]: string;
  }
  
  const myArray: StringArray = getStringArray();
  const secondItem = myArray[1]; 
  // This index signature states that when a StringArray is indexed with a number, it will return a string.
  ```
    - Only some types are allowed for index signature properties: **string**, **number**, **symbol**, **template string patterns**, and **union types consisting only of these**.
    - Index signatures enforce that **all properties** must match their return type
    ```
    interface NumberDictionary {
      [index: string]: number;
      length: number; // ok
      name: string; // Not ok, Property 'name' of type 'string' is not assignable to 'string' index type 'number'.
    }

    interface NumberOrStringDictionary {
      [index: string]: number | string;
      length: number; // ok, length is a number
      name: string; // ok, name is a string
    }
    ```
    - Index signatures can be readonly in order to prevent assignment to their indices:
    ```
    interface ReadonlyStringArray {
      readonly [index: number]: string;
    }
    
    let myArray: ReadonlyStringArray = getReadOnlyStringArray();
    myArray[2] = "Mallory"; // Error: Index signature in type 'ReadonlyStringArray' only permits reading.
    ```
    <br>
    
- **Optional Chaining**:

  - use `?.` to access the property that may or may not exist, return `undefined` if not.
  - this can also be used with array if the target array may or may not exist
  - this can also be used with function if the function may or may not match the invocation.

  ```
  type Customer = { birthday: Date }

  function getCustomer(id: number): Customer | null | undefined {
    return id === 0 ? null : { birthday: new Date() }
  }

  console.log(getCustomer(0)?.birthday); // undefined
  console.log(getCustomer(1)?.birthday); // Date for now

  customer?.[0] // access its first element if customer is an array, or return undefined

  let log: any = null;
  log?.('a') // will execute only log is a actual function, or return undefined
  ```
<br>

### Functions

**Best Practice**: annotate every parameters and variables in functions as **literal function definition**

- parameter types are annotated in the parentheses and return type is annotated outside of the parentheses

  - if type of return value is `void`, meaning it does not return any value;

- default value could be given to parameters just like javascript, no need to annotate type if default value is given

```
function rectangleArea(h: number, w: number): number {
  return h * m;
}

function getArea(shape: string, h = 100, w?: number, calculateFn: (a: number, b: number) => number): number {
  if (shape === 'Square') return calculateFn(h, h);
  return calculateFn(h, w);
}
```
<br>

**Function type alias**: assign function type to a type alias, commonly used with higher order functions
  ```
  type GreetFunction = (a: string) => void;
  function greeter(fn: GreetFunction) {
    // ...
  }

  // or use call signature, see below
  function greeter(fn: { (a: string): void} ) {
    // ...
  }
  ```
  <br>

**Function Signature**: a more general term that encompasses the concept of specifying the interface of a function, including the function's name, parameter names, and types, as well as the return type.
  - It defines how the function should be called and what it returns, but it doesn't create a new type or alias for a type. It's primarily about describing the behavior of a function. 
  - The parameter names are arbitrary

```
// below is a function signature
let greet: (a: string, b:string) => void;

greet = (name: string, greeting: string) => {
  console.log(`${name} says ${greeting}`)
}

// below is function overload signatures, which use functio signature with implementation signature
fucntion parseCoordinate(obj: Coordinate): Coordinate;
fucntion parseCoordinate(x: number, y: number): Coordinate;
fucntion parseCoordinate(arg1: unknonwn, arg2?: unknown): Coordinate {
  let coord: Coordinate = { x: 0, y: 0 }
  if (typeof arg1 === 'object') {
    coord = { ...(arg1 as Coordinate) }
  } else {
    coord = { x: arg1 as number, y: arg2 as number }
  }
  return coord;
}
```
<br>

**Call Signatures**: add properties to function type in addition to function type expressions.
```
type DescribableFunction = {
  description: string;
  (argOne: number, argTwo: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6, 9));
}
 
function isLarger(argOne: number, argTwo: number) {
  return argOne > argTwo;
}
myFunc.description = "default description";
 
doSomething(isLarger);
```
  - here function type expression uses `:` instead of `=>`:  `(someArg: number): boolean;`
  <br>

**Construct Signatures**: for functions that work with `new` operator:
```
type SomeConstructor = {
  new (s: string): SomeObject;
};
function fn(ctor: SomeConstructor) {
  return new ctor("hello");
}
```
  - add `new` in call signature to make is construct signatures
  - call signature and construct signature can be used together for one function that can be called with or without `new`, like `Date` object:
    ```
    interface CallOrConstruct {
      (n?: number): string;
      new (s: string): Date;
    }
    ```
    <br>

**Generic function**: When invoking, depending on what `<Type> or <T>` is (_name is arbitrary, could be anything_), and the function will take that `<Type> or <T>` as input or returns

  ```
  interface GenericIdentityFn<Type> {
    (arg: Type): Type;
  }

  function identity<Type>(arg: Type): Type {
    return arg;
  }

  // myIdnetity only takes number as parameter
  let myIdentity: GenericIdentityFn<number> = identity; 

  function map<Input, Output>(array: Input[], callback: (Input) => Output): Output[] {
    const newArray: Output[] = [];
    for (let item of array) {
      newArray.push(callback(item));
    }
    return newArray
  }
  ```
  - **Rules**: 
    - Always use as few type parameters as possible

    - When possible, use the type parameter itself rather than constraining it

    - If a type parameter only appears in one location, strongly reconsider if you actually need it
    <br>

  - **Type inference**: if it can be **inferred** when using function type, then no need to specify it.
    ```
    function map<Input, Output>(arr: Input[], func: (arg: Input) => Output): Output[] {
      return arr.map(func);
    }
    
    const parsed = map(["1", "2", "3"], (n) => parseInt(n)); // Parameter 'n' is of type 'string'

    // below will give error because 'n' is of type 'string | number', and parseInt() doesn't work with number type argument
    const parsed = map(["1", 2, "3"], (n) => parseInt(n));

    /*----- type inference is not always accurate ----- */

    function combine<Type>(arr1: Type[], arr2: Type[]): Type[] {
      return arr1.concat(arr2);
    }

    // below works
    const arr = combine<string | number>([1, 2, 3], ["hello"]); 

    // below will give error because TS infers Type from the first array as 'string', which doesn't apply to 'number' in the second array
    const arr = combine([1, 2, 3], ["hello"]); 
    ```
    <br>

  - **Constraints**: For **generic type parameters**, using `extends` clause to constrained generic type to only those that patially includes the extended type.
    ```
    function minimumLength<Type extends { length: number }>(
      obj: Type,
      minimum: number
    ): Type {
      if (obj.length >= minimum) {
        return obj;
      } else {
        return { length: minimum };
        /** 
         * Type '{ length: number; }' is not assignable to type 'Type'.
         * '{ length: number; }' is assignable to the constraint of type 'Type', 
         * but 'Type' could be instantiated with a different subtype of constraint '{ length: number; }'.
         */
      }
    }
    ```
    <br>

**Optional parameters**: add `?` after parameter name. 
  - making a parameter optional will change its type to be a union of its original type and `undefined`
    ```
    function f(x?: number) {
      // x here has type of (number | undefined)
    }
    f(); // OK
    f(10); // OK
    f(undefined); //OK
    ```
  - **When in Callbacks**: never write an optional parameter unless you intend to call the function without passing that argument
    ```
    function myForEach(
      arr: any[],
      callback: (arg: any, index?: number) => void
    ): void {
      arr.forEach((ele, i) => {
        callback(ele, i)
      })
    }

    // this work
    myForEach([1, 2, 3], (a) => {
      console.log(a);
    });

    // this gives error because TS thinks i could be undefined, to fix this, either remove the optional modifier or check if 'index' is defined (narrowing)
    myForEach([1, 2, 3], (a, i) => {
      console.log(i.toFixed());
    });
    ```
    <br>

**Function overload**
  - specify a function with different ways of implementation, using a number of function signatures with the body of the function (implementation signature)
  ```
  function makeDate(timestamp: number): Date;
  function makeDate(m: number, d: number, y: number): Date;
  function makeDate(mOrTimestamp: number, d?: number, y?: number): Date {
    if (d !== undefined && y !== undefined) {
      return new Date(y, mOrTimestamp, d);
    } else {
      return new Date(mOrTimestamp);
    }
  }
  ```
  - **Rules**:

    - The implementation signature must also be **compatible with all** the overload signatures. 

    - Always prefer parameters with union types instead of overloads when possible

  


<br>

### Class

- when define classes, specifiy the type of each property **above the constructor method**
- access modifiers: optional
  - `public`: can be accessed anywhere
  - `private`: can only be accessed from within the class itself

```
class User {

}
```

<br>

### Type Manipulation

#### Generics
  
  - **Generic Types**: 

  <br>

  - `extends`: In TS, `extends` can have several use cases in different context:

    - **Generic Type Constraints**: in *generic type parameters* to enforce type constraints.
      ```
      function exampleFunction<Type extends SomeType>(param: Type) {
        // Code that only works with 'Type' that have SomeType
      }
      ```
    - **Interface Inheritance**: used in interfaces to extend or inherit from other interfaces.

    - **Class Inheritance**: Similar to interfaces, the `extends` keyword is used in classes to inherit from another class.

    - **Conditional Types**: used to deduce types based on conditions, create more complex type definitions
      ```
      type TypeName<Type> = Type extends string ? 'string' : 'non-string';
      ```

#### The `keyof` type operator
  - takes an object type and produces a string or numberic **literal union type** of its keys.
  ```
  type Point = { x: number; y: number };
  type P = keyof Point; // same as type P = 'x' | 'y'
  ```
  - if the type has a string or number index signature, `keyof` will return those types instead. Note JS object keys are always coerced to a string, so key could be either string or number.
  ```
  type Arrayish = { [n: number]: unknown };
  type A = keyof Arrayish; // same as type A = number

  type Mapish = { [k: string]: boolean };
  type M = keyof Mapish; // same as type M = string | number
  ```
  <br>

#### The `typeof` type operator
  - In JS, `typeof` exists in **run-time**, can be used as an expression context, 
  - In TS, `typeof` only exists in **compile-time**, refers to the type of a variable or property
  - Be careful that `typeof` only works on **value** or **identifiers(variables)** or **variable properties**
  ```
  // this is JS typeof, same as let n: string
  let s = "hello";
  let n: typeof s; 

  // these are TS typeof, same as type Greet = "hello";
  const greet = "hello";
  type Greet = typeof greet; 

  const obj = {
    name: 'xiao',
    age: 34,
  }
  type NameType = typeof obj.name; // same as type NameType = "string";
  type Person = keyof typeof obj; // same as type Person = "name" | "age";

  const func = () => {
    const val = 'string';
    return val
  }
  type Return = ReturnType<typeof func> // same as type Return = "string"
  ```

  <br>

#### The Indexed Type operator

  - Indexed access type can look up a specific property on another type

  - Notice that indexing property **itself is a type**

  - Indexing type can work with unions, `keyof`, or other types entirely

  ```
  type Person = { 
    age: number; 
    name: string; 
    alive: boolean 
  };
  type Age = Person["age"]; // same as type Age = number
  
  type Key = "name"; 
  type Name = Person[Key] // same as type Name = Person["name"], Key is also a type

  const key = "name";
  type Name = Person[key] // Error: 'key' refers to a value, but is being used as a type here.

  type I1 = Person["age" | "name"]; // same as type I1 = string | number
  
  type I2 = Person[keyof Person]; // same as type I2 = string | number | boolean
  
  type AliveOrName = "alive" | "name";
  type I3 = Person[AliveOrName]; // same as type I3 = string | boolean

  // Will give error if property doesn't exist
  type I4 = I3["age"]; // Error: Property 'age' does not exist on type 'I3'.
  ```
  <br>

#### The Conditional Types

  ```
  SomeType extends OtherType ? TrueType : FalseType;
  ```
  - if `SomeType` 
  <br>
#### The Mapped Types
#### Template Literal Types

<br>

### Untility TYpes
- `Awaited<Type>`
- `Patial<Type>`
- `Required<Type>`
- `Readonly<Type>`
- `Record<Keys, Type>`
- `Pick<Type, Keys>`
- `Omit<Type, Keys>`
- `Exclude<UnionType, ExcludedMembers>`
- `Extract<Type, Union>`
- `NonNullable<Type>`
- `Parameters<Type>`
- `ConstructorParameters<Type>`
- `ReturnType<Type>`
- `InstanceType<Type>`
- `ThisParameterType<Type>`
- `OmitThisParameter<Type>`
- `ThisType<Type>`
- Intrinsic String Manipulation Types:
  - `Uppercase<StringType>`
  - `Lowercase<StringType>`
  - `Capitalize<StringType>`
  - `Uncapitalize<StringType>`

## Concepts

#### Type assertion
- To **ensure TS** that a specific variable has a certain type. 
  - Non-null assertion operator`!`:
    ```
    // without !
    function UpperCase(x?: string | null) {
      // this has to be done, otherwise gives error
      if (x === null || x === undefined) {
        return '';
      } else {
        return x.toUpperCase();
      }
    } 
    // use !, ensure x will never be undefined or null
    function UpperCase(x?: string | null) {
      // No error
      console.log(x!.toFixed());
    }
    ```
    <br>

  - as Type `as TypeName` or angle-bracket syntax`<TypeName>`:

    ```
    const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

    // below is equivalent to above, except in .tsx files
    const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
    ```
#### types.d.ts
  - in `tsconfig.json`, set `"include": [..., **/*.ts, ...]`
  - then `.d.ts` files do not need export anything, TS will know about them.
  <br>

#### import type
  - a TS syntax added after 3.8 for type-only imports and exports
  ```
  import type { SomeThing } from "./some-module.js";

  export type { SomeThing }
  ```




## Topics to check later
1. 
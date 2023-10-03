## TypeScript: Javascript with type checking
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
- Configure typescript compiler:
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

#### <span>TypeScript basic types:</span> 
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


#### <span>TypeScript new primitive types:</span> `any`, `unknown`, `never`

- `any`: if not assigned any type, it will be `any` type, meaning it could be **anything**, so TS will give no error or warning on any operation of that variable, it **disables type checking** for that variable. This is useful when you don’t want to write out a long type just to convince TypeScript that a particular line of code is okay.

- `unknown`: unlike `any`, TS restricts any operations on `unknown` variable, useful when **multiple types are accepted** for one variable, and use **conditional check** to narrow it down for one particular type.
  ```
  let val: unknown = 1;
  // all below would have type checking error
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

#### <span>Enum</span>: 
  
`enum`: associate a set of **named constants** with **values**, and make it a type for a variable that could be one of the values.
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

#### <span>Arrays</span>:

- TS can annotate the array element type (two ways)
  - `let numbers: number[] = [1, 2, 3]`
  - `let numbers: Array<number> = [1, 2, 3]`
- add `readonly` to prevent arrays from being changed:
  - `let numbers: readonly number[] = [1, 2, 3]`
- if assigned value is an array of same types, then the type annotation of the variable can be omitted: `let numbers = [1, 2, 3]`
- if declare an empty array, it is better to apply a type annotation: `let numbers: number[] = []`
- and for typed array methods (like `forEach`), in its arrow function, typescript can show all the properties and methods of that type objects.

<br>

#### <span>Tuple</span>: 

- a tuple is a typed array with pre-defined length and types:
  `let user: [number, string] = [33, 'age']`

  <br>

#### <span>Functions</span>:

Best Practice: annotate every parameters and variables in functions

- parameter types are annotated in the parentheses and return type is annotated outside of the parentheses

  - if type of return value is `void`, meaning it does not return any value;

- default value could be given to parameters just like javascript, no need to annotate type if default value is given
- Optional parameters can be used if add `?` after

```
function calculatedTax(income: number, taxYear = 2023, name?: string): number {
  if (taxYear < 2022) return income * 1.2;
  return income * 1.3;
}
```

#### <span>Generics Types</span>:

- When invoking, depending on what `Type` is (_name is arbitrary, could be anything_), and the function will take that `Type` as input or returns

```
function identity<Type>(arg: Type): Type {
  return arg;
}

function map<Input, Output>(array: Input[], callback: (Input) => Output): Output[] {
  const newArray: Output[] = [];
  for (let item of array) {
    newArray.push(callback(item));
  }
  return newArray
}

map<>
```

<br>

#### <span>Object</span>:

- when annotate type of an object, add a `?` after property indicating this property may not be shown in the object, or annotate normally and temporarily assign a empty string to it.
- `readonly` can also apply to properties by adding in the front to make it unchangable

```
let emplyee: {
  readonly id: number,
  name: string,
  fax?: string,
  retire: (date: Date) => void
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

#### <span>Class</span>:

- when define classes, specifiy the type of each property **above the constructor method**
- access modifiers: optional
  - `public`: can be accessed anywhere
  - `private`: can only be accessed from within the class itself

```
class User {

}
```

<br>

#### <span>Type Alias</span>:
 can be used for primitives and complex types

```
type Employee = {
  readonly id: number,
  name: string,
  fax?: string,
  retire: (date: Date) => void
}
```

<br>

#### <span>Interfaces</span>:

- just like type alias, but have two distinctions:
  - Interfaces can only apply to object types
  - Interfaces can extend other interface's definition, while type alias can not.

```
interface Rectangle {
  height: number,
  width: number
}

interface ColoredRectangle extends Rectangle {
  color: string
}
```

<br>

#### <span>Union Type</span>: 
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

<br>

#### <span>Intersection Type</span>: 
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

#### <span>Literal Type</span>: 
exact, specific value

```
type Quantity = 50 | 100;
let quantity: Quantity = 100;

// practical use
type Metric = 'cm' | 'inch';
```

<br>


#### <span>Optional Chaining</span>:

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
## Concepts

#### <span>Type assertion:</span>
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
  - as Type `as TypeName` or angle-bracket syntax`<TypeName>`:
    ```
    const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

    // below is equivalent to above, except in .tsx files
    const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas");
    ```
#### <span>types.d.ts</span>
  - in `tsconfig.json`, set `"include": [..., **/*.ts, ...]`
  - then `.d.ts` files do not need export anything, TS will know about them.
  <br>

#### <span>import type</span>
  - a TS syntax added after 3.8 for type-only imports and exports
  ```
  import type { SomeThing } from "./some-module.js";

  export type { SomeThing }
  ```




## Topics to check later
1. 
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

TypeScript new types:

- any: if not assigned any type, it will be any type
- unknown:
- never
- enum
- tuple

in typescript, large number can be seperated using `_`: `let num: number = 123_456_789;`

for `number`, `string` and `boolean` types, no type notation is needed cause compiler will figure it out based on the value (implicit type assignment)

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

if only `let x` without assignment, x will have the type of `any`, which just like using `let` to declare a variable, you can reassign it with different types, but this is highly unrecommanded.

- when using parameters in a function, if not explicitly annotate the type, and typescirpt will generate a error.
  - Two ways to solve this: give parameters `any` type or turn `noImplicityAny` to `false` in tsconfig.json

**Arrays**:

- typescript can annotate the array element type (two ways)
  - `let numbers: number[] = [1, 2, 3]`
  - `let numbers: Array<number> = [1, 2, 3]`
- add `readonly` to prevent arrays from being changed:
  - `let numbers: readonly number[] = [1, 2, 3]`
- if assigned value is an array of same types, then the type annotation of the variable can be omitted: `let numbers = [1, 2, 3]`
- if declare an empty array, it is better to apply a type annotation: `let numbers: number[] = []`
- and for typed array methods (like `forEach`), in its arrow function, typescript can show all the properties and methods of that type objects.

**Tuples**:

- a tuple is a typed array with pre-defined length and types:
  `let user: [number, string] = [33, 'age']`

**enum**;

- a enum is a special "class" that represnets a group of constants
- by default, enums will

  - if the first value is not initialized, initialize it to `0`
  - if any value is not initialized and the previous value is a number, add `1` to each additional value

- String Enums must be initialized
- Mix and match string and numeric enum values is not recommonded.

  ```
  cosnt small = 0;
  const medium = 1;
  const large = 2;

  // if using enum
  enum Size { Small, Medium = 3, Large};
  let myMedium: Size = Size.Medium; // myMedium is 1;
  let myLarge: Size = Size.Large; // myLarge is 4;
  ```

- if use `const` before `enum`, the compiler will generate more optimized code.
  `const enum Size { Small, Medium, Large}`
  <br>

**Functions**:
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

**Generics Types**:

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

**Object**:

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

**Class**:

- when define classes, specifiy the type of each property **above the constructor method**
- access modifiers: optional
  - `public`: can be accessed anywhere
  - `private`: can only be accessed from within the class itself

```
clas User {

}
```

<br>

**Type Alias**: can be used for primitives and complex types

```
type Employee = {
  readonly id: number,
  name: string,
  fax?: string,
  retire: (date: Date) => void
}
```

<br>

**Interfaces**:

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

**Union Type**: one or another
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

**intersection Type**: one and another
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

**Literal Type**: exact, specific value

```
type Quantity = 50 | 100;
let quantity: Quantity = 100;

// practical use
type Metric = 'cm' | 'inch';
```

<br>

**Nullable Type**: `null` and `undefined` are both types of its own value

<br>

**Optional Chaining**:

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

# TypeScript

- [TypeScript](#typescript)
  - [Types](#types)
    - [TypeScript basic types](#typescript-basic-types)
    - [TypeScript new primitive types `any`, `unknown`, `never`](#typescript-new-primitive-types-any-unknown-never)
    - [Enum](#enum)
    - [Arrays](#arrays)
    - [Tuple](#tuple)
    - [Functions](#functions)
    - [Object](#object)
    - [Class](#class)
    - [Type Alias](#type-alias)
    - [Interfaces](#interfaces)
    - [Union Type](#union-type)
    - [Intersection Type](#intersection-type)
    - [Literal Type](#literal-type)
    - [Optional Chaining](#optional-chaining)
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


### TypeScript new primitive types `any`, `unknown`, `never`

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

### Enum 
  
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

### Functions

**Best Practice**: annotate every parameters and variables in functions

- parameter types are annotated in the parentheses and return type is annotated outside of the parentheses

  - if type of return value is `void`, meaning it does not return any value;

- default value could be given to parameters just like javascript, no need to annotate type if default value is given
- Optional parameters can be used if add `?` after

```
function rectangleArea(h: number, w: number): number {
  return h * m;
}

function getArea(shape: string, h = 100, w?: number, calculateFn: (a: number, b: number) => number): number {
  if (shape === 'Square') return calculateFn(h, h);
  return calculateFn(h, w);
}
```
**Call Signatures**: add properties to function type in addition to functionp type expressions.
```
type DescribableFunction = {
  description: string;
  (someArg: number): boolean;
};
function doSomething(fn: DescribableFunction) {
  console.log(fn.description + " returned " + fn(6));
}
 
function myFunc(someArg: number) {
  return someArg > 3;
}
myFunc.description = "default description";
 
doSomething(myFunc);
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



<br>

### Object

- when annotate type of an object, add a `?` after property indicating this property may not be shown in the object, or annotate normally and temporarily assign a empty string to it.
<br>
- properties without `?` must match the Object literal
<br>
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

- **Index Signatures**: use this when the names of a type's properties are not known, but the shape of the values are known ahead of time.
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

### Type Alias
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

### Interfaces

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
  - **Discriminated Union (or tagged union)**: a special type of union, there is an **identical** property in each variant as the **discriminant** (shared discriminative property), may has an optional leading `|` , useful in type checking and exhaustiveness checking. Also works great with `switch`

    ```
    {
      type Shape = 
        | { kind: "circle", radius: number }
        | { kind: "square", sideLength: number }
        | { kind: "triangle", base: number, height: number }

      /* -------------- or below --------------- */

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


### Optional Chaining

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

### Type Manipulation

#### Generics
  - **Generic function**: When invoking, depending on what `<Type> or <T>` is (_name is arbitrary, could be anything_), and the function will take that `<Type> or <T>` as input or returns

    ```
    function identity<Type>(arg: Type): Type {
      return arg;
    }

    let myIdentity: <T>(arg: T) => T = identity; //  (<T>(arg: T) => T) is the function type

    function map<Input, Output>(array: Input[], callback: (Input) => Output): Output[] {
      const newArray: Output[] = [];
      for (let item of array) {
        newArray.push(callback(item));
      }
      return newArray
    }

    map<>
    ```
  - **Generic Interface**: 

#### The `keyof` type operator
  - takes an object type and produces a string or numberic **literal union** of its keys.
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
  - In JS, `typeof` can be used as an expression context, in TS, `typeof` refers to the type of a variable or property
  ```
  let s = "hello";
  let n: typeof s; // same as let n: string

  const greet = "hello";
  type Greet = typeof greet; // same as type Greet = "hello";

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
  - Be careful that there are two `typeof`: 
    - JS `typeof`: only works on **value** or identifiers or their property;
    - TS `typeof`: only works with **type** identifiers.
  <br>

#### The Indexed Type operator

#### The Conditional Types
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
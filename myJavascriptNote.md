# Javascript notes

## Table {#table}

- [Js Primitive Types](#js-primitive)
- [Boolean](#boolean)
- [Null](#null)
- [Undefined](#undefined)
- [Numbers](#number)
- [String](#string)
- [Symbol](#symbol)
- [Array](#array)
- [Object](#object)
- [Function](#function)
- [Hoist](#hoist)
- [Promise](#promise)
- [Async/await](#async_await)
- [Regular Expression](#RegExp)
- [Interesting topics](#interesting)

---

## Js Primitive Types {#js-primitive}

- Number, String, Boolean, null, undefined, BigInt, Symbol (#js primitive)

- `var.valueOf()`: return the primitive value
- `typeof var`: return the variable type in `string` format

Primitives are immutable, can be **replaced** but **not directly altered**, e.g.,:

    var str = "cool";
    str[2] = "l"; /*This doesn't work*/

##### **[Back to table](#table)**

---

### Boolean {#boolean}

boolean
: `true` or `false`, no quotes, any value in JS can be used for boolean

|                     Falsy                     |                     Truthy                     |
| :-------------------------------------------: | :--------------------------------------------: |
| 0, -0, null, NaN, undefined, ""(empty string) | anything else (like empty object, empty array) |

<br>

- Operators that return Boolean results:

  - **Equality, Inequality** & **Strict equality, strict inequality**:`==` `!=` & `===` `!==`
  - **Greater, greater or equal than** & **less, less or equal than**: `>` `>=` & `<` `<=`
  - **in** operator: `prop in object`

    - check if `object` (or its prototype chain) contains the property with specified name `prop`.

<br>

##### **[Back to table](#table)**

---

### Null {#null}

null
: Intentional absence of any value, **must be assigned**

<br>
##### **[Back to table](#table)**
---

### Undefined {#undefined}

undefined
: Variables that do not have an assigned value, from values that **hasn't been defined** or **doesn't exist**

<br>
##### **[Back to table](#table)**
---

### Numbers {#number}

- No positive/negative/integers/decimal classes, uses **double-precision 64-bit binary format IEEE 754**
- `NaN` is in also `number` type;
- Two zeros: `0` & `-0`
- Two infinities: `Infinity` & `-Infinity`

#### Math Object (commomly used)

##### Properties:

- `Math.PI` : PI
- `Math.E` : Euler's number (e)
  <br>

##### Static Methods

- `Math.floor(3.65) // 3` : nearest smaller integer
- `Math.ceil(-3.65) // -3 ` : neareast larger integer;
- `Math.round(3.65) // 4` : nearest integer (eg., +/-0.5 => 1/0);
- `Math.trunc(3.65) // 3` : integer part of given number;
- `Math.exp(2)` : e^2^
- `Math.log(2)` : ln2
- `Math.log10(2)` : log~10~2
- `Math.log2(3)` : log~2~3
- `Math.pow(3,7)` : 3^7^
- `(Math.ln(y)/Math.ln(x))` : log~x~y
- `Math.abs(-3) // 3` : |-3|
- `Math.sqrt(x)` : $\sqrt{x}$ (x>=0)
- `Math.sin/cos/tan/asin/acos/atan(x)`: trigonometric (x in radius)
- `Math.random()` : random number bewteen [0,1),
  - random number among [ 1, N ]: `Math.floor(Math.random()*N+1)`
- `Math.max/min(1,2,3) // 3, 1` : max/min value of inputs
  <br>

#### Number methods (commomly used)

##### Static Methods

- **Number()**: `Number(value) // converts value to number type`
  <br>
- **Number.isInteger()**: test if value is integer
  1. if not `number` type, return `false`
  2. if `number` type => test for `integer`
     <br>
- **Number.isFinite() / Number.isNaN() vs isFinite() / isNaN()**:

- `Number.isFinite() / Number.isNaN()`:

  1. if not `number` type, return `false`
  2. if `number` type => test for `finite`/`NaN`

  - `Number.isNaN('3') // false`

- `isFinite() / isNaN()` : coerced to `number` type, then test for `finite`/`NaN`

  - `isNaN('3') //true`
    <br>

- **Number.parseInt() / parseInt()**: From left to right, return starting integer part
  - `Number.parseInt() === parseInt() // true`
  - `parseInt('123a456.7') // 123`
    <br>
- **Number.parseFloat() / parseFloat()**: From left to right, return starting float part

  - `Number.parseFloat() === parseFloat() // true`
  - `parseFloat('1.23a45') // 1.23`
    <br>

##### Instance Methods

- **.toExponential()**: `123.456.toExponential() = '1.23456e+2' `: return a ==string== representing the scientific notation formatted number
  <br>
- **.toFixed()**: `123.456.toFixed(x) = '123.4' // x = 1 `: return a ==string== representing the fixed-point notation number, [x] = 0
  <br>
- **.toPrecision()**: `123.456.toPrecision(x) = '1.2e+2' // x = 2 | '123.5' // x = 4` : return a ==string== representing fixed-point or exponential notation rounded to precision significant digits
  <br>
- **.toString()**: `123.456.toString(b) = '443.212' // b = 5` : return a ==string== representing the object in the specified radix (base), default [b] = 10
  <br>

##### **[Back to table](#table)**

---

### String {#string}

- quoted, single or double, consistent
- concatenate: `"hello" + ", " + "world!"` = `"hello, world!"`
- indexed: `var str = "hello";` `str[0]` is `"h"`, `str[1]` is `"e"`
- has **built-in iterator** which can be used to iterate over the string
- unchangeable (immutable), but reassignable;
- quotes in strings: `'He said "Hello!"'` or `"She says 'Goodbye'"`
- String template literals: <code> \`${expression}\` </code>
- use `\` to escape `'`, `"` and `\` in string:

  | Code | Result | Description  |
  | :--: | :----: | :----------: |
  | `\\` |  `\`   |  Backslash   |
  | `\'` |  `'`   | Single quote |
  | `\"` |  `"`   | Double quote |

#### **String methods**

- **str.length** : return the length of str`

  <br>

- **.charAt()**: `'hello'.charAt(x) = "l"; // x = 2` :

  <br>

- **.concat()**: `"Hello".concat(", ", "World!")`

  - return: a modified ==copy== of `str` with concatenated `chars`/`substring`(`"Hello, World!`)

  <br>

- **.endsWith()**: `str.endsWith(searchstring[, length])`

  - return: `true` or `false`
  - default `[length]`= `str.length`
  - `"markdown file".endsWith('down', 8) // true`

- **.startsWith()**: `str.startsWith(searchstring[, position])`

  - return: `true` or `false`
  - default starting `[position]` = `0` (included)
    <br>

- **.includes()**: `str.includes(searchstring[, position])`

  - return: `true` or `false`
  - default starting [position] = `0` (included)
  - `"This is a markdown file".includes('This', 1) // false`

    <br>

- **.indexOf()**: `str.indexOf(searchstring[, position])`

  - return: first index of the first occurrence or -1 (not found)
  - default starting `[position]` = `0` (included)

  <br>

- **.lastIndexOf()**: `str.lastIndexOf(searchsting[, position])`

  - return: first index of the last occurrence or -1 (not found)
  - default ending [position] = `str.length - 1` (included)

  <br>

- **.padEnd()**: `str.padEnd(targetlength[, padstring])`

  - return: a modified ==copy== of `str` with `targetlength` and `padstring`
  - `targetlength`: length of the return `str`
  - `"hello".padEnd(3) // "hello"` : `targetlength` < `str.length`
  - <code>"hello".padEnd(10) // "hello&UnderBracket;&UnderBracket;&UnderBracket;&UnderBracket;&UnderBracket;" </code> : default `[padstring]`=<code>"&UnderBracket;"</code>(space)
  - `"hello".padEnd(10, '123') // "hello12312"` : `padstring.length` < `targetlength` - `str.length`
  - `"hello".padEnd(10, '12345678') // "hello12345"` : `padstring.length` > `targetlength` - `str.length`

- **.padStart()**: `str.padStart(targetlength[, padstring])`

  - return: a modified ==copy== of `str` with `targetlength` and `padstring`
  - `targetlength`: length of the return `str`
  - `"hello".padStart(3) // "hello"` : `targetlength` < `str.length`
  - <code>"hello".padStart(10) // "&UnderBracket;&UnderBracket;&UnderBracket;&UnderBracket;&UnderBracket;hello" </code> : default `[padstring]` = <code>"&UnderBracket;"</code>(space)
  - `"hello".padStart(10, '123') // "12312hello"` : `padstring.length` < `targetlength` - `str.length`
  - `"hello".padStart(10, '12345678') // "12345hello"` : `padstring.length` > `targetlength` - `str.length`

  <br>

- **.trim()**: `str.trim()`

  - return: a modified ==copy== of `str` with whitespaces at beginning and end are removed

- **.trimStart()**: `str.trimStart()`

  - return: a modified ==copy== of `str` with whitespaces from beginning are removed

- **.trimEnd()**:`str.trimEnd()`

  - return: a modified ==copy== of `str` with whitespaces from end are removed

  <br>

- **.repeat()**: `"Aaa".repeat(3)`

  - return: a modified ==copy== of `str` with repeating (`"AaaAaaAaa"`)

  <br>

- **.replace()**: `"Aaa".replace('a', '-')`

  - return: a modified ==copy== of `str` with ==first== occurance replaced (`"A-a"`)

- **.replaceAll()**: `"Aaa".replaceAll('a', '-')`

  - return: a modified ==copy== of `str` with ==all== occurance replaced (`"A--"`)

  <br>

- **.search()**: `"hello".search('e') // 1`

  - return: index of first occurence or -1 (not found)

  <br>

- **.slice()**: `str.slice(start[, end])`

  - return: a modified ==copy== of `str[start]` (included) to `str[end]` (excluded)
  - `start` and `[end]` could be negative integer
  - `"hello".slice(1) // "ello", remove first char`
  - `"hello".slice(-1,1) // ""` : `start` > `end`

- **.substring()**: `str.substring(start[, end])`

  - return: a ==copy== from `str[start]` (included) to `str[end]` (excluded)
  - almost identical to `str.slice()`, but there are two differences:

    - `"hello".substring(-1,6) // "hello", same as "hello".substring(0,5)` : negative and larger than `str.length` indexes are treated as 0 and `str.length`, repectively
    - `"hello".substring(4,1) // "ell", same as "hello".substring(1,4)` : ==swap== `start` and `end` when `start` > `end`

    <br>

- **.split()**: `str.split([seperator][,limit])`

  - return: an `array` whose elements are substrings of `str` seperated by `[seperator]`, and `array.length` <= `[limit]`
  - `[limit]`: Maximum number of elements in the returned subarray. If `limit` is `0`, `[]` is returned
  - `"a b c d e f".split(' ',4) // ['a','b','c','d']` : 4 elements
  - `"a b c d e f".split(',') // ['a b c d e f']` : 1 element cause `['a b c d e f']` has no `','`
    <br>

- **.toLowerCase()**: `"Hello".toLowerCase() // "hello"`
- **.toUpperCase()**: `"Hello".toUpperCase() // "HELLO"`

  <br>

- **.toString()**: `str.toString() // works on String Object, same as str.valueOf()`
  <br>

- **.match()**: `str.match(regex) // retrieves the result of matching a string against a regular expression.`
  - return: An Array whose contents depend on the presence or absence of the global (`g`) flag, or `null` if no matches are found.
    - with `g` : all matches
    - without `g`: the first match

<br>

##### **[Back to table](#table)**

---

### Symbol {#symbol}

- can only be created with `Symbol([lable])`
  - `label` is optional, only a note for this symbol
- each symbol is unique
- a symbol value is only used as an identifier for object propeties
- when add a symbol as a property, there are two ways
  - ```
      const propSym = Symbol('prop')
      obj[propSym] = propValue
    ```
    or
  - ```
    const propSym = Symbol('prop')
    obj = {
      [propSym] : propValue
    }
    ```
- Symbols are not enumerable, so it will not show up in `for...in` loop or `Object.getOwnPropertyNames()`
- Symbols can be accessed by `Object.getOwnPropertySymbols()`

<br>
##### **[Back to table](#table)**
---

## Array {#array}

- resizable
- integers as indexes
- has **built-in iterator** which can be used to iterate over the array
- pass as reference
  <br>

#### **Array static methods**

- array-like objects:

  - objects with a length property and indexed elements
  - iterable objects (like `Map` and `Set`)
    <br>

- **Array()**:

  - return: a new `Array` instance
  - can work as a constructor or a function

    1. constructor: work with `new` operator
    2. function: creates and initialises a new `Array` object, same as `new Array()`

    ```
    // From elements
    new Array(element0, element1, ... , elementN)
    Array(element0, element1, ... , elementN)

    // From array length (interger argument), empty array with a length
    new Array(arrayLength)
    Array(arrayLength)
    ```

    <br>

- **Array.of()**: creates a new Array instance from a variable number of arguments, regardless of number or type of the arguments.

  - return a new `Array` instance.
  - arguments are the elements, regardless of data type, different from `Array()`
    ```
    Array.of(7) // [7]
    Array(7) // An array of 7 empty slots
    ```
    <br>

- **Array.from()**: `Array.from(arrayLike[, callbackFn(element[, index]) { /*...*/ } [, thisArg]])`

  - return a new `Array` instance
  - for array-like object specifically.

    - object with a `length` property
    - indexed elements

    ```
    Array.from({length: 3}) // [undefined, undefined, undefined]
    Array.from({length: 3}, (v,i) => i) // [0, 1, 2]

    Array.from('hello') // ['h', 'e', 'l', 'l', 'o']
    ```

- **Array.isArray()**: determine whether the passed value is an `Array`

  - return: true if the value is an Array; otherwise, false.
    <br>

#### **Array instance methods**

`const arr = [1,2,3,'a','b','c']`
<br>

- **.at()**: `arr.at(-1) // 'c'`

  - return: item at the index
  - negative number count back from last item.
    <br>

- **.indexOf()**: `arr.indexOf(searchElement[, start])`

  - return: the ==index== of the first element in the array or -1 (not found)

- **.lastIndexOf()**: `arr.lastIndexOf(searchElement[, start])`

  - return: the ==index== of the last element in the array or -1 (not found)
    <br>

- **.includes()**: `arr.includes(searchElement[, start])`(case-sensitive)

  - return: `true` or `false`
  - default `[start]` = `0`
  - `arr.includes('a', 4) // false`

  <br>

- **.join()**: `arr.join([seperator])`

  - return: a ==string== with all array elements joined.
  - default `[seperator]` = `","`

- **.toString()**: `arr.toString()`

  - return: a ==string== representing the elements of the array.
  - is the same as `arr.join()`
    <br>

- **.concat()**: `arr.concat(arr[, value1, ... , valueN])`

  - return: a modified ==copy== of `arr` with concatenated elements
  - `arr.concat([4,5,6],'d','e','f') // [1,2,3,'a','b','c',4,5,6,'d','e','f']`
    <br>

- **.slice()**: `arr.slice([start][, end])`

  - return: a modified ==copy== of `arr` with array elements from `arr[start]` (included) to `arr[end]` (excluded)
  - default `[start]` = `0`, could be negative integer
  - default `[end]` = `arr.length`, could be negative integer
    <br>

- **.flat()**: `arr.flat([depth])`

  - return: a modified ==copy== of `arr` with sub-array elements concatenated into it
  - default [depth] = `1` (from outside to inside)
  - `[1,[2,[3,4]]].flat() // [1,2,[3,4]]`
    <br>

- **.copyWithin()**: `arr.copyWithin(targetIndex[, start][, end])`(==mutator method==)

  - return: the modified array whose elements are replaced starting from `targetIndex` with elements from `[start]`(included) to `[end]` (excluded), no change to `arr.length`
  - default `[start]` = `0`
  - default `[end]`=`arr.length`
  - `targetIndex`, `[start]`, `[end]` could be negative integer
  - no change when `[start]` >= `[end]`
  - no change when `targetIndex` > `arr.length`
  - `arr.copyWithin(1,3,5) // [1,'a','b','a','b','c']`: start from `arr[1]`,replace `arr[1]`, `arr[2]` with `arr[3]`, `arr[4]`, the rest remain the same
    <br>

- **.fill()**: `arr.fill(value[, start][, end])`(==mutator method==)

  - return: the modified array whose elements are replaced with `value` from `[start]`(included) to `[end]` (excluded), no change to `arr.length`
  - default `[start]` = `0`, could be negative integer
  - default `[end]`=`arr.length`, could be negative integer
    <br>

- **.reverse()**: `arr.reverse()` (==mutator method==)

  - return: the modified array whose elements order are reversed
    <br>

- **.pop()**: `arr.pop()` (==mutator method==)

  - return: the removed element (last) from the array; undefined if the array is empty.

- **.push()**: `arr.push(element(s))` (==mutator method==)

  - return: the new `length` property

- **.shift()**: `arr.shift()` (==mutator method==)

  - return: the removed element (first) from the array; undefined if the array is empty.

- **.unshift()**: `arr.unshift(element(s))` (==mutator method==)

  - return: the new `length` property

  <br>

- **.splice()**: `arr.splice(start[, deletecount][,additem(s)])` (==mutator method==)

  - return: an array containing the deleted elements
  - default `[deletcount]` = `array.length` - `start` (number of elements in array), if omitted, will delete all elements in array and return them in an array.
    > let arr = [1,2,3]
    > let removed = arr.splice(0)
    >
    > // arr is []
    > // removed is [1,2,3]

<br>

#### **Array callback methods**

- `CallbackFn` types (_f_): (`thisArg` is used as `this` when executing `callbackFn`)

  - Arrow function: `(element[, index][, array]) => {/*...*/}`
  - Callback function: `callbackFn[, thisArg]`
  - Inline callback funciton: `function(element[, index][, array]) {/*...*/} [,thisArg]`

- ==Note==: `index` manipulation during iteration doesn't affect next iteration, this is different from `for (let i = 0; i < array.length; i++)`iteration
  <br>

- **.every(_f_)**: return `true` if `callbackFn` returns a truthy value for ==every== `element`
  **.some(_f_)**: return `true` if `callbackFn` returns a truthy value for ==at least one== `element`
  <br>

- **.forEach(_f_)**: return `undefined`, it executes `callbackFn` once for ==each== `element`
- **.map(_f_)**: return a new `array` with the results of `callbackFn` for ==each== `element`
- **.reduce(_f_)**: return the =="accumulated"== value from running `callbackFn` over the entire array

  - `element` here are two arguments: `accumulator` & `currentElement`
  - `[index]` here is `[currentElementIndex]`
  - no `thisArg`, instead there is a `[initialValue]`, it could be any value
  - if `[initialValue]`:
    - `accumulator` = `[initialValue]`
    - `currentElement` = `array[0]`
    - start from first element `array[0]`
  - if no `[initialValue]`:
    - `accumulator` = `array[0]`
    - `currentElement` = `array[1]`
    - start from second element `array[1]`

- **.reduceRight(_f_)**: same as `.reduce()`, but the order is right-to-left
  <br>

- **.find(_f_)**: return the ==first== `element` in array which makes `callbackFn` return `true`, or `undefined` if not found
- **.findIndex(_f_)**: return ==index of the first== `element` in the array which makes `callbackFn` return `true`, or `-1` if not found
- **.filter(_f_)**: return a ==new array== with all the `elements` which makes `callbackFn` return `true`, or `[]` if no `element` is found
  <br>
- **.sort(_f_)**: return the ==sorted array==

  - `arr.sort([compareFn(a,b)])` - `compareFn` return negative: a placed before b - `compareFn` return positive: b placed before a - `compareFn` return `0`: a, b order unchange - if omit `compareFn`, a & b are converted to strings, then sorted according to each `char` Unicode value

<br>
##### **[Back to table](#table)**
---

## Object {#object}

- { key : value } pair
  - key: string (identifier)
  - value: anything (primitive data, array, function, other objects)
    <br>
- property accessors: dot(`.`) & bracket notation(`[]`)
  - `const obj = {'name' : 'Xiao', '2' : 2}`
  - `obj.name = 'Xiao'`
    - ~~`obj.2`~~
  - `obj['name'] = 'Xiao'`
  - `obj[2] = 2`
    - ~~`obj[name]`~~
  - when working with variables: `let key = 'name'`
    - `obj[key] = 'Xiao'`
    - ~~`obj.key`~~
      <br>
- Properties can be enumerated (for...in loop) if they are enumerable

  <br>

- Object manipulation

  - add: `obj[newKey] = newValue`
  - update: `obj[key] = newValue`
  - delete: `delete obj[key]` or `delete obj.keyValue`

    <br>

#### **Methods**:

- functions in objects
- `obj[methodName] = function () {/*...*/}`
- shorthand: `const obj = { methodName(){/*...*/} }`
- method invoke: `obj.methodName()`

  <br>

- Static methods:
  <detail>

  - **Object.is()**: `Object.is(value1, value2)`

    - return: A Boolean indicating whether or not the two arguments are the same value.
    - truthy: both `undefined`/`null`/`NaN`/`true` or `false`/same strings/same reference/same number/`+0` or `-0`
    - vs `==`:

  - **Object.assign()**: `Object.assign(target, ...sources)`

    - return: modified target object
    - Update target properties by properties in the sources if they have the same key
    - Define new properties to target if not exist

    ```
    const target = { a: 1, b: 2 };
    const source = { b: 4, c: 5 };
    const returntarget = Object.assign(target, source);

    console.log(target);   // expected output: Object { a: 1, b: 4, c: 5 }
    console.log(returntarget);   // expected output: Object { a: 1, b: 4, c: 5 }
    ```

      <br>

  - **Object.create()**: `Object.create(proto[, propertiesObject])`

    - return: a new object with the specified prototype object [and properties]
    - `propertiesObject`:

      ```
      {
        propName:{
        /* Data descriptors or accessor descriptors */
        }
      }
      ```

      <br>

  - **Object.defineProperty()**: `Object.defineProperty(obj, prop, descriptor)`

    - return: the object that was passed to the function
    - `prop`: the name or Symbol of the property to be defined or modified
    - `descriptor`: objects, could be data descriptor or accessor descriptor

      - _**data descritpor**_: a property that has a value
        - configurable [false]: true if this `prop` descriptor may be changed and this `prop` could be deleted from object
        - enumerable [false]: true if this `prop` shows up during enumeration (e.g., `for...in` loop, `console.log()` and `Object.keys()` returns enumerable properties only)
        - ==value== [undefined]: property value
        - ==writable== [false]: true if value can be changed with an assignment operator
      - _**accessor descriptor**_ : a property described by a getter-setter pair of functions
        - configurable [false]: same as in _data decsriptor_
        - enumerable [false]: same as in _data decsriptor_
        - ==get== [undefined]: a function serves as a _getter_ for the property
        - ==set== [undefined]: a function serves as a _setter_ for the property

    ```
    const object1 = {};
    Object.defineProperty(object1, 'property1', {
      value: 42,
      writable: false
    });
    ```

  - **Object.defineProperties()**: `Object.defineProperties(obj, props)`

    - return: the object that was passed to the function
    - props: `{prop1:{descriptors}, prop2:{descriptors}}`

      <br>

  - **Object.getOwnPropertyDescriptor()**: `Object.getOwnPropertyDescriptor(obj, prop)`

    - return: A property `descriptor` of the given property if it exists on the object, `undefined` otherwise.

  - **Object.getOwnPropertyDescriptors()**: `Object.getOwnPropertyDescriptors(obj)`

    - return: An object containing all own property descriptors of an object. Might be an empty object, if there are no properties.

    <br>

  - **Object.keys()**: `Object.keys(obj)`

    - return: an array of strings representing all the ==enumerable== properties

  - **Object.values()**: `Object.values(obj)`

    - return: an array containing all the ==enumerable== property values

      <br>

  - **Object.entries()**: `Object.entries(obj)`

    - return: An array of the given object's own enumerable string-keyed property `[key, value]` pairs.

  - **Object.fromEntries()**: `Object.fromEntries(iterable)`

    - return: A new object whose properties are given by the entries of the iterable.

  - `Object.fromEntries()` performs the reverse of `Object.entries()`:

    ```
    const entries = [
      ['foo', 'bar'],
      ['baz', 42]
    ];

    const obj = {
      foo: 'bar',
      baz: 42
    };

    const entriesReturn = Object.entries(obj);
    // entriesReturn = [
    //   ['foo', 'bar'],
    //   ['baz', 42]
    // ];

    const fromEntriesReturn = Object.fromEntries(entries);
    // fromEntriesReturn = {
    //   foo: 'bar',
    //   baz: 42
    // };
    ```

    <br>

  - **Object.getPrototypeOf()**: `Object.getPrototypeOf(obj)`
    - return: The `[[Prototype]]` of the given object, which may be `null`.

  <br>

  - **Object.hasOwn()**: `Object.hasOwn(instance, prop)`

    - return: `true` if the specified object has directly defined the specified property. Otherwise `false`
    - `Object.hasOwn()` is recommended over `Object.prototype.hasOwnProperty()` because it works for objects created using `Object.create(null)` and with objects that have overridden the inherited `hasOwnProperty()` method.

  - <br>

<br>
##### **[Back to table](#table)**
---

## Function {#function}

Every JS function is a `Function` object: `(function(){}).constructor === Function //true`

- **argument**: value passed to function during function invocation
- **parameter**: placeholder in function definition

- function properties:

  - length: the number of parameters expected by the function

  - name: the name of the function

  - prototype: A Function object's prototype property is used when the function is used as a constructor with the new operator. It will become the new object's prototype.

  - getter:

  - setter:

#### **factory function**

(==not recommanded==): a function creates and returns a new object

```

function createPerson(name, age) {
  return {
    Name: name,
    Age: age,
    getPersonInfo() {
      return name + ',' + age
    },
  }
}
```

- Methods are duplicated in objects created by factory function, `Object.create()` could be used in facotry function using an existing object as the prototype of the new object

```
const personAction = {
  getAge() {
    return this.Age
  },
};

function createPerson(name, age) {
  let person = Object.create(personActions);
  person.Name = name;
  person.Age = age;
  return person;
}
```

<br>

#### **Constructor**

A special function that can only be called with `new` operator

- **Create constructor**:

```
function ConstructorName(prop) {
  this.prop = prop;
  this.method1 = function () {}
}
```

**Note**: methods created in constructor definition is ==duplicated in every instance==
<br>

- **Add shared methods**:

```
ConstructorName.prototype.method2 = function () {};
```

methods created inside of constructor prototype is shared with all instances.

<br>

- **Create object instance**:

```
const instance = new ConstructorName(prop)
```

`new` operator would do the following:

1. Create a empty object (e.g., `newInstance`)
2. Points the `[[Prototype]]` of `newInstance` to the constructor function's `prototype` property
3. Executes the constructor function with the given arguments, binding `newInstance` as the `this` context
4. If the constructor function returns a non-primitive, this return value becomes the result of the whole `new` expression. Otherwise, if the constructor function doesn't return anything or returns a primitive, `newInstance` is returned instead.

without `new` operator, `this` refers to global object.

(In constructor definition, use `try ... catch` with `new.target` to detect whether a function or constructor was called using `new` operator)

<br>

#### **Class**

(==introduced after ES6==) Declared with keyword `class`, encapsulates constructor(can only have one constructor) and shared methods

```
class Person {
  constructor(name) {
    this.name = name;
  }
  getName() {
    return this.name;
  }
}
```

- Main differences with constructor function:

|                    |          Constructor           |                         Class                         |
| :----------------: | :----------------------------: | :---------------------------------------------------: |
|    Declaration     |         can be hoisted         |                      not hoisted                      |
|     Execution      |        non-strict mode         |                      strict mode                      |
| Shared properties  | added to constructor prototype | created in Class declaration (outside of constructor) |
|  &#8970; writable  |              true              |                         false                         |
| &#8970; enumerable |              true              |                         false                         |

**==Note==**: **non-writable** (`writable: false`) means it cannot be assigned to something else, but it still **can be changed** by adding or deleting properties from inside

- **instanceof**: `object instancof constructor/class`

  - check if `constructor/class.prototype` (not [\[Prototype]]) in object's `[[Prototype]]` chain.

- **extends & super**:

  - **extends**: chain the `prototype` of ParentClass to be the `[[Prototype]]` in the `prototype` of ChildClass, so that childInstance will have access to the ParentClass methods from the `[[Prototype]]` chain

  ```
  class ChildClass extends ParentClass { /* ... */ }
  const parentInstance = new ParentClass()
  const childInstance = new ChildClass()

  // use of __proto__ is not recommended, below is just for clarification

  ChildClass.prototype.__proto__ === ParentClass.prototype // true
  childInstance.__proto__.__proto__ === parentInstance.__proto__  // true
  ```

  - **super**: used in the constructor body of a derived class (with extends), or as a "property lookup" (`super.prop` and `super[expr]`)

    - when used as a "function call":
      - calls the parent class's constructor
      - binds the parent class's public fields
      - then the derived class's constructor can further access and modify `this`
      - must be called before the `this` keyword is used, and before the constructor returns.
    - when used in "property lookup" form
      - access methods and properties of an object literal's or class's `[[Prototype]]`

    <br>

**Public class fields**

Public static fields

<br>
##### **[Back to table](#table)**
---

## Hoist {#hoist}

Take part of the code and move it to the top of the file

- **Hoisting function**: only work with normal `function` declaration

```

funcName() // This works
...
function funcName(){}

```

- **Hoisting variable**: only variable declared with `var` can be hoisted, but its value would be undefined before initialization. (`var` is less used than `let` and `const`)

```

console.log(x) // undefined
var x = 1
console.log(x) // 1

```

<br>
##### **[Back to table](#table)**
---

## Promise {#promise}

Promise is a object represents the resulting value of an asynchronous operation, working as a proxy for a value that was not necessarily known when the promise is created.

```

new Promise(executor)
new Promise((resolve, reject) => {
  // do something asynchronous which eventually calls either:
  // resolve(someValue) // fulfilled
  // or
  // reject("failure reason") // rejected
})

```

- return: a promise object, has three states:
  - pending: initial state, neither fulfilled nor rejected.
  - resolved: meaning that the operation was completed successfully.
  - rejected: meaning that the operation failed.
- executor: a function called "executor function", which takes two functions as parameters (resolve, reject)

  <br>
Promises uses microtasks queue to handle `.then/catch/finally`
  - The queue is first-in-first-out(FIFO);
  - only resolved/rejected promise handlers can be enqueued, pending
  - Execution of a task is initialted only when nothing else is running (empty call stack)

<br>
##### **[Back to table](#table)**
---

## Async/await {#async_await}

- `async` functions always return a `promise`. If the return value of an `async` function is not explicitly a `promise`, it will be implicitly wrapped in a `promise`.
- The body of an `async function` can be thought of as being split by zero or more `await` expressions.
- ==Top-level code==, up to and including the first `await` expression (if there is one), is run ==synchronously==.
  - an `async` function ==without== an `await expression` will run ==synchronously==.
  - when there is an `await expression` inside the function body, the `async` function will always complete ==asynchronously==.
- An `await` splits execution flow, allowing the caller of the `async` function to resume execution.
  - **Important**: only when `expression` is resolved, the function can resume
  - **Imagine**: `await expression` wraps the rest of codes in current function as a promise handler callback, and only when `await expression` resolve/reject, this handler callback is pushed in the microtask queue
- After the `await` defers the continuation of the `async` function, execution of following statements resumes.

```

async function name (args) {
  // ...statement...
  // [...await... ] // execute synchronously
  // [...statement...] // continue only when first await finished
  // [...await...]
  // ...
}
```

<br>
##### **[Back to table](#table)**
---
## Regular expression {#RegExp}

- Patterns used to ==match== character combinations in strings
- Regular expressions are also objects
- Regular expressions are used with the RegExp methods
- Two ways to create a `RegExp` object: a literal notation and a constructor:
  - **literal notation** : a pattern between two slashes, followed by optional flags
    - `let re = /ab+c/i`
  - **constructor function**: two parameters(a string or a RegExp object as its first parameter, and a string of optional flags as its second parameter)
    - `let re = new RegExp('ab+c', 'i')`

Assertion

<br>

Character classes

<br>

Quantifiers

- **x?**: 0 or 1
- **x+**: 1 or more
- **x\***: 0 or more
  <br>

RegExp methods

- re.test()
-

<br>
##### **[Back to table](#table)**
---

## Interesting concepts {#interesting}

1. **A function to return one of two functions based on their execution results, which can only be decided during function invocation.**

```

function eitherCallback(callback1, callback2) {
  return (x)=>{
    return callback1(x) || callback2(x)
  }
}
```

---

2. **There are two types of expressions**:

   1. those that assign value to a variable with side effects: `x = 1`
   2. those that in some sense evaluate and therefore resolve to a value `1 + 2`

---

3. **Check if a Character is a Letter**
   Compare the lowercase and uppercase variants of the character
   `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`

---

4. **Deep copy an array**
   `arrayCopy = [...array]`

---

5. **Capitalize a string**
   `string.charAt(0).toUpperCase() + string.slice(1)`

---

6. **DP problem common characteristics:**

   - Ask for optimum value:

     - Ask for max/min/longest etc. of something;
     - Ask for the number of ways to do something;

   - The future decisions depend on earlier decisions

     - distinguish DP problem from greedy algorithm / divide and conquer problem

    <br>

   - tips:
     - DP[i] should have close connection to nums[i];

---

7. **In `for` loop, the condition could be anything, it doesn't have to be related to `i`.**

```
let y = 3;
for (let i = 0; y < 5; i++) {
    y += i;
    console.log(y);
}

// 3
// 4
// 6
```

---

8. **Create an array with**
   <br>

##### **[Back to table](#table)**

# Javascript notes

## Table {#table}

- [Js Primitive Types](#js-primitive)
- [Boolean](#boolean)
- [Null](#null)
- [Undefined](#undefined)
- [Numbers](#number)
- [String](#string)
- [Symbol](#symbol)
- [Operator](#operator)
- [Regular Expression](#RegExp)
- [Array](#array)
- [Object](#object)
- [Set](#set)
- [Map](#map)
- [Function](#function)
- [Hoist](#hoist)
- [Asynchronous Javascript](#asynchronous-js)
- [Promise](#promise)
- [Async/await](#async_await)
- [Event loop and macrotask vs microtask](#eventloop)
- [DOM Traversal](#dom)
- [Web APIs](#webapis)
- [Web-related terms](#webterms)
- [Interesting topics](#interesting)

---

## Js Primitive Types {#js-primitive}

- Number, String, Boolean, null, undefined, BigInt, Symbol (#js primitive)

- `var.valueOf()`: return the primitive value
- `typeof var`: return the variable type in `string` format

Primitives are immutable, can be **replaced** but **not directly altered**, e.g.,:

    var str = "cool";
    str[2] = "l"; /*This doesn't work*/

- Another data type is **composite** (reference) type: constructed using primitive data types
  and other composite types.

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
  - `Number.isNaN('a') // false`

- `isFinite() / isNaN()` : coerced to `number` type, then test for `finite`/`NaN`

  - `isNaN()` will only give `false` when the input is `number` or number in string type.
  - `isNaN('3') // false`
  - `isNAN('a') // true`;
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
- Backslash (`\`) turns special characters (such as quote `'` or double quote `"`) into string characters. Use `\` to escape `'`, `"` and `\` in string (the escape backslash will only exist in the string value, it is not a string character and it can not be printed out by console.log):

  | Code | Result | Description  |
  | :--: | :----: | :----------: |
  | `\\` |  `\`   |  Backslash   |
  | `\'` |  `'`   | Single quote |
  | `\"` |  `"`   | Double quote |
  | `\t` |        |     Tab      |
  | `\n` |        |   Newline    |
  | ...  |        |   and more   |

  - `'\'` can not be printed out, because it escapes the closing single quote (`'`), which turns into a string character not a funcitonal character

  <br>

#### **String methods**

- **str.length** : return the length of `str`

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
  - `[seperator]`: if leave blank, will put entire string as only element in an array, `'abc'.split(); // ['abc']`
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
## Operator {#operator}

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

- **.find(_f_)**: return the **first** `element` in array which makes `callbackFn` return `true`, or `undefined` if not found
- **.findIndex(_f_)**: return **index** of the first `element` in the array which makes `callbackFn` return `true`, or `-1` if not found
- **.filter(_f_)**: return a **new array** with all the `elements` which makes `callbackFn` return `true`, or `[]` if no `element` is found
  <br>
- **.sort(_f_)**: return the sorted array (==mutator method==)

  - `arr.sort([compareFn(a,b)])`
  - `compareFn` return negative: a placed before b
  - `compareFn` return positive: b placed before a
  - `compareFn` return `0`: a, b order unchange
  - if omit `compareFn`, a & b are converted to strings, then sorted according to each `char` Unicode value

<br>
##### **[Back to table](#table)**
---

## Object {#object}

- { key : value } pair
  - key: string (identifier), anything other than string will be forced to string type
  - value: anything (primitive data, array, function, other objects)
    <br>
- property accessors: dot(`.`) & bracket notation(`[]`)
  - `const obj = {'name' : 'Xiao', '2' : 2}`
  - `obj.name = 'Xiao'`
    - ~~`obj.2`~~
  - `obj['name'] = 'Xiao'`
  - `obj[2] = 2`
  - `obj['2'] = 2`
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

    - return: always return an empty object, with the specified \_\_proto\_\_ object [and properties]
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

      - _**data descritpor**_: a property that has a value [default]
        - configurable [`false`]: true if this `prop` descriptor may be changed and this `prop` could be deleted from object
        - enumerable [`false`]: true if this `prop` shows up during enumeration (e.g., `for...in` loop, `console.log()` and `Object.keys()` returns enumerable properties only)
        - ==value== [`undefined`]: property value
        - ==writable== [`false`]: true if value can be changed with an assignment operator
      - _**accessor descriptor**_ : a property described by a getter-setter pair of functions
        - configurable [`false`]: same as in _data decsriptor_
        - enumerable [`false`]: same as in _data decsriptor_
        - ==get== [`undefined`]: a function serves as a _getter_ for the property
        - ==set== [`undefined`]: a function serves as a _setter_ for the property

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
    - **non-negative integer** keys will be stored **_in front of_** `String` keys or float or negative number keys when using `Object.keys()`

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

  <br>

#### **Error Object**:

`Error` objects are thrown when runtime errors occur. The `Error` object can also be used as a base object for user-defined exceptions.

- **Constructor**: `Error([message, options])`
  - `Error()` can be called with or without `new`. Both create a new `Error` instance.
    <br>
- **Instance properties**:
  - `err.message`: string, for user-created Error objects, this is the string provided as the constructor's first argument.
    ```
    const e = new Error("Could not parse input"); // e.message is 'Could not parse input'
    throw e; // get error: 'Uncaught Error: Could not parse input'
    ```
  - `err.name`: string, the initial value is `'Error'`, can be redefined
    ```
    const e = Error()
    console.log(e.name) // 'Error'
    e.name = 'ParseError';
    console.log(e.name) // 'ParseError'
    ```
  - `err.casue`: The value of cause can be of any type. The value that was passed to the `Error()` constructor in the `options.cause` argument. It may not be present. If presents, it indicates the specific original cause of the error.
    ```
    try {
      connectToDatabase();
    } catch (err) {
      throw new Error('Connecting to database failed.', { cause: err });
    }
    ```
- **Instance methods**:
  - `err.toString()`: return a string representing the specified `Error` object.
    ```
    const e = new Error("Could not parse input");
    e.name = 'ParseError';
    e.toString(); // 'ParseError: Could not parse input'
    ```
    <br>

##### **[Back to table](#table)**

---

## Set {#set}

The Set object lets you store **unique** values of any type, whether primitive values or object references.

- `Set`: set constructor, work with `new` to creates a new Set object.
  <br>

##### **[Back to table](#table)**

---

## Map {#map}

- The `Map` object holds key-value pairs and remembers the ==original insertion order== of the keys.
- Any value (both **objects** and **primitive values**) may be used as either a **key** or a **value**.

<br>
##### **[Back to table](#table)**

---

## Function {#function}

Every JS function is a `Function` object: `(function(){}).constructor === Function //true`

- **argument**: value passed to function during function invocation
- **parameter**: placeholder in function definition

- function default properties:

  - length: the number of parameters expected by the function

  - name: the name of the function

  - ==prototype==: A Function object's prototype property is used when the function is used as a constructor with the new operator. It will become the new object's prototype.

  - getter:??

  - setter:??

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

A special function that can only be called with `new` operator, capitcalized first letter

- **Create constructor**:

```
function ConstructorName(prop) {
  this.prop = prop;
  this.method1 = function () {}
}
```

**Note**: methods created in constructor definition is ==duplicated== in every instance
<br>

- **Add shared methods**:

```
ConstructorName.prototype.method2 = function () {};
```

methods created inside of constructor prototype is ==shared== with all instances.

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

(==introduced after ES6==) Declared with keyword `class`, encapsulates `constructor` (reserved key word, can only have one) and shared methods

```
// class declaration
class Person {
  constructor(name) {
    this.name = name;
    ObjectLiteralMethod: function(){};
  }
  classPrototypeProperty() {
    return this.name;
  }
}

// class expression
const Person = class [className] {
  constructor(name) {
    this.name = name;
    ObjectLiteralMethod: function(){};
  }
  classPrototypeProperty() {
    return this.name;
  }
}
```

To declare a variable within a class, it needs to be a property of the class or, scoped within a method in the class. It's all about scoping and **variables are not supported in the scope definition of a class**
<br>

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

## Asynchronous Javascript {#asynchronous-js}

- AJAX is **asynchronous javascript and XML**, it is a combination of:
  - A browser built-in `XMLHttpRequest` object (to request data from a web server)
  - JavaScript and HTML DOM (to display or use the data without the necessity to reloading the page).
    <br>
- _**Asynchronous**_ means something happens in the future, not right now.
- Javascript is just a programming language that is implemented in browsers.
- Browsers are usually written by C++, which can do things that JS is bad at, hence ==Web APIs== in general.
  <br>
- XML vs JSON

  - XML (eXtensible Markup Language) is a data format, similar to HTML, but it does not describe presentation like HTML.
    - The name of the tag is to represent data meaning, it is meaningless to the browser
    ```
    <pin>
      <title>This is a title</title>
      <author>This is the author</author>
      <year>This is when it is wrote</year>
    </pin>
    ```
  - JSON (Javascript Object Notation) is a more commonly used data format, much easier for API's to parse, so AJAX(XML) is basically AJAJ(JSON) nowadays.

    - JSON doesn't support comments, all the strings must be **double quoted**.
    - Data is in name / value pairs, separated by commas.
    - Values must be string, number, object, array, boolean or null.
    - No function, date or undefined.
    - pros:
      - lightweight (small file size) and easy to read/write
      - integrates easily with most languages

    ```
    "book": {
      "title": "Three body problem",
      "author": "Cixin Liu",
      "year": 2008
    }
    ```

    - `JSON.stringify(value[, replacer][, space])`

      - `Boolean`, `Number`, `String` and `BigInt` are converted to the corresponding primitive values during stringification
      - `Object` (including `Array`) is recursively stringified
      - `undefiend`, `Function` and `Symbol` value will be omitted (in object) or changed to `null` (in array) or return `undefined` (directly passed in)
      - `Infinity`, `NaN` and `null` are all considered `null` and will not be omitted.

      - My understanding: Since strings in JSON data are all double quoted, to make valid json string and to avoid the conflict of meanings, `JSON.stringify()` works as:
        1. turn all string syntax (`'`, `` ` ``) into double quotes (`"`)
        2. For all string character double quotes`"`, preattach a backslash (`\`) to make it non-syntax character.
        3. stringify everyting, use a second `\` to escape any `\`, `"`, and the second `\` will not be printed out by console.log, cause they are escape character.

      ```
      const str_error = """;  // SyntaxError

      const str1 = '"';
      const jsonStr1 = JSON.stringify(str1);   // jsonStr1 = '"\\""'
      console.log(jsonStr1);    // output: "\"" , only one backslash when printing

      jsonStr1 === JSON.stringify("\"");  // true
      ```

      <br>

1.  In early days, asynchronous APIs used event handler (AJAX).

    - Browser APIs — constructs built into the browser that sits on top of the JavaScript language and allows you to implement functionality more easily.
      <br>
    - APIs don't respond with HTML. APIs respond with **pure data** (XML and JSON), not structure.
      <br>

    ```
    var xhr = new XMLHttpRequest();

    xhr.onreadystatechange = function() {
      if (xhr.readyState === 4 && xhr.status === 200) {
        console.log(xhr.responseText);
      }
    }

    xhr.open(method, url); // methods: "GET", "POST", "HEAD", "PUT", "DELETE", "OPTIONS", etc.
    xhr.send([data]); //
    ```

      <br>

    - [XMLHttpRequest docs](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/XMLHttpRequest)
      <br>
    - **Event handler**: the function that will be called when the event happens.
      <br>
    - `XMLHttpRequest` is a constructor, `new` operator required:
      - `const xhr = new XMLHttpRequest()` : returns a `XMLHttpRequest` object, which is not a promise
        <br>
    - `xhr.readyState`: returns the state an XHR client is in.

    | Value | State            | Description                                                    |
    | :---: | ---------------- | -------------------------------------------------------------- |
    |   0   | UNSENT           | Client has been created, `open()` not called yet               |
    |   1   | OPENED           | `open()` has been called                                       |
    |   2   | HEADERS_RECEIVED | `send()` has been called, and headers and status are available |
    |   3   | LOADING          | Downloading; `responseText` holds partial data                 |
    |   4   | DONE             | The operation is complete                                      |

      <br>

    - `xhr.onreadystatechange` is an event handler, it defines a function that **will be called** ==whenever== `readyState` changes

      - check when if the request is done:
        ```
        xhr.onreadystatechange = function () {
          if (xhr.readyState === 4) {
            // do something when XMLHttpRequest is done
          }
        }
        ```
        <br>

    - `xhr.addEventListener('event', (e) => {})` other XHR 'events' (or just use event handler):

      - `'loadstart'`, `xhr.onloadstart = (e) => {}` : fired when a request has started to load data
      - `'load'`, `xhr.onload = (e) => {}` : fired when a request transaction completes successfully
      - `'loadend'`, `xhr.onloadend = (e) => {}` : fired when a request has completed (`load`/`abort`/`error`)
      - `'progress'`, `xhr.onprogress = (e) => {}` : fired periodically when a request receives more data.
      - `'error'`, `xhr.onerror = (e) => {}` : fired when the request encountered an error
      - `'abort'`, `xhr.onabort = (e) => {}` : fired when a request has been aborted
      - `'timeout'`, `xhr.ontimeout = (e) => {}` : fired when progression is terminated due to preset time expiring
        <br>

    - `xhr.open()`: initializes a newly-created request, or re-initializes an existing one.
      <br>
    - `xhr.send([data])`: sends the request to the server.
      <br>
    - `xhr.status` returns the numerical HTTP status code of the `XMLHttpRequest`'s response

      - [HTTP Status Codes Cheat Sheet](https://www.restapitutorial.com/httpstatuscodes.html)
        - successful responses: 200-299
        - Redirection message: 300-399
        - Client error responses: 400-499
        - Server error responses: 500-599
        - [Cut puppy reference](https://httpstatusdogs.com/)
      - check if xhr is succeeded: `if (xhr.status === 200) { ... }`
        <br>

    - `xhr.responseText` returns the text received from a server following a request being sent.
      - the return is string, and it needs to be parsed before getting access to the actual data
      - JSON parser: `const data = JSON.parse(xhr.responseText)`
        <br>
    - `method`: request type, these are equivalent to the **CRUD** operations (create, read, update, and delete).

      - `GET`: retrieve some data
      - `POST`: give data to the server
      - `PUT`: update entire entry
      - `PATCH`: update a piece of an entry
      - `DELETE`: delete an entry
        <br>

    - Problems with XHR:
      - bulky syntax
      - old
      - no streaming
        <br>

1.  **Fetch API** (an update to XHR) is provided by browsers (webapi) based on [chained promise](#promise)

    - nice and clean
    - more powerful functionalites

    ```
    fetch(url)                    // That's it, no XMLHttpRequest() constructor, no open(), no send()
    .then(function(res) {         // fetch will return a promise, whose resolved value is a 'response' object,
      return res.json();
    }).then(function(data) {
      console.log(data);
    }).catch(function(e) {
      console.log('problem!')
    });
    ```

    - Fetch Intefaces
      - `fetch(resource[, options])`: method used to fetch a resource.
        - return: a `Promise` that resolves to a `Response` object
        - options: an object, can include {parameters / value} pairs
        - ==only reject== when a network error is encountered (does not reject on HTTP errores)
      - `Headers`: Represents response/request headers, allowing you to query them and take different actions depending on the results.
      - `Request`: Represents a resource request.
      - `Response`: Represents the response to a request.
        - `Res.json()`: Returns a `Promise` that resolves with the result of parsing the response body text as JSON.
      - [more details](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
        <br>

1.  **jQuery AJAX**: jQuery is 'The Write Less, Do More JavaScript **Library**' (based on JS)

    - [Docs](https://api.jquery.com/)
    - tons of functionality, not just AJAX
    - heavy library
    - Install: npm or CDN (content delivery network) or many other ways
      <br>
    - **jQuery AJAX** is another way of sending http request (evetually based on `XHR`), mainly differs from **fetch**:
      - jQuery AJAX could respond to HTTP error
      - jQuery AJAX could receive cookies from server
        <br>
    - The 'base' jQuery AJAX Method: `$.ajax([url][, settings])`

      - `$.ajax()` is the same as `jQuery.ajax()`
      - settings`{ ... }`: A set of key/value pairs that configure the Ajax request
        - common settings:
          - method: HTTP method to use for the request (default: `GET`)
          - url: the URL to which the request is sent (default: `The current page`)
          - data: data to be sent to the server
          - datatype: type of data expected from the server (default: `Intelligent Guess (xml, json, script, or html)`)
          - cache: If set to `false`, it will force requested pages not to be cached by the browser. (default: `true, false for dataType 'script' and 'jsonp'`)
          - `success`: A ==function== to be called if the request succeeds. Arguments: **the data returned from the server** (formatted according to the dataType parameter or the dataFilter callback function, if specified), **a string describing the status**, and **the `jqXHR` object**.
            ...
            <br>

    - 3 Shorthand methods that are commonly used:

      - `$.get(url[, data][, success][, dataType])` same as below:
        - `success`: cb, Required if dataType is provided, but you can use null or jQuery.noop as a placeholder.

      ```
      $.ajax({
        url: url,
        data: data,
        success: success,
        dataType: dataType
      });
      ```

      <br>

      - `$.post(url[, data][, success][, dataType])` same as below:
        - `success`: cb, Required if dataType is provided, but you can use null

      ```
      $.ajax({
        type: "POST",
        url: url,
        data: data,
        success: success,
        dataType: dataType
      });
      ```

      <br>

      - `$.getJSON(url[, data][, success])` same as below:

      ```
      $.ajax({
        dataType: "json",
        url: url,
        data: data,
        success: success
      });
      ```

      <br>

1.  **Axios**: a lightweight HTTP request **library** (HTTP request only)
    - [Docs](https://axios-http.com/docs/intro)
    - Install: npm or CDN
    - get request:
      ```
      axios.get(url)
      .then(function(res){ ... })
      .catch(function(err){ ... })
      ```
      - have nice error handlers: `error.request` / `error.response`
      - Axios vs Fetch
        | Axios | Fetch |
        | :--- | :--- |
        | Axios has `url` in request object.| Fetch has no `url` in request object. |
        | Axios is a **stand-alone third party package** that can be easily installed. |Fetch is built into most modern browsers; **no installation** is required as such.|
        | Axios enjoys built-in XSRF protection. |Fetch does not.|
        | Axios uses the `data` property. |Fetch uses the `body` property.|
        | Axios’ data contains the `Object`. |Fetch’s body has to be **stringified**.|
        | Axios request is ok when `status` is `200` and `statusText` is `OK`. |Fetch request is `ok` when **response object contains** the `ok` property.|
        | Axios performs **automatic transforms of JSON data**. |Fetch is a **two-step process** when handling JSON data- first, to make the actual request; second, to call the .json() method on the response.|
        | Axios allows **cancelling request and request timeout**. |Fetch does not.|
        | Axios has the ability to **intercept HTTP requests**. |Fetch, by default, doesn’t provide a way to intercept requests.|
        | Axios has **built-in support for download progress**. |Fetch does not support upload progress.|
        | Axios has **wide browser support**. |Fetch only supports Chrome 42+, Firefox 39+, Edge 14+, and Safari 10.1+ (This is known as Backward Compatibility).|
        | Axios `GET` call can have body Content |Fetch `GET` call cannot have body Content|
        <br>

##### **[Back to table](#table)**

---

## Promise {#promise}

Promise is an object represents the resulting value of an ==asynchronous operation==, working as a proxy for a value that was not necessarily known when the promise is created.

- return: a promise object, has three states:
  - pending: initial state, neither fulfilled nor rejected.
  - resolved: meaning that the operation was completed successfully. (Colloquially, 'resolved' equals 'fulfilled')
  - rejected: meaning that the operation failed.
- executor: a function called "executor function", which takes two functions as parameters (resolveFunc, rejectFunc)
  - executors are called synchronously, as soon as the Promise is `constructed`
    <br>

```
new Promise(executor) // only work with 'new' operator
new Promise((resolveFunc, rejectFunc) => {
  // do something asynchronous which eventually calls either:
  // resolveFunc(someValue) -- fulfilled
  // or
  // rejectFunc(reason) -- rejected
})
```

<br>

Promises are handled by [microtasks queue](#eventloop)

- The queue is first-in-first-out(FIFO);
- only resolved/rejected promise handlers can be enqueued, pending promises will not be enqueued until settled
- Execution of a task is initialted only when nothing else is running (empty call stack)
  <br>

==Chained Promises==: `Promise.prototype.then/catch/finally`<br>

- `then(onFulfilled[, onRejected])`: Returns a new `Promise` immediately. This new promise is always `pending` when returned, regardless of the current promise's status.

  ```
  promise.then(onFulfilled[, onRejected])

  promise.then(
    (value) => { /* fulfillment handler */},
    [(reason) => { /* rejection handler */}]
  )
  ```

  - When `onFulfilled` is not a function: internally replaced with an **_identity_** function `(x) => x`, which ==passes== the `fulfillmentValue`
  - When `onRejected` is not a function: internally replaced with an **_thrower_** function `(x) => throw x`, which ==throws== the `receivedRejectionReason`
    <br>
  - Assuming `x` is the return of `onFulfilled` / `onRejected`, and `p` is the return promise of `then()`:
    - `x` is a value ==> `p` is resolved with value `x`
    - `x` is `undefined` ==> `p` is resolved with `undefined`
    - `x` is an error throwed by handler ==> `p` is rejected with value `x`
    - `x` is a resolevd promise ==> `p` is resovled with `x`'s value
    - `x` is a rejected promise ==> `p` is rejected with `x`'s value
    - `x` is pending promise ==> `p` is pending until `x` is settled, then apply rules above
      <br>

- `catch(onRejected)`: Internally calls `Promise.prototype.then` on the object upon which it was called, passing the parameters `undefined` and the received `onRejected` handler. Returns the value of that call, which is a `Promise`.

  ```
  promise.catch(function(reason) {
    // rejection
  })
  ```

  - equals to `Promise.prototype.then(undefined, onRejected)`
  - The `Promise` returned by `catch()` will be ==fulfilled (resovled)== with the handler function `onRejected`'s return value unless `onRejected` ==throws an error== or returns an already ==rejected== `Promise`.

  - Example with comments

  ```
  const promise = new Promise((resolve, reject) => {
    reject('wrong');
  });

  promise.then(1, 2)
    .catch((e) => {
      console.log(e);
      return 'right';
    })
    .then((n) => {
      console.log(n);
    });

  // Here 'promise' is a rejected promise with rejected reason of 'wrong'
  // Since first 'then' has no onRejected handler,
      // number '2' is internally replaced with a thrower function ((x) => { throw x; }),
      // so the first 'then' returns a rejected promise with reason 'wrong'.
  // The following 'catch' has a onRejected handler,
      // but it doesn't throw an error or return a rejected promise,
      // instead it returns a string 'right'
      // therefore 'catch' returns a resolved promise with result value 'right'
  // The second 'then' following the resolved 'catch' promise, has a onFullfilled handler,
      // it receives the resolved value of 'right' and loggs it out,
      // but because it doesn't return anything,
      // the second 'then' will return a resolved promise with value of undefined
  ```

  <br>

- `finally(onFinally)`: Returns an **equivalent** `Promise` with its finally handler set to the specified function. - **Equivalent** means the returned `Promise` is the same as the original promise (the same `fulfilledValue` / `error`), unless the handler function `onFinally` ==throws an error== or returns an already ==rejected== `Promise`.

  - `onFinally` callback does not receive any argument.
    `promise.finally(() => { // Code that will run after promise is settled (fulfilled or rejected) })`
    <br>

  - `then` vs `reject` vs `finally`:

    ```
    Promise.resolve(2).then(() => 77, () => 88) // resolved with result 77
    Promise.resolve(2).finally(() => 77) // resolved with result 2

    Promise.reject(3).then(() => 77, () => 88) // resolved with result 88
    Promise.reject(3).finally(() => 88) // rejected with reason 3

    // Both return a rejected promise with reason 99
    Promise.reject(3).finally(() => {throw 99})
    Promise.reject(3).finally(() => Promise.reject(99))

    ```

  <br>

- `Promise.all([an array of promises])`: only ==resolve== when ==all== promises inside is ==resolved==, and it will resolve to an array of resolved values. It rejects when any of the input's promises rejects, with this first rejection reason.
- `Promise.any([an array of promises])`: will ==resolve== when ==any== promise inside is ==resolved==, and it will resolve to that resolved values. If all promises are rejected, it will reject with `AggregateError`, which is an object containing an array of rejection reasons.
- `Promise.race([an array of promises])`: will ==settle== when ==any== promise inside is ==settled==, and it will settles with the eventual state of the first promise that settles (resolved or rejected).

  <br>

##### **[Back to table](#table)**

---

## Async / await {#async_await}

- `async` functions always return a `promise`. If the return value of an `async` function is not explicitly a `promise`, it will be implicitly wrapped in a `promise`.
  <br>
- `await` is an ==operator==, its operand is a promise, a thenable object, or any value to wait for.
  - **return**: the ==fulfillment value== of the promise or thenable object, or the expression itself's value if it's not thenable. If the promise is not resolved, the await expression throws the rejected value.
  - It can only be used inside an async function or a JavaScript module.
    <br>

```
async function name (args) {
  // ...statement...
  // [...await... ] // execute synchronously
  // [...statement...] // continue only when first await finished
  // [...await...]
  // ...
}
```

- The body of an `async function` can be thought of as being split by zero or more `await` expressions.
  <br>
- ==Top-level code==, up to and including the first `await` expression (if there is one), is executed ==synchronously==.
  - an `async` function ==without== an `await expression` will run ==synchronously==.
  - when there is an `await expression` inside the function body, the `async` function will always complete ==asynchronously==.
    <br>
- An `await` splits execution flow, allowing the caller of the `async` function to resume execution.
  - **Important**: only when `expression` is resolved, the function can resume
  - **Imagine**: `await expression` wraps the rest of codes in current function as a promise handler callback, and only when `await expression` resolve/reject, this handler callback is pushed in the ==microtask queue==
    <br>
- After the `await` defers the continuation of the `async` function, execution of following statements resumes.

<br>
##### **[Back to table](#table)**
---
## Event loop and macrotask vs microtask {#eventloop}

- ==Macrotask queue== (or just **task queue** or **callback queue**): after web api handles the JS request, it passes callabcks to task queue which is handled by JS engine. Only after JS finishes all the codes, it starts to execute whatever is in the task queue chronologically (FIFO).
  <br>
- Promises are handled by ==microtasks queue==
  - The queue is first-in-first-out(FIFO);
  - only resolved/rejected promise handlers can be enqueued, pending
  - Execution of a task is initialted only when nothing else is running (empty call stack)
    <br>
- Event loop algorithm:

  - JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.
    <br>

  1. Dequeue and run the oldest task from the ==_macrotask_== queue (Attention: ==main script execution== is considered a ==_macrotask_==, so this part holds true).
  1. Execute all ==_microtasks_==:
     - While the microtask queue is not empty:
       - Dequeue and run the oldest microtask.
  1. Render changes if any.
  1. If the macrotask queue is empty, wait till a macrotask appears.
  1. Go to step 1.
     <br>

- Tasks in ==_macrotask_== queue or ==_microtask_== queue means the preparing work for the tasks is finished (e.g., promise resolved/rejected, settimeout countdown finished, etc.), so that the tasks can be executed directly.
  <br>
- In general, after main script is finished, all ==microtasks== will be executed before any ==macrotask==.
  <br>

##### **[Back to table](#table)**

---

## DOM Traversal {#dom}

[JS DOM Traversal Cheat Sheet](./JS%20DOM%20Traversal%20Cheat%20Sheet%20-%20Dark.pdf)

In DOM:

- Everything is **node**;
- Tags are **elements**;
- **Element** is a specical type of **node**;
  - ==HTMLCollection== is a live collection of **elements**, it is automatically updated when DOM changes;
  - ==NodeList== is a collection of **nodes**;
    <br>
- A ==token== is a string representing the token you want to check for the existence of in the list.
  <br>
- ==DOMTokenList==: represent a set of space-separated tokens in a form of JS array objects with instance methods.
  - `DOMTokenList.item(index)`: return the item in the list by its index
  - `DOMTokenList.contains(token)`: return `true` / `false`
  - `DOMTokenList.supports(token)`: return `true` / `false`
  - `DOMTokenList.forEach()`: callback function just like `array.forEach()`
  - `DOMTokenList.keys()`: returns an `iterator`
  - `DOMTokenList.values()`: returns an `iterator`
  - `DOMTokenList.add(token0, token1, /* … ,*/ tokenN)`: add specificed token(s)
  - `DOMTokenList.remove(token1, token2, /* … ,*/ tokenN)`: remove specificed token(s)
  - `DOMTokenList.replace(oldToken, newToken)`: replaces an existing token, or return `false` if oldToken doesn't exist.
  - `DOMTokenList.toggle(token[, force])`: removes or adds token, return `true` or `false` indicating whether `token` is in the list or not after the call.
    - if token existed already, removes it and return `false`;
    - if token doesn't existed, adds it and return `true`;
    - `force`: can be `true` or `false`, force toggle() to behave as its boolean return
  - `DOMTokenList.entries()`
    <br>

##### **[Back to table](#table)**

---

## Web APIs {#webapis}

- **API**: application programming interface
  <br>
- **className vs classList**:
  - `Element.className`: a string representing the class(s) of the element, seperated by space.
  - `Element.classList`: (read-only) returns a live `DOMTokenList` collection of the class attribute of the element.
    ```
    const div = document.createElement('div');
    div.className = 'col border text-center'; // A string.
    div.classList = ['col', 'border', 'text-center'] // A DOMTokenList, not an array
    ```
    - To turn `DOMTokenList` into an `array`, use `const elementArray = Array.from(DOMTokenList)`
      <br>
- **srollHeight vs clientHeight vs offsetHeight**:
  - `Element.scrollHeight`: (read-only) returns the minimum height the element would require in order to fit all the content in the viewport without using a vertical scrollbar, including content not visible on the screen due to overflow.
  - `Element.clientHeigth`: (read-only) returns the height of an element's content.
    - both including padding but excludes borders, margins, and horizontal scrollbars.
    - `scrollHeight` doesn't care about the text content if `Element` is a `textarea`, if no content inside `textarea`, it will just show the rendered `height`.
    - If the element's content can fit without a need for a vertical scrollbar, its `scrollHeight` equal to its `clientHeight`
  - `Element.offsetHeight`: (read-only) returns the viewable height of an element (in pixels), including padding, border and scrollbar, but not the margin.
    <br>
- **innerHTML vs innerText vs textContent**:

  - `Element.innerHTML`: The text content of the element, including all spacing and inner HTML tags.
  - `Element.innerText`: Just the text content of the element and all its children, without CSS hidden text spacing and tags, except `<script>` and `<style>` elements.
  - `Element.textContent`: The text content of the element and all descendaces, with spacing and CSS hidden text, but without tags.

  ```
  // HTML
  <div id="mylinks">
    This is my <b>link collection</b>:
    <ul>
      <li><a href="www.borland.com">Bye bye <b>Borland</b> </a></li>
      <li><a href="www.microfocus.com">Welcome to <b>Micro Focus</b></a></li>
    </ul>
  </div>
  ```

  ```
  // JS
  const div = document.getElementById('mylinks');

  console.log(div.textContent) // This is my link collection:

  console.log(div.innerText) // This is my link collection:Bye bye Borland Welcome to Micro Focus

  console.log(div.innerHTML)
  // This is my <b>link collection</b>:
  // <ul>
  //   <li><a href="www.borland.com">Bye bye <b>Borland</b></a></li>
  //   <li><a href="www.microfocus.com">Welcome to <b>Micro Focus</b></a></li>
  // </ul>
  ```

    <br>

- **querySelector**:

  - `Element.querySelector()`: returns the first Element within the document that matches the specified selector, or group of selectors. If no matches are found, null is returned.
    - Selectors:
      - Universal selector: `*`
      - Type selector: `tagname`
      - Class selector: `.classname`
      - ID seletor: `#id`
      - Attribute selector:
        - `[attr]`: has attribute
        - `[attr=value]`: equal to value
        - `[attr~=value]`: contain and space-separated
        - `[attr|=value]`: contain and as a whole or be followed by `-`
        - `[attr^=value]`: contain and starts with value, not necessarily have to be a whole word
        - `[attr$=value]`: contain and ends with value, not necessarily have to be a whole word
        - `[attr*=value]`: contain, no other limits.
    - Grouping selectors:
      - Selector list: `,`
    - Combinators:
      - Descendant combinator: space '` `'
      - Child combinator: `>`
      - General sibling combinator: `~`
      - Adjacent sibling combinator: `+`
      - Column combinator: `||`
    - Pseudo-classes and pseudo-elements: `:` / `::`

  <br>

##### **[Back to table](#table)**

---

## Web-related terms {#webterms}

- **URI** (Uniform Resource Identifier): a string that refers to a resource
- **URL** (Uniform Rsource Locator): a type of URI, specifies where a resource can be found on the Internet (Web address).
  <br>
- `Host`: a device connected to the Internet (or a local network).

  - clients and servers are just programs that run on a host
    <br>

- **Origin**: `[scheme]://[hostname]:[port]`

  - defined by the scheme (**protocol**), hostname (**domain**), and port of the URL
  - `http://example.com:8080`
    - `http`: called "scheme",
      - http: resources transported over unencrypted connections using HTTP protocol.
      - https: resource is transported using the HTTP protocol, but over a secure TLS (Transport Layer Security) channel.
    - `example.com`: called domain name, it is hosted on a server where the document resides
    - `8080`: called ports
    - `wwww.example.com` is actually a subdomain of example.com
  - "Same-origin" means the client has the same origin as the server it's calling
  - "Cross-origin" means the client origin is different than the server it's calling
  - CORS (Cross-Origin Resource Sharing) is a system, consisting of transmitting HTTP headers, that determines whether browsers block frontend JavaScript code from accessing responses for cross-origin requests.
    <br>

- **Client**: Any device that can send request to server, and receive respond from server;
- **Server**: Any device that can receive a request and respond to it. Server could refer to hardware, software, or both.

  - **Hardware**: a web server is a computer that stores web server software and a websites's component files. It connnects to the Internet and supports phy sical data interchange with other devvices connected to the web
  - **Software**: a web server includes several parts that control how web users access hosted files. At a minimum, this is an HTTP server.
    - An HTTP server is software that understands URLs (web addresses) and HTTP (the protocol your browser uses to view webpages).
    - An HTTP server can be accessed through the domain names of the websites it stores, and it delivers the content of these hosted websites to the end user's device.
      <br>
  - **A static web server** (stack): consists of hardware with an HTTP server(software). Static server sends its hosted files as-is to your browser
  - **A dynamic web server**: consists of a static web server plus extra software, most commonly an _**application server**_ and a **_database_**. The application server updates the hosted files before sending content to your browser via the HTTP server.
    <br>
  - **Routing**: determines which handler receives a specific request.

    - A handler is a function dedicated to receiving and acting on certain requests.
    - Requests are routed based on two pieces of information: the HTTP request method, and the request path.
    - A route refers to an HTTP method, path, and handler combination.
    - Routes are created and added to the server before it starts listening for requests.
      <br>

  - **REST**: representational state transfer, a software **architectural** style that describes a uniform interface between physically separate components, often across the Internet in a client-server architecture.
    - RESTful routes:
      <br>

- **Static Media**: refers to content that never or rarely change, like images, movies, audio, etc
  <br>
- **Domain Name System** (DNS): the protocol used to translate **human readable hostnames** into **IP addresses**.
  <br>
- **Streaming** involves breaking a resource that you want to receive over a network down into small chunks, then processing it bit by bit.
  <br>
- **CDN**: content delivery network
  <br>
- **SPA**:single page application
  <br>

##### **[Back to table](#table)**

---

## Interesting concepts {#interesting}

1. [Big O Cheatsheet](./Big%20O%20cheatsheet.png)
   <br>
1. A function to return one of two functions based on their execution results, which can only be decided during function invocation.

   ```
   function eitherCallback(callback1, callback2) {
     return (x)=>{
       return callback1(x) || callback2(x)
     }
   }
   ```

   <br>

1. There are two types of ==expressions== 1. those that assign value to a variable with side effects: `x = 1` 1. those that in some sense evaluate and therefore resolve to a value `1 + 2`
   <br>

1. **Check if a Character is a Letter**
   Compare the lowercase and uppercase variants of the character
   `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`
   <br>

1. **Deep copy an array with primitive elements**
   `arrayCopy = [...array]`
   <br>

1. **Capitalize a string**
   `string.charAt(0).toUpperCase() + string.slice(1)`
   <br>

1. **DP problem common characteristics:**

   - Ask for optimum value:
     - Ask for max/min/longest etc. of something;
     - Ask for the number of ways to do something;
   - The future decisions depend on earlier decisions
     - distinguish DP problem from greedy algorithm / divide and conquer problem
   - Tips:
     - DP[i] should have close connection to nums[i];
       <br>

1. **In `for` loop, the condition could be anything, it doesn't have to be related to `i`.**

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

   <br>

1. Find the checked radio `input` element: `document.querySelector('input:checked')`
   <br>

1. **Create an array with**
   <br>

1. **imperative** vs **declarative**:
   - imperative code focuses on writing an explicit sequence of commands to describe how you want the computer to do things
   - declarative code focuses on specifying the result of what you want

##### **[Back to table](#table)**

## Table of content
- [Table of content](#table-of-content)
  - [Python General](#python-general)
  - [Python build-in types](#python-build-in-types)
  - [Python build-in function](#python-build-in-function)
  - [Python library:](#python-library)
  - [python module (import XXX)](#python-module-import-xxx)
  - [memo](#memo)


### Python General
- comments start with `#`
  <br>
- The keyword for defining a function is `def` instead of `function`.
  .js

  ```
  function addTwo(x){
      var sum = x + 2;
      return sum;
  }
  console.log(addTwo(3)) // prints 5
  ```

  .py

  ```
  # The same function would be written as follows in python:
  def add_two(x):
      sum = x + 2
      return sum

  print(add_two(3)) # prints 5
  ```

   <br>

- In almost all cases where you would use a set of curly braces in javascript, in python, we will use a colon(`:`) followed by an **indented block** of code. How many spaces/indents does not matter, as long as everything in the **same block** has the same amount of indentation.
  <br>
- Python variables are usually written in **snake-case** rather than camel-case
  <br>
- The `return` keyword behaves nearly identically to javascript
  <br>
- can use `pass` as the body of a function to make it temporarily work and avoid error
  ```
  def unfinished_func():
      pass
  ```
  <br>
- **No keyword** is used for **variable initialization**. Variable scoping rules work similarly to variables declared with var in javascript (there are notable differences which are unlikely to appear in this unit. If you are absolutely dying to know, look into the python keyword `global`).
  <br>
- lines of code don't end with semicolons
  <br>
- for loop: `for` element `in` sequence `:`
  ```
  for i in range(10):
    print(i)
  ```
   <br>

- if statement
  ```
  if xxx:
    XXX
  elif yyy:
    YYY
  else zzz:
    ZZZ
  ```
- Collections of data:
  1. <span>List</span>: square brackets `[]`, ordered, changeable, allow duplicates
     ```
     list1 = ["abc", 34, True, 40, "male"]
     print(list1[0])  # "abc"
     ```
     <br>
  2. <span>Tuple</span>: round brackets `()`, ordered, unchangeable, allow duplicates
     ```
     thistuple = ("apple", "banana", "cherry")
     print(thistuple[0]) # "apple"
     ```
     <br>
  3. <span>Set</span>: curly brackets `{}`, unordered, unchangeable (but addable and removable), no duplicates
     ```
     thisset = {"apple", "banana", "cherry"}
     ```
     <br>
  4. <span>Dictionary</span>: curly brackets `{}`, and have keys and values, ordered, changeable, no duplicates
     ```
     thisdict = {
       "brand": "Ford",
       "model": "Mustang",
       "year": 1964
     }
     ```
     <br>

[back to top](#table-of-content)
<br>

  
### Python build-in types
- In python everything is an **object**, each entity (string, function, class, etc) has a value and associated properties and methods. 
  - In JS, primitives types have no methods, JS will automatically wrap them in respective prototype object wrappers when invoking methods for better performance, higher memory efficiency and simplicity.

- <span>Numeric Types</span>: `int`, `float`, `complex`
  - All numeric types (except complex) support the following operations:
    - `+`, `-`, `*`, `/`, `%`, `//`(floor division), `**`(to the power of), `@`(matrix multiplication[new]), `==`(check equality)
    - Bitwise operators:
      `x | y`, `x ^ y`(exclusive or), `x & y`, `x << n`, `x >> n`, `~x` 
    - Augmented assignment: 
        `+=`, `-=`, `*=`, `/=`, `%=`, `//=`, `**=`, `@=`, `|=`, `^=`, `&=`, `<<=`, `>>=`

        <br>

- <span>Text Sequence Type</span>: `str` 
  - **immutable** sequences of Unicode code points.
  - String expressions: 
    - `'s"t"r'`
    - `"s't'r"`, 
    -  `'''str'''`/`"""str"""`(can span multiple lines)
    - Raw strings(prefixing `r` or `R`): backslashes (`\`) are treated as **literal characters** and do not interpreted as escape characters.
      - `raw_string = r"C:\new_folder"`
    - Formated strings(f-string): allow for embeded expressions with curly braces `{}`:
      - `name = "Alice"`
      - `age = 30`
      - `f_string = f"My name is {name} and I am {age} years old."`
      - `fr` or `rf` string: both works
    - Byte strings(prefixing `b` or `B`): sequences of bytes instead of Unicode characters, used for working with binary data, such as files in binary mode.
      - `byte_string = b"This is a byte string."`
    - Unicode strings(prefixing `u` or `U`): (*only in py2, all strings are unicode in py3*)
      - unicode_string = u"This is a Unicode string."


  - `str` class methods:
    - `static str.maketrans({'a': '1'})`: create a translation table to replace characters in a string
    - `my_str.translate(translate_table)`: return the translated string
  
    ```
    translation_table = str.maketrans({'t': 'c', 'l': 'b'})
    translated_string = my_string.translate(translation_table)
    ```
    - `my_str.isXXX()`: return `True` if all characters in the `my_str` are XXX and there is at least one character, otherwise `False`
      - `isalpha`: alphabetic (letters)
      - `isascii`: within ASCII or empty string
      - `islower`: lowercase
      - `isupper`: uppercase
      - `isdecimal`: Decimal characters are those that can be used to form numbers in base 10, in the Unicode General Category “Nd”. 
      - `isdigit`: This covers digits which cannot be used to form numbers in base 10, is a character that has the property value Numeric_Type=Digit or Numeric_Type=Decimal.
      - `isnumeric`: numieric characters, including digit
      - `isalnum`: alphanumeric (letters + numieric)

      - `isspace`: only whitespace characters
      - `isidentifier`: identifier (keywords are identifier by default), `keyword.iskeyword('def') => true`
      - `isprintable`: printable or empty. Nonprintable characters are those characters defined in the Unicode character database as “Other” or “Separator”
      - `istitle`:  titlecased string (`Hello World` => `True`, `Hello world` => `False`)

    - `seperator_string.join(iterator)`: concatenate a sequence of strings together with a **separator** string
      ```
      words = ['Hello', 'world', '!']
      separator = ' '
      result = separator.join(words)

      print(result) # Output: 'Hello world !'
      ```
    - `str.strip([char_set])`: Return a copy of the string with the **leading** and **trailing** characters removed. The chars argument is a string specifying the set of characters to be removed.
      - `char_set` is a string specifying the set of characters to be removed. If omitted or `None`, defaults to whitespace
      ```
      '   spacious   '.strip() => 'spacious'
      'www.example.com'.strip('comwz.') => 'example'
      ``` 

  <br>

- <span>Binary Sequence Types</span>: `bytes`, `bytearray`, `memoryview`

<br>

- <span>Sequence Types</span>: `list`, `tuple`, `range`
  - `list`: (like js array)
    - list comprehension: a concise way to create lists
      - basic syntax: `[expression for item in iterable]`
      - filtering with if:  `[expression for item in iterable if condition]`
      - filtering with if-else:  `[expression1 if condition1 else expression2 for item in iterable]`
      - filtering with mutiple if-else:  `[expression1 if condition1 else expression2 if condition2 else expression3 if condition3 ... for item in iterable]`
<br>

- <span>Mapping Types</span>: `dict`

<br>

- <span>Set Types</span>: `set`, `fronzenset`

<br>

- <span>Boolean Types</span>: `bool`
  - Only two value: `True` and `False`
<br>

- <span>None Types</span>: `none` (like `null` in JS)

<br>

- <span>Iterator Types</span>: `iter`, `rang_iterator`

<br>

- <span>Generator Types</span>: `generator`

<br>  

[back to top](#table-of-content)
<br>




### Python build-in function
  - `print()`: log to cli
    
  - `input()`: display prompt message and waits for user input in cli, accept input with Enter key
   
  - `len(s)`: Return the length (the number of items) of an object. The argument may be a sequence (such as a string, bytes, tuple, list, or range) or a collection (such as a dictionary, set, or frozen set).

  - `all(iterable)`: return `True` if all elements of the `iterable` are true or `iterable` is empty. Otherwise `False`

  <br>

[back to top](#table-of-content)
<br>

### Python library:
- <span>Numpy</span>: for better data manipulation
  - Numpy array Broadcasting
    <br>

- <span>Matplotlib</span>: for draw histogram
    <br>

[back to top](#table-of-content)
<br>

---

### python module (import XXX)

  1. **string**
      - `string.ascii_letters` 
        - same as `string.ascii_lowercase` + `string.ascii_uppercase`
        - `string.ascii_lowercase`: `'abcdefghijklmnopqrstuvwxyz'`
        - `string.ascii_uppercase`: `'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`
      - `string.digits`: `'0123456789'`
      - `string.punctuation`: ``'!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~'``
     
  2. **random**
       - `random.random()`: 0.0 <= X < 1.0
       - `random.choice(seq)`: randomly choose one from `seq` (for crypographic uses, use `secrets.choice`)

  3. **secrets**
       - `secrets.choice(seq)`: randomly choose one from `seq` (more randomness)
  
  4. **re**
      - regular expression
      - `re.search(pattern, string, flags=0)`: Scan through string looking for the **first** location where the regular expression pattern produces a match, and return a corresponding `Match`
        - `flags`: RegexFlag object
      - `re.findall(pattern, string, flags=0)`: Return all non-overlapping matches of pattern in string, as a **list of strings** or **tuples**.
      - `re.compile(pattern, flags=0)`: compile a re into a re object, used for matching
        <br>

      - class re.Pattern: Pattern object returned by `re.compile()`
        - `pattern = re.compile("d")`
        - `Pattern.search(string[, pos=0[, endpos=len(excluded)]])`: 
          - same as `re.search(patternLiteral, string)`
          - return: `None` if no match, or Match object
      - class re.Match: Match object returned by successful `pattern.match()` and `pattern.search()`
        - `m = pattern.search("dog")`;
      - class re.RegexFlag: regex flag object ([docs](https://docs.python.org/3/library/re.html#re.RegexFlag))

  <br>

[back to top](#table-of-content)
<br>

### memo
  - generator expression (like list comprehension, but with parentheses)
  - call function with assigned arguments: `add(x=1, y=7)`, this can change the order of arguments: same as `add(y=7, x=1)`
  - `if __name__ == '__main__':`
  
[back to top](#table-of-content)
<br>
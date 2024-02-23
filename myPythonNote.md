# Python

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

  

### Python build-in types
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
  - Written in: `'s"t"r'`, `"s't'r"`, `'''str'''`/`"""str"""`(may span multiple lines)
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

- <span>None Types</span>: `none`

<br>

- <span>Iterator Types</span>: `iter`, `rang_iterator`

<br>

- <span>Generator Types</span>: `generator`

<br>




### Python build-in function
  - `print()`: log to cli
    
  - `input()`: display prompt message and waits for user input in cli, accept input with Enter key

### Python library:
- <span>Numpy</span>: for better data manipulation
  - Numpy array Broadcasting
    <br>

- <span>Matplotlib</span>: for draw histogram

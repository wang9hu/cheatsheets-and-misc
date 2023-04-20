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
- Collections of data:
  1. <span>List</span>: square brackets `[]`, ordered, changeable, allow duplicates
     ```
     list1 = ["abc", 34, True, 40, "male"]
     print(list1[0])  # "abc"
     ```
     <br>
  1. <span>Tuple</span>: round brackets `()`, ordered, unchangeable, allow duplicates
     ```
     thistuple = ("apple", "banana", "cherry")
     print(thistuple[0]) # "apple"
     ```
     <br>
  1. <span>Set</span>: curly brackets `{}`, unordered, unchangeable (but addable and removable), no duplicates
     ```
     thisset = {"apple", "banana", "cherry"}
     ```
     <br>
  1. <span>Dictionary</span>:  curly brackets `{}`, and have keys and values, ordered, changeable, no duplicates
     ```
     thisdict = {
       "brand": "Ford",
       "model": "Mustang",
       "year": 1964
     }
     ```
     <br>
- <span>Numpy</span>: 
   - Numpy array Broadcasting
<br>
- <span>Matplotlib</span>: 
1. **DP problem common characteristics:**

   - Ask for optimum value:
     - Ask for max/min/longest etc. of something;
     - Ask for the number of ways to do something;
   - The future decisions depend on earlier decisions
     - distinguish DP problem from greedy algorithm / divide and conquer problem
   - Tips:
     - DP[i] should have close connection to nums[i];
       <br>

1. **Check if a Character is a Letter**
   Compare the lowercase and uppercase variants of the character
   `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`
   <br>

1. **Capitalize a string**
   `string.charAt(0).toUpperCase() + string.slice(1)`
   <br>

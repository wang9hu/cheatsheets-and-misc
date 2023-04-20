# Leetcode Notes

- <span>DP problem common characteristics:</span>

  - Ask for optimum value:
    - Ask for max/min/longest etc. of something;
    - Ask for the number of ways to do something;
  - The future decisions depend on earlier decisions
    - distinguish DP problem from greedy algorithm / divide and conquer problem
  - Tips:
    - DP[i] should have close connection to nums[i];
      <br>

- <span>Check if a Character is a Letter</span>
  Compare the lowercase and uppercase variants of the character
  `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`
  <br>

- <span>Check if a variable is an integer</span>
  `~~a === a`: `true` if integer, `false` other
  <br>

- <span>Capitalize a string</span>
  `string.charAt(0).toUpperCase() + string.slice(1)`
  <br>

- <span>Get the middle index</span>
  - use: 
  `const mid = Math.floor(left + (right - left) / 2)` 
  instead of 
  `const mid = Math.floor((left + right) / 2)`
  to prevent number overflow
  <br>

- <span>2 sum, 3 sum questions</span>
  - unique nums: hash
  - duplicates: sort + two pointers (start, end)
  - unsortable: use hashset, for inner loop, set `nums[j]: i` pair and check for complement value (will be slower than sorted method);
    <br>
- <span>Backtrack recursive</span>

  - **Permutation**, similar to DFS (_depth first search_), traverse through all possible outcome
  - its time complexity will always be
  - Three questions:

    1. Decisions that have already been made (track)
    2. Choices list (choice)
    3. No choice condition (ends)

    ```
    // pseudo codes
    result = [];
    backtrack(track, choices) {
      if (ends):
        result add track
        return
      for (choice in choices) {
        make choice: track add choice
        backtrack(track, choices)
        cancel choice: track remove choice
      }
    }
    ```

  - Example: Generate Parentheses

    ```
    var generateParenthesis = function(n) {
      if (n === 0) return [];
      const res = [];

      // left, right means how many start/close parentheses left
      function backtrack(left, right, track, res) {
        if (right < left) return;
        if (left < 0 || right < 0) return;

        // end condition
        if (left === 0 && right === 0) {
            res.push(track);
            return;
        }

        // for choice '(':
        track += '('; // make choice
        backtrack(left - 1, right, track, res);
        track = track.slice(0, -1); // cancel choice

        // for choice '):
        track += ')'; // make choice
        backtrack(left, right - 1, track, res);
        track = track.slice(0, -1); // cancel choice
      }

      backtrack(n, n, '', res);
      return res;
    }
    ```
    <br>
- <span>Binary Search</span>
  - Binary Search should be considered every time you need to **search for an index or element** in a collection. If the collection is unordered, we can always **sort it first** before applying Binary Search.
  <br>
  - Composed of 3 main sections:
    1. Pre-processing: sort if collection is unsorted
    1. Binary Search: Using a loop or recursion to divide search space in half after each comparison. <span>Note</span>: _When defining the boundries, consider which boundary to be **excluded** for the **next iteration**
    1. Post-processing: Determine viable candidates in the remaining space.
    <br>
  - Templates:
    1. Most basic and elementary form: no depend on other elements or neighbors to determine if the condition is met
        ```
        while (left <= right) {
          const mid = left + Math.floor((right - left) / 2);
          if (nums[mid] === target) {
            return mid;
          } else if(nums[mid] < target) {
            left = mid + 1;
          } else {
            right = mid - 1;
          }
        }

        return -1;
        ```
      - search space: could be just **1** element, hence the `left <= right` 
      - **No post-porcessing** required becasue all elements are checked in the iteration
      <br>
    2. Use the element's <span>right neighbor</span> to determine if the condition is met and decide whether to go left or right
        ```
        while (left < right) { 
          const mid = left + Math.floor((right - left) / 2);
          if (nums[mid] === target) {
            return mid;
          } else if (nums[mid] < target) {
            left = mid + 1;
          } else {
            right = mid;
          }
        }
        // Post-processing:
        if (nums[left] === target) return left

        return -1;
        ```
      - search space: at least **2** in size at each step, hence the `left < right` 
      - Post-processing required, iteration ends when `left === right`, need to check `nums[left]` or `nums[right]` for condition
      <br>
    3. Use element's <span>neighbors</span> to determine if condition is met and decide whether to go left or right
       ```
       while (left + 1 < right) {
        const mid = left + Math.floor((right - left) / 2);
          if (nums[mid] === target) {
            return mid;
          } else if (nums[mid] < target) {
            left = mid;
          } else {
            right = mid;
          }
       }
       // Post-processing:
       if (nums[left] === target) return left;
       if (nums[right] === target) return right;

       return -1
       ```
       - search space: at least **3** in size at each step, hence the `left + 1 < right` 
       - Post-processing is required, iteration ends when `left + 1 === right`, need to check `nums[left]` and `nums[right]` for condition.
        
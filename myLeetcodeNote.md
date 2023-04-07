- **DP problem common characteristics:**

  - Ask for optimum value:
    - Ask for max/min/longest etc. of something;
    - Ask for the number of ways to do something;
  - The future decisions depend on earlier decisions
    - distinguish DP problem from greedy algorithm / divide and conquer problem
  - Tips:
    - DP[i] should have close connection to nums[i];
      <br>

- **Check if a Character is a Letter**
  Compare the lowercase and uppercase variants of the character
  `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`
  <br>

- **Capitalize a string**
  `string.charAt(0).toUpperCase() + string.slice(1)`
  <br>

- **2 sum, 3 sum questions**
  - unique nums: hash
  - duplicates: sort + two pointers (start, end)
  - unsortable: use hashset, for inner loop, set `nums[j]: i` pair and check for complement value (will be slower than sorted method);
    <br>
- **Backtrack recursive**

  - ==Permutation==, similar to DFS (_depth first search_), traverse through all possible outcome
  - its time complexity will always be
  - 3Q (three questions):

    1. Decisions that have already been made (track)
    1. Choices list (choice)
    1. No choice condition (ends)

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

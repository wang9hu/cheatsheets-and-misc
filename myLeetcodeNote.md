# Leetcode Notes

- [Leetcode Notes](#leetcode-notes)
  - [Tricks](#tricks)
    - [DP problem](#dp-problem)
    - [2 sum, 3 sum](#2-sum-3-sum)
    - [Backtrack recursive](#backtrack-recursive)
    - [Graph Data Structure](#graph-data-structure)
      - [Dijkstra algorithm](#dijkstra-algorithm)
      - [Union find (Disjoint Set/Bipartite Group)](#union-find-disjoint-setbipartite-group)
      - [Topological Sort (Kahn's algorithm)](#topological-sort-kahns-algorithm)
    - [Binary Search](#binary-search)
    - [Sliding Window](#sliding-window)
    - [Double Linked List](#double-linked-list)
    - [Pointers](#pointers)
    - [BTS](#bts)
    - [Heap](#heap)

## Tricks

- **Check if a Character is a Letter**
  Compare the lowercase and uppercase variants of the character
  `char.toLowerCase() !== char.toUpperCase() // true if char is not a letter`
  <br>

- **Check if a Variable is an Integer**
  `~~a === a`: `true` if integer, `false` other
  <br>

- **Capitalize a String**
  `string.charAt(0).toUpperCase() + string.slice(1)`
  <br>

- **Get the Middle Index**
  - use:
    `const mid = left + Math.floor((right - left) / 2)`
    instead of
    `const mid = Math.floor((left + right) / 2)`
    to prevent number overflow
    <br>
  - `x >> 1` is equivalent to `Math.floor(x / 2)`, so the above could be written as
    `const mid = left + (right - left) >> 1`
    <br>
- **When caching a string or an array in obj**:
  - if existed in `cache` then add `1`, or assign it to `0`:
    `cache[key] = (cache[key] || 0) + 1;`
  - if existed as array, push or assign `ele`, can't use `push` cause it returns the number of elements
    `cached[key] = (cached[key] || []).concat(ele)`
    <br>
- **Empty an array**
  - use `arr.length = 0` to empty an array;
    ```
    const arr = [1, 2, 3]
    arr.length = 0; 
    console.log(arr) // [];
    ```
    <br>
- **Create M * N array filled with 0**
  - `const grid = Array(M).fill(0).map((el) => Array(N).fill(0))`
  - `const grid = Array.from({ length: M }).map(() => Array(N).fill(0))`
  <br>

**[Back to top](#leetcode-notes)**

### DP problem

- Ask for optimum value:
  - Ask for max/min/longest etc. of something;
  - Ask for the number of ways to do something;
- The future decisions depend on earlier decisions
  - distinguish DP problem from greedy algorithm / divide and conquer problem
- Tips:
  - DP[i] should have close connection to nums[i];
  <br>
- Two ways: <span>tabulation & memoization</span>
  - **tabulation**: bottom-up way, solving related sub-problem first, filling up the n-dimensional table, then based on the table to compute the top problem
    - mostly used when all subproblems must be solved at least once, from bottom to top
    - iteratively
  - **memoization**: top-down way, from the original problem and split it into multiple sub-problem, and store subproblem solution dynamically.
    - recursive functions from top to down order
    <br>

**[Back to top](#leetcode-notes)**

### 2 sum, 3 sum

- unique nums: hash
- duplicates: sort + two pointers (start, end)
- unsortable: use hashset, for inner loop, set `nums[j]: i` pair and check for complement value (will be slower than sorted method);
  <br>

**[Back to top](#leetcode-notes)**

### Backtrack recursive

- **Permutation**, similar to **DFS** (_depth first search_), traverse through all possible outcome, differences is that **DFS** focus on every single point and **backtrack** focus on the path it goes by.
- its time complexity will always be
- Three questions:

  1. Decisions that have already been made (track)
  2. Choices list (choice)
  3. No choice condition (ends)
  <br>
- **Note**: choices doesn't have to be a single value, it could be a combination of different values, e.g. row and column index of a 2-D table

  ```
  // pseudo codes
  result = [];
  backtrack(track, choices) {
    if (no more choices):
      result add track
      return
    for (choice in choices) {
      make choice: track add choice
      backtrack(track, choices)
      cancel choice: track remove choice
    }
  }
  ```
- <span>Duplicate choices & Repeated choices</span>
  - Sort array when possible 
  - use a `start` parameter to indicate which element is current backtrack starts from
  - use `let i = start | 0` to iterate from `start` or `0`
  - If choices 
    - **No duplicates && No repeats**: use `start` with `i + 1`, end condition is run out of choices, no same track
    <br>
    - **Has duplicates && No repeats**: use `start` with `i + 1`, end condition is run out of choices, possible same track, use cache to check if existed already, 
      - for array, sorted, and use iteration of all choices and check `i > start && choices[i] === choices[i - 1] ? skip current iteration : finish current iteration` so that iteration afterwards don't need to count that element again.
      - like`JSON.stringify(track)` 
    <br>
    - **No duplicates && Can repeats**: use `start` with `i`, end condition is decided by problem matching condition, maybe something else like `sum === target`, no same track
    <br>
    - **Has duplicates && Can repeats** (Very Rarely): use `start` with `i`, end condition is decided by problem matching condition.  
    <br>

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

**[Back to top](#leetcode-notes)**

### Graph Data Structure
A **Graph** is a non-linear data structure consisting of <span>vertices</span> and <span>edges</span>. 

Graph is denoted by G(E, V):
  - graph: G 
  - vertices: V, aka, nodes, 
    - degree: number of edges connected to a node
    - indegree: (directed graph) number of edges pointing **to** a node
    - outdegree: (directed graph) number of edges pointing **from** a node
  - edges: E, lines that connect nodes
  <br>

**Types of graphs**:

  - <span>Directed Graphs</span>: edges have a direction
  - <span>Undirected Graphs</span> edges have **no** direction
  <br>
  - <span>Weighted Graphs</span>: edges have weights or costs associated with them (e.g. distance)
  - <span>Unweighted Graphs</span>: edges have **no** weights or costs associated with them 
  <br>
  - <span>Complete Graphs</span>: each vertex is connected to every other vertex
  <br>
  - <span>Bipartite Graphs:</span>: vertices can be divided into two disjoint sets such that every edge connects a vertex in one set to a vertex in the other set.
  <br>
  - <span>Trees</span>: A connected graph with **no** cycles
  - <span>Cyclic Graph</span>: A graph with **at least one** cycle, doesn't have to be directed.
  <br>

#### Dijkstra algorithm


#### Union find (Disjoint Set/Bipartite Group)
Used for storing non-overlapping **subsets** of elements. For each subset there is a unique **representative** that represent current subset. Disjoint sets have these operations:

- Add new set to disjoint sets
  - find the parent of a element x: `Parent[x]`
  - if x has no parent, use initialization: `Parent[x] = x`
- Find representative of a disjoint set: **find**
  ```
  function find(x) {
    if (Parent[x] !== x) return find(Parent[x]);
    return x; // reach representative
  }
  ```
- Merge disjoint sets to a single set: **union**
  ```
  // x, y are elements from different subset
  function union(x, y) {
    // now two subsets are merged into one and the representative is find(x)
    Parent[find(y)] = find(x) 
  }
  ```
- check if two sets are disjoint or not
  ```
  // x, y are elements from different subset
  return find(x) === find(y)
  ```
**Example**: find redundant connection in undirected graph:
```
function findRedundantConnection(edges: number[][]): number[] {
    const parent: { [key:number]: number } = {};
    const find = (x: number): number => {
        if (parent[x] !== x) return find(parent[x]);
        return x;
    }
    const union = (x: number, y: number) => {
        parent[find(y)] = find(x);
    }
    for (const [a, b] of edges) {
        if (parent[a] === undefined) parent[a] = a;
        if (parent[b] === undefined) parent[b] = b;
        if (find(a) !== find(b)) {
            union(a, b)
        } else {
            return [a, b];
        }
    }
};
```

#### Topological Sort (Kahn's algorithm)
The **topological sort** algorithm takes a <span>directed graph</span> and returns an <span>array</span> of the nodes where each node appears <span>before</span> all the nodes it points to.
- **Cyclic graphs** don't have valid topological orderings.

<span>Implementation</span>: (edges are direction pointing from one to another)
  1. Identify a node with no incoming edges.
  1. Add that node to the ordering.
  2. Remove it from the graph. (also remove the edges from it to other nodes)
  1. Repeat.
  <br>


**[Back to top](#leetcode-notes)**

### Binary Search

- Binary Search should be considered every time you need to **search for an index or element** in a collection. If the collection is unordered, we can always **sort it first** before applying Binary Search.
  <br>
- Composed of 3 main sections:
  1. Pre-processing: <span>sort</span> if collection is unsorted
  1. Binary Search: Using a loop or recursion to divide search space in half after each comparison. <span>Note</span>: \_When defining the boundries, consider which boundary to be **excluded** for the **next iteration**
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
       <br>

**[Back to top](#leetcode-notes)**

### Sliding Window

Mostly used when getting dealing with <span>array</span> or <span>string</span>, like getting info about **subarray** or **substring**, like **max/min sum**, **max diff**, or **non-repeat substring**.
<br>

1. use **left** or **right** represent a section of the total, usually both start from 0
1. move **right** to next index, and decide if **left** needs to move to a new index
1. get the info in between current **left** and **right**
1. repeat 2 and 3 until **right** reach the end. Usually, set **right** as the <span>next</span> iteration boundary (exclusive) by the end of current loop, so that if while condition unsatisfied, no next iteration.

<br>

**[Back to top](#leetcode-notes)**

### Double Linked List

- One advantage of double linked list is that the node can <span>remove itself without other reference</span>. In addition, it takes <span>constant time</span> to add and remove nodes from the head or tail.
  ```
  cur.next.prev = cur.prev;
  cur.prev.next = cur.next;
  ```
  <br>
- One paticular implementation is that there could have pseudo head and tail to mark the boundary, so that no need to check `null` node during the update
  <br>

**[Back to top](#leetcode-notes)**

### Pointers

- One trick when dealing with pointers is that use a pseudo `prevHead` before `head`, and use `cur` starting from `prevHead` so that when moving to `cur.next`, `cur` is ensured existing.
  ```
  const prevHead = new ListNode();
  prevHead = head;
  let cur = prevHead.next;
  while (cur) {
    // do something
    cur = cur.next;
  }
  return prevHead.next;
  ```
  <br>

- find loop in linked list
  1. use two pointers: *fast* vs *slow*
  1. fast pointer move *two steps* and slow pointer move *one step*
  1. when fast and slow meet, they must be inside of the loop
  1. from where they meet, counting the steps it takes to loop back to the same node 

**[Back to top](#leetcode-notes)**

### BTS

```
  A
 / \
B   C
```

- <span>Traversal</span>:
  - Inorder: B -> A -> C
    ```
    // recursively
    function recursiveInorder(root) {
      function 
      const leftResult = recursiveInorder(root.left);
      const rootResult = 
      return something
    }
    ```
  - Preorder: A -> B -> C
  - Postorder: B -> C -> A
- <span>Search</span>
  - Recursively Search:
    ```
    function recursiveTreeSearch(root, value) {
      if (!root || root.val = value) {
        return root;
      } else if (root.val < value) {
        return recursiveTreeSearch(root.right, value)
      } else {
        return recursiveTreeSearch(root.left, value)
      }
    }
    ```
  - Iteratively:
    ```
    function iterativeTreeSearch(root, value) {
      let cur = root;
      while (cur && cur.val !== value) {
        if (cur.val < value) {
          cur = cur.right
        } else {
          cur = cur.left
        }
      }
      return cur
    }
    ```

  <br>

**[Back to top](#leetcode-notes)**

### Heap
  - **Complete Binary Tree (CBT)**: Each level of a Complete Binary Tree contains the maximum number of nodes, except possibly the last layer, which must be filled from **left to right**.  
  <br>
  - A Complete Binary Tree of **n** nodes can only have **one possible shape**
    <br>
  - Heap property: for any given node C, if P is a parent node of C, then:
    - max heap: P.val >= C.val
    - min heap: P.val <= C.val
  <br>
  - All heaps must be <span>Complete Binary Trees</span>
    ```
    // max heap: | // min heap: |  // index tree:
         30      |       3      | Math.floor((i-1)/2)      
        /  \     |      / \     |       /  \     
       25  17    |     9   14   |      i   i+1   
      /  \       |    / \       |     / \       
    19   21      |  10   15     |  2i+1 2i+2     
    ```
  - Heap operations:
    - insert(num): add a new key to heap
    - delete(num): remove a key from heap
    - **heapify**:  creat a heap (max or min) from the given array
    - findMax/Min: return max/min element from heap
    - extractMax/Min: remove and return max/min element from heap
    - deleteMax/Min: remove max/min element from heap
    - size: return the size
    - isEmpty: check for empty
    - getList: get the heap as an array
    <br>
  - Binary heap represented using array index
    - for any node whose index position in an array is `i`
      - `const leftChildIndex = 2i + 1`
      - `const rightChildIndex = 2i + 1`
      - `const parentIndex = Math.floor((i - 1) / 2)`
    ```
    /** ----------function approach---------- */
    const heap = [];

    function (max|min)HeapUp(index) {
      if (index === 0) return;
      const parentIndex = Math.floor((index - 1) / 2);
      if (heap[index] (>|<) heap[parentIndex]) {
        [heap[index], heap[parentIndex]] = [heap[parentIndex], heap[index]];
        (max|min)HeapUp(parentIndex);
      }
    }

    function (max|min)HeapDown(index) {
      const leftChildIndex = 2 * index + 1;
      const rightChildIndex = 2 * index + 2;
      if (leftChildIndex > heap.length - 1) {
        return
      } else if (rightChildIndex > heap.length - 1) {
        if (heap[index] (<|>) heap[leftChildIndex]) {
          [heap[index], heap[leftChildIndex]] = [heap[leftChildIndex], heap[index]];
          return
        }
      } else {
        const (max|min)ChildIndex = heap[leftChildIndex] >|< heap[rightChildIndex] ? leftChildIndex : rightChildIndex;
        if (heap[index] <|> heap[maxChildIndex]) {
          [heap[index], heap[maxChildIndex]] = [heap[maxChildIndex], heap[index]];
          (max|min)HeapDown(maxChildIndex);
        }
      }
    }

    function insert(val) {
      heap.push(val);
      (max|min)HeapUp(heap.length - 1);
    }

    function extract(val) {
      const index = heap.findIndex(val);
      [heap[index], heap[heap.length - 1]] = [heap[heap.length - 1], heap[index]];
      heap.pop();
      (max|min)HeapDown(index);
    }

    /** ----------class approach---------- */
    class Heap {
      constructor() {
        this.data = [];
      }

      getParentIndex(i) {
        return Math.floor((i - 1) / 2);
      }

      getLeftChildIndex(i) {
        return 2 * i + 1;
      }

      getRightIndex(i) {
        return 2 * i + 2;
      }

      swap(i1, i2) {
        const temp = this.data[i1];
        this.data[i2] = this.data[i1];
        this.data[i1] = this.data[i2];
      }

      maxHeapifyUp(i) {
        if (i === 0) return;
        const parentIndex = this.getParentIndex(i);
        if (this.data[i] > this.data[parentIndex]) {
          this.swap(i, parentIndex);
          this.maxHeapifyUp(parentIndex);
        }
      }

      maxHeapifyDown(i) {
        if (i > this.data.length - 1) return;
        const leftChildIndex = this.getLeftChildIndex(i);
        const rightChildIndex = this.getRightChildIndex(i);

        const leftChildValue = this.data[leftChildIndex]
        const rightChildValue = this.data[rightChildIndex]

        let maxChildIndex;
        if (leftChildIndex < this.data.length && rightChildIndex < this.data.length) {
          maxChildIndex = leftChildValue > rightChildValue ? leftChildValue : rightChildValue;
        } else if (leftChildIndex < this.data.length) {
          maxChildIndex = leftChildIndex;     
        } else {
          // because complete binary tree, if no left child, then no right child
          return; 
        }
        if (heap[i] < heap[maxChildIndex]) {
          this.swap(i, maxChildIndex);
          this.maxHeapifyDown(maxChildIndex);
        }
      }

      insert(num) {
        this.data.push(num);
        this.maxHeapifyUp(this.data.length - 1);
      }

      extract(num) {
        let numIndex = this.data.findIndex(n => n === num);
        this.swap(numIndex, this.data.length - 1);
        const res = this.data.pop();
        maxHeapifyDown(numIndex);
        return res;
      }
    }
    ```

**[Back to top](#leetcode-notes)**
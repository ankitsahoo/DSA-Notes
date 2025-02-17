### **15 LeetCode Algorithmic Patterns**

------

### **1. Prefix Sum**

**Concept**: The prefix sum pattern is useful when you're repeatedly calculating the sum of subarrays or subsets of a given array. By precomputing the cumulative sum at each index, you can quickly calculate the sum of any subarray in constant time.

#### Example:

If you have an array `arr = [1, 2, 3, 4, 5]`, the prefix sum array will be:

```
prefix_sum = [1, 3, 6, 10, 15]
```

Now, the sum of elements from index `i` to `j` can be computed as:

```
sum(i, j) = prefix_sum[j] - prefix_sum[i-1]
```

#### Use Case:

- **Range sum queries**.
- **Subarray sum problems**.

------

### **2. Two Pointers**

**Concept**: The two pointers pattern uses two indices (or pointers) to traverse the data structure, often from opposite ends or at different speeds. This technique is especially useful for problems involving sorted arrays or linked lists.

#### Example:

In a sorted array, to find two elements that sum up to a target, you can initialize one pointer at the beginning and the other at the end, and move them towards each other.

```python
def two_sum(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return (arr[left], arr[right])
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return None
```

#### Use Case:

- **Finding pairs or triplets in sorted arrays**.
- **Rearranging or partitioning arrays**.

------

### **3. Sliding Window**

**Concept**: The sliding window pattern is used for problems where you need to examine a subarray or substring of a fixed or variable length. You maintain a window (subarray) that "slides" across the data structure.

#### Example:

Finding the maximum sum of a subarray of size `k` in an array:

```python
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])
    max_sum = window_sum
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i-k]  # Slide the window
        max_sum = max(max_sum, window_sum)
    return max_sum
```

#### Use Case:

- **Maximum sum subarray problems**.
- **Substring problems (like longest substring with at most k distinct characters)**.

------

### **4. Fast and Slow Pointers (Tortoise and Hare)**

**Concept**: This pattern uses two pointers, one moving faster than the other, to solve problems like cycle detection or finding the middle element of a linked list.

#### Example:

To find the middle element of a linked list:

```python
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

#### Use Case:

- **Cycle detection** in linked lists or arrays (Floyd’s cycle-finding algorithm).
- **Finding the middle element** in a linked list.

------

### **5. Linked List In-place Reversal**

**Concept**: This pattern involves reversing the elements of a linked list without using extra space, by modifying the pointers of the nodes.

#### Example:

Reversing a singly linked list:

```python
def reverse_linked_list(head):
    prev = None
    current = head
    while current:
        next_node = current.next
        current.next = prev
        prev = current
        current = next_node
    return prev
```

#### Use Case:

- **Reversing linked lists** (e.g., for palindrome checking).
- **Reversing sublists** in a linked list.

------

### **6. Monotonic Stack**

**Concept**: A monotonic stack keeps elements in a specific order (either increasing or decreasing) to efficiently solve problems related to nearest greater or smaller elements.

#### Example:

Finding the next greater element for each element in an array:

```python
def next_greater_elements(arr):
    stack = []
    result = [-1] * len(arr)
    for i in range(len(arr)):
        while stack and arr[stack[-1]] < arr[i]:
            result[stack.pop()] = arr[i]
        stack.append(i)
    return result
```

#### Use Case:

- **Finding next/previous greater/smaller elements**.
- **Stock span problem**.

------

### **7. Top 'K' Elements**

**Concept**: This pattern is used when you're tasked with finding the `K` largest or smallest elements in a collection. Heaps (min or max) are typically used to efficiently solve these problems.

#### Example:

Finding the top `K` largest elements in an array:

```python
import heapq

def top_k_elements(arr, k):
    return heapq.nlargest(k, arr)
```

#### Use Case:

- **Finding K largest or smallest elements**.
- **Median of a stream**.

------

### **8. Overlapping Intervals**

**Concept**: The overlapping intervals pattern is useful for problems where you need to merge or count overlapping intervals.

#### Example:

Merging intervals:

```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])  # Sort by start time
    merged = []
    for interval in intervals:
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            merged[-1][1] = max(merged[-1][1], interval[1])
    return merged
```

#### Use Case:

- **Interval scheduling problems**.
- **Finding the union or intersection of intervals**.

------

### **9. Modified Binary Search**

**Concept**: This pattern is used when binary search is applied in a modified way, for example, finding the first or last occurrence of an element, or finding the ceiling/floor of a number in a sorted array.

#### Example:

Finding the first occurrence of a target element:

```python
def find_first_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    result = -1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid
            right = mid - 1  # Continue searching on the left side
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return result
```

#### Use Case:

- **Finding first or last occurrence** in a sorted array.
- **Finding element’s floor or ceiling**.

------

### **10. Binary Tree Traversal**

**Concept**: This pattern refers to traversing a binary tree using different strategies like **preorder**, **inorder**, **postorder**, and **level-order traversal**.

#### Example:

Inorder Traversal:

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.val, end=" ")
        inorder(root.right)
```

#### Use Case:

- **Tree traversals**.
- **Binary search trees (BST) operations**.

------

### **11. Depth-First Search (DFS)**

**Concept**: DFS is a graph traversal algorithm where you explore as far as possible along each branch before backtracking. It's often implemented using recursion or a stack.

#### Example:

DFS on a graph:

```python
def dfs(graph, node, visited):
    if node not in visited:
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)
```

#### Use Case:

- **Graph traversal**.
- **Pathfinding**.

------

### **12. Breadth-First Search (BFS)**

**Concept**: BFS is another graph traversal algorithm where you explore all neighbors at the current level before moving on to the next level. It's usually implemented with a queue.

#### Example:

BFS on a graph:

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    visited.add(start)
    
    while queue:
        node = queue.popleft()
        print(node, end=" ")
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

#### Use Case:

- **Shortest path in unweighted graphs**.
- **Level order traversal in trees**.

------

### **13. Matrix Traversal**

**Concept**: This pattern is used when you're working with 2D matrices. It includes operations like iterating through rows and columns or performing specific operations based on matrix properties.

#### Example:

Matrix traversal to find the sum of elements:

```python
def sum_matrix(matrix):
    total = 0
    for row in matrix:
        total += sum(row)
    return total
```

#### Use Case:

- **Matrix-based problems** (e.g., search, pathfinding).

------

### **14. Backtracking**

**Concept**: Backtracking is an algorithmic technique for solving problems incrementally. It tries to build a solution piece by piece and abandons a path as soon as it is determined that the path cannot lead to a valid solution.

#### Example:

Solving a sudoku puzzle:

```python
def solve_sudoku(board):
    def is_valid(board, row, col, num):
        # Check if the number is valid for the current position
        pass
    def solve():
        for row in range(9):
            for col in range(9):
                if board[row][col] == 0:
                    for num in range(1, 10):
                        if is_valid(board, row, col, num):
                            board[row][col] = num
                            if solve():
                                return True
                            board[row][col] = 0
                    return False
        return True
    solve()
```

#### Use Case:

- **Sudoku solver**.
- **Combination, permutation problems**.

------

### **15. Dynamic Programming (DP) Pattern**

**Concept**: DP is used to solve problems by breaking them into simpler overlapping subproblems and storing the results of these subproblems to avoid redundant computations. It is used when the problem exhibits **optimal substructure** and **overlapping subproblems**.

#### Example:

Fibonacci sequence using DP:

```python
def fib(n):
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

#### Use Case:

- **Knapsack problem**.
- **Longest common subsequence**.

------


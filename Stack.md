# **Stack**

## **1. What is a Stack?**

A **stack** is a linear **LIFO (Last In, First Out)** data structure where the **last element added is the first to be removed**.

✅ **Real-Life Examples of Stacks:**

- **Undo/Redo operations** in text editors
- **Back/Forward navigation** in browsers
- **Call Stack in Recursion**

------

## **2. Stack Operations**

| **Operation**      | **Description**             | **Time Complexity** |
| ------------------ | --------------------------- | ------------------- |
| `push(x)`          | Add `x` to the stack        | **O(1)**            |
| `pop()`            | Remove the top element      | **O(1)**            |
| `peek()` / `top()` | Get the top element         | **O(1)**            |
| `isEmpty()`        | Check if the stack is empty | **O(1)**            |

------

## **3. Implementing Stack in Python**

### **(1) Using Python List (Built-in Stack)**

```python
stack = []  # Create an empty stack

stack.append(10)  # Push operation
stack.append(20)
stack.append(30)
print(stack)  # Output: [10, 20, 30]

stack.pop()  # Removes 30 (LIFO)
print(stack)  # Output: [10, 20]

print(stack[-1])  # Peek (Output: 20)
print(len(stack) == 0)  # Check if empty (Output: False)
```

✅ **Time Complexity: O(1) per operation**

------

### **(2) Using `collections.deque` (Faster)**

```python
from collections import deque

stack = deque()
stack.append(5)  # Push
stack.append(10)
stack.append(15)
print(stack.pop())  # Output: 15 (LIFO)
```

✅ **Deque (`collections.deque`) is faster for stack operations than lists.**

------

### **(3) Implementing Stack Using a Class**

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        return "Stack is empty"

    def peek(self):
        if not self.is_empty():
            return self.stack[-1]
        return "Stack is empty"

    def is_empty(self):
        return len(self.stack) == 0

# Example usage
s = Stack()
s.push(1)
s.push(2)
print(s.pop())  # Output: 2
print(s.peek())  # Output: 1
```

✅ **Encapsulates stack behavior in a class**

------

## **4. Common Stack Problems & Solutions**

### **(1) Valid Parentheses (LeetCode 20)**

👉 **Check if a string has balanced parentheses.**

```python
def is_valid(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}

    for char in s:
        if char in mapping:
            top = stack.pop() if stack else '#'  # Get top element or default
            if mapping[char] != top:
                return False
        else:
            stack.append(char)  # Push opening bracket

    return not stack  # Return True if stack is empty

print(is_valid("({[]})"))  # Output: True
print(is_valid("({[})"))  # Output: False
```

✅ **Time Complexity: O(n)**

------

### **(2) Next Greater Element (LeetCode 496)**

👉 **Find the next greater element for each element in an array.**

```python
def next_greater_element(nums):
    stack = []
    res = [-1] * len(nums)  # Default to -1

    for i in range(len(nums) - 1, -1, -1):
        while stack and stack[-1] <= nums[i]:
            stack.pop()  # Remove smaller elements

        res[i] = stack[-1] if stack else -1  # Get next greater
        stack.append(nums[i])  # Push current element

    return res

print(next_greater_element([4, 5, 2, 10, 8]))  # Output: [5, 10, 10, -1, -1]
```

✅ **Time Complexity: O(n) (Each element is pushed & popped once)**

------

### **(3) Implement Min Stack (LeetCode 155)**

👉 **Stack with `O(1)` min retrieval.**

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []  # Stores minimum values

    def push(self, val):
        self.stack.append(val)
        min_val = min(val, self.min_stack[-1] if self.min_stack else val)
        self.min_stack.append(min_val)  # Track min value

    def pop(self):
        self.stack.pop()
        self.min_stack.pop()

    def top(self):
        return self.stack[-1]

    def getMin(self):
        return self.min_stack[-1]

# Example usage
ms = MinStack()
ms.push(3)
ms.push(5)
ms.push(2)
print(ms.getMin())  # Output: 2
ms.pop()
print(ms.getMin())  # Output: 3
```

✅ **Time Complexity: O(1) per operation**

------

## **5. Stack in Recursion & DFS**

### **(1) Stack in Recursion (Call Stack)**

```python
def recursive_function(n):
    if n == 0:
        return
    print(n)
    recursive_function(n - 1)  # Recursive call

recursive_function(3)
```

🔹 **Python internally uses a stack for recursive calls.**

------

### **(2) Depth-First Search (DFS) Using Stack**

```python
def dfs(graph, start):
    stack = [start]
    visited = set()

    while stack:
        node = stack.pop()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            stack.extend(graph[node])  # Push adjacent nodes

graph = {1: [2, 3], 2: [4, 5], 3: [6], 4: [], 5: [], 6: []}
dfs(graph, 1)  # Output: 1 3 6 2 5 4 (DFS order)
```

✅ **Use Case:** **Graph traversal using DFS**

------

## **6. Summary of Stack Concepts**

| **Operation**                | **Time Complexity** |
| ---------------------------- | ------------------- |
| **Push (Insert)**            | **O(1)**            |
| **Pop (Remove)**             | **O(1)**            |
| **Peek (Top Element)**       | **O(1)**            |
| **Search (Find an Element)** | **O(n)**            |

✅ **Use Cases of Stacks:**

- **Undo/Redo operations**
- **Expression evaluation (Infix to Postfix)**
- **Backtracking problems (Maze, N-Queens)**
- **Graph Algorithms (DFS)**
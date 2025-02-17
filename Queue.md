# **Queue**

## **1. What is a Queue?**

A **queue** is a linear **FIFO (First In, First Out)** data structure where the **first element added is the first to be removed**.

✅ **Real-Life Examples of Queues:**

- **Waiting lines (e.g., Bank, Ticket Counter)**
- **Task scheduling (OS process queue, Printers)**
- **Breadth-First Search (BFS) in Graphs**

------

## **2. Queue Operations**

| **Operation**        | **Description**             | **Time Complexity** |
| -------------------- | --------------------------- | ------------------- |
| `enqueue(x)`         | Add `x` to the queue        | **O(1)**            |
| `dequeue()`          | Remove the front element    | **O(1)**            |
| `front()` / `peek()` | Get the front element       | **O(1)**            |
| `isEmpty()`          | Check if the queue is empty | **O(1)**            |

------

## **3. Implementing Queue in Python**

### **(1) Using `collections.deque` (Efficient)**

```python
from collections import deque

queue = deque()  # Create an empty queue

queue.append(10)  # Enqueue operation
queue.append(20)
queue.append(30)
print(queue)  # Output: deque([10, 20, 30])

queue.popleft()  # Dequeue (Removes 10)
print(queue)  # Output: deque([20, 30])

print(queue[0])  # Peek front element (Output: 20)
print(len(queue) == 0)  # Check if empty (Output: False)
```

✅ **Time Complexity:** **O(1)** for `append()` and `popleft()`

------

### **(2) Using `queue.Queue` (Thread-Safe)**

```python
from queue import Queue

q = Queue()

q.put(10)  # Enqueue
q.put(20)
q.put(30)

print(q.get())  # Dequeue (Output: 10)
print(q.queue)  # Output: [20, 30]
```

✅ **Use Case:** **Thread-safe operations in multithreading**

------

### **(3) Implementing Queue Using a Class**

```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):
        if not self.is_empty():
            return self.queue.pop(0)  # Removes first element
        return "Queue is empty"

    def front(self):
        return self.queue[0] if not self.is_empty() else "Queue is empty"

    def is_empty(self):
        return len(self.queue) == 0

# Example usage
q = Queue()
q.enqueue(1)
q.enqueue(2)
print(q.dequeue())  # Output: 1
print(q.front())  # Output: 2
```

✅ **Encapsulates queue behavior in a class**

------

## **4. Types of Queues**

### **(1) Circular Queue**

🔹 **The last element connects to the first to form a loop.**

```python
class CircularQueue:
    def __init__(self, size):
        self.queue = [None] * size
        self.size = size
        self.front = self.rear = -1

    def enqueue(self, value):
        if (self.rear + 1) % self.size == self.front:  # Full queue
            return "Queue is full"
        elif self.front == -1:  # Empty queue
            self.front = self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = value

    def dequeue(self):
        if self.front == -1:
            return "Queue is empty"
        temp = self.queue[self.front]
        if self.front == self.rear:  # Only one element
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.size
        return temp
```

✅ **Use Case:** **Fixed-size buffering (like CPU scheduling).**

------

### **(2) Priority Queue (LeetCode 703)**

🔹 **Elements are dequeued in priority order instead of FIFO.**

```python
import heapq

pq = []
heapq.heappush(pq, (1, "Task 1"))  # Lower priority value = Higher priority
heapq.heappush(pq, (3, "Task 3"))
heapq.heappush(pq, (2, "Task 2"))

print(heapq.heappop(pq))  # Output: (1, 'Task 1') (Highest priority)
```

✅ **Time Complexity: O(log n)** (Heap operations)
 ✅ **Use Case:** **Dijkstra’s Algorithm, Job Scheduling**

------

## **5. Common Queue Problems & Solutions**

### **(1) Implementing Stack Using Queue (LeetCode 225)**

👉 **Use a queue to mimic stack operations (LIFO).**

```python
from collections import deque

class StackUsingQueue:
    def __init__(self):
        self.queue = deque()

    def push(self, value):
        self.queue.append(value)
        for _ in range(len(self.queue) - 1):  # Reverse order
            self.queue.append(self.queue.popleft())

    def pop(self):
        return self.queue.popleft() if self.queue else "Stack is empty"

    def top(self):
        return self.queue[0] if self.queue else "Stack is empty"

# Example usage
s = StackUsingQueue()
s.push(1)
s.push(2)
print(s.pop())  # Output: 2
```

✅ **Time Complexity: O(n) for push, O(1) for pop**

------

### **(2) Implementing Queue Using Stack (LeetCode 232)**

👉 **Use two stacks to implement queue operations.**

```python
class QueueUsingStack:
    def __init__(self):
        self.s1 = []
        self.s2 = []

    def enqueue(self, value):
        self.s1.append(value)

    def dequeue(self):
        if not self.s2:
            while self.s1:
                self.s2.append(self.s1.pop())
        return self.s2.pop() if self.s2 else "Queue is empty"

# Example usage
q = QueueUsingStack()
q.enqueue(1)
q.enqueue(2)
print(q.dequeue())  # Output: 1
```

✅ **Time Complexity: O(1) average for enqueue/dequeue**

------

### **(3) Rotten Oranges (LeetCode 994)**

👉 **Find the minimum time for all oranges to rot using BFS.**

```python
from collections import deque

def orangesRotting(grid):
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                queue.append((r, c, 0))  # Store (row, col, time)
            elif grid[r][c] == 1:
                fresh += 1  # Count fresh oranges

    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
    time = 0

    while queue:
        r, c, time = queue.popleft()
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            if 0 <= nr < rows and 0 <= nc < cols and grid[nr][nc] == 1:
                grid[nr][nc] = 2
                queue.append((nr, nc, time + 1))
                fresh -= 1  # Reduce fresh count

    return time if fresh == 0 else -1

grid = [[2, 1, 1], [1, 1, 0], [0, 1, 1]]
print(orangesRotting(grid))  # Output: 4
```

✅ **Use Case:** **Shortest path problems in a grid (BFS).**

------

## **6. Summary of Queue Concepts**

| **Queue Type**                 | **Use Case**            |
| ------------------------------ | ----------------------- |
| **FIFO Queue**                 | BFS, task scheduling    |
| **Circular Queue**             | CPU scheduling          |
| **Priority Queue**             | Dijkstra’s Algorithm    |
| **Double-Ended Queue (Deque)** | Sliding window problems |

✅ **Why Use Queues?**

- **FIFO structure** (Processing in order)
- **Used in Graphs (BFS, Shortest Path)**
- **Task scheduling & real-world applications**


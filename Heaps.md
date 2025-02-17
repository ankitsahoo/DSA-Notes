# **Heaps**

## **1. What is a Heap?**

A **heap** is a **tree-based data structure** that satisfies the **heap property**:

1. **Min-Heap:** The **smallest** element is at the root.
2. **Max-Heap:** The **largest** element is at the root.

✅ **Use Cases of Heaps:**

- **Priority Queues** (Task Scheduling, Process Scheduling)
- **Dijkstra’s Algorithm (Shortest Path)**
- **Finding the Kth Largest/Smallest Element**

------

## **2. Types of Heaps**

| **Heap Type** | **Property**                                      |
| ------------- | ------------------------------------------------- |
| **Min-Heap**  | Parent node ≤ Children (smallest element at root) |
| **Max-Heap**  | Parent node ≥ Children (largest element at root)  |

------

## **3. Implementing Heaps in Python**

### **(1) Min-Heap Using `heapq` (Default)**

Python’s `heapq` module implements a **Min-Heap** (smallest element at the top).

```python
import heapq

min_heap = []
heapq.heappush(min_heap, 10)  # Insert 10
heapq.heappush(min_heap, 5)   # Insert 5
heapq.heappush(min_heap, 15)  # Insert 15
heapq.heappush(min_heap, 1)   # Insert 1

print(min_heap)  # Output: [1, 5, 15, 10] (Min-Heap Property)

print(heapq.heappop(min_heap))  # Output: 1 (Removes smallest element)
print(min_heap)  # Output: [5, 10, 15]
```

✅ **Time Complexity:** O(log n) for `push` and `pop`

------

### **(2) Max-Heap Using `heapq` (Negate Values)**

Python does not provide a built-in **Max-Heap**, but we can simulate one by **storing negative values**.

```python
import heapq

max_heap = []
heapq.heappush(max_heap, -10)  # Insert -10 (Acts as 10)
heapq.heappush(max_heap, -5)   # Insert -5 (Acts as 5)
heapq.heappush(max_heap, -15)  # Insert -15 (Acts as 15)
heapq.heappush(max_heap, -1)   # Insert -1 (Acts as 1)

print([-x for x in max_heap])  # Output: [15, 5, 10, 1] (Max-Heap Property)

print(-heapq.heappop(max_heap))  # Output: 15 (Largest element removed)
```

✅ **Trick:** Insert elements as **negative values** and negate them when retrieving.

------

### **(3) Heapify an Existing List**

👉 **Convert a list into a Min-Heap in O(n) time.**

```python
import heapq

arr = [3, 1, 4, 1, 5, 9, 2]
heapq.heapify(arr)  # Convert list into Min-Heap
print(arr)  # Output: [1, 1, 2, 3, 5, 9, 4]
```

✅ **Time Complexity:** O(n)

------

## **4. Common Heap Problems & Solutions**

### **(1) Find Kth Largest Element (LeetCode 215)**

👉 **Use a Min-Heap of size `k` to keep track of the largest `k` elements.**

```python
import heapq

def kth_largest(nums, k):
    min_heap = nums[:k]  # Take first k elements
    heapq.heapify(min_heap)  # Convert to Min-Heap
    
    for num in nums[k:]:
        if num > min_heap[0]:  # Compare with smallest in heap
            heapq.heappop(min_heap)
            heapq.heappush(min_heap, num)

    return min_heap[0]  # Kth largest element

print(kth_largest([3, 2, 3, 1, 2, 4, 5, 5, 6], 3))  # Output: 4
```

✅ **Time Complexity: O(n log k)**

------

### **(2) Merge K Sorted Lists (LeetCode 23)**

👉 **Use a Min-Heap to merge multiple sorted lists efficiently.**

```python
import heapq

def merge_k_sorted_lists(lists):
    heap = []
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst[0], i, 0))  # Store (value, list index, element index)
    
    result = []
    while heap:
        val, list_idx, elem_idx = heapq.heappop(heap)
        result.append(val)

        if elem_idx + 1 < len(lists[list_idx]):  # Push next element from the same list
            heapq.heappush(heap, (lists[list_idx][elem_idx + 1], list_idx, elem_idx + 1))
    
    return result

lists = [[1, 4, 5], [1, 3, 4], [2, 6]]
print(merge_k_sorted_lists(lists))  # Output: [1, 1, 2, 3, 4, 4, 5, 6]
```

✅ **Time Complexity: O(N log k) (where N = total elements, k = number of lists)**

------

### **(3) Find Median in a Stream (LeetCode 295)**

👉 **Use two heaps (Max-Heap for left half, Min-Heap for right half).**

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.left_max = []  # Max-Heap (store negatives)
        self.right_min = [] # Min-Heap

    def addNum(self, num):
        heapq.heappush(self.left_max, -num)  # Add to Max-Heap
        heapq.heappush(self.right_min, -heapq.heappop(self.left_max))  # Balance

        if len(self.left_max) < len(self.right_min):  # Balance sizes
            heapq.heappush(self.left_max, -heapq.heappop(self.right_min))

    def findMedian(self):
        if len(self.left_max) > len(self.right_min):
            return -self.left_max[0]
        return (-self.left_max[0] + self.right_min[0]) / 2

mf = MedianFinder()
mf.addNum(1)
mf.addNum(2)
print(mf.findMedian())  # Output: 1.5
mf.addNum(3)
print(mf.findMedian())  # Output: 2
```

✅ **Time Complexity: O(log n) for `addNum()`, O(1) for `findMedian()`**

------

## **5. Summary of Heap Concepts**

| **Operation**  | **Min-Heap Complexity** | **Max-Heap Complexity** |
| -------------- | ----------------------- | ----------------------- |
| Insert (Push)  | **O(log n)**            | **O(log n)**            |
| Remove (Pop)   | **O(log n)**            | **O(log n)**            |
| Get Min/Max    | **O(1)**                | **O(1)**                |
| Heapify a List | **O(n)**                | **O(n)**                |

✅ **Why Use Heaps?**

- **Efficient priority-based retrieval**
- **Used in Graph Algorithms (Dijkstra’s, Prim’s)**
- **Optimized for Kth largest/smallest element problems**


# **Array**

Arrays are one of the most important topics in competitive programming. Mastering arrays means solving problems efficiently using different techniques and patterns.

------

## **1. Basics of Arrays in Python**

Python does not have a built-in "array" like C++ or Java. Instead, we use **lists**.

```python
arr = [1, 2, 3, 4, 5]  # List as an array
print(arr[0])  # Accessing elements (Output: 1)
arr.append(6)  # Adding an element
arr.pop()  # Removing the last element
arr[1] = 10  # Modifying an element
print(arr)  # [1, 10, 3, 4, 5]
```

**Useful Functions:**

```python
arr = [1, 5, 3, 7, 2]
print(len(arr))  # Length of array
print(sum(arr))  # Sum of elements
print(min(arr))  # Minimum element
print(max(arr))  # Maximum element
```

------

## **2. Array Traversal Techniques**

### **1D Array Traversal**

```python
arr = [1, 2, 3, 4, 5]
for num in arr:
    print(num, end=" ")  # Output: 1 2 3 4 5
```

### **2D Array (Matrix) Traversal**

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

# Row-wise traversal
for row in matrix:
    for num in row:
        print(num, end=" ")  # Output: 1 2 3 4 5 6 7 8 9

# Using index
for i in range(len(matrix)):
    for j in range(len(matrix[0])):
        print(matrix[i][j], end=" ")
```

------

## **3. Common Patterns & Tricks in Array Problems**

### **(1) Sliding Window (Efficient for Subarray Problems)**

👉 **Used when we need to find a subarray with a certain condition.**

**Example: Find maximum sum of `k` consecutive elements in an array.**

```python
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])  # Initial window sum
    max_sum = window_sum
    
    for i in range(len(arr) - k):
        window_sum += arr[i + k] - arr[i]  # Slide the window
        max_sum = max(max_sum, window_sum)
    
    return max_sum

arr = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(arr, k))  # Output: 9 (5+1+3)
```

✅ **Sliding Window is useful in:**

- Maximum/minimum subarray sum
- Longest substring problems
- Finding a subarray that meets certain conditions

------

### **(2) Two Pointer Approach (Optimal for Sorting & Searching)**

👉 **Used when working with sorted arrays or finding pairs/triplets.**

**Example: Find if two numbers in sorted array sum to target**

```python
def two_sum(arr, target):
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            return [arr[left], arr[right]]
        elif current_sum < target:
            left += 1  # Increase sum
        else:
            right -= 1  # Decrease sum
            
    return []  # No pair found

arr = [1, 2, 3, 4, 6]
target = 6
print(two_sum(arr, target))  # Output: [2, 4]
```

✅ **Two Pointers are useful in:**

- Finding pairs/triplets with a given sum
- Merging sorted arrays
- Removing duplicates from sorted arrays

------

### **(3) Prefix Sum (For Range Sum Queries)**

👉 **Used when calculating sum over a range repeatedly.**

**Example: Find the sum of elements between index `l` and `r` in `O(1)`.**

```python
def prefix_sum(arr, queries):
    prefix = [0] * (len(arr) + 1)
    
    for i in range(len(arr)):
        prefix[i + 1] = prefix[i] + arr[i]
    
    results = []
    for l, r in queries:
        results.append(prefix[r + 1] - prefix[l])
    
    return results

arr = [1, 2, 3, 4, 5]
queries = [(1, 3), (0, 2)]
print(prefix_sum(arr, queries))  # Output: [9, 6]
```

✅ **Prefix Sum is useful in:**

- Range sum queries
- Finding equilibrium index
- Checking subarray conditions quickly

------

### **(4) Hashing / Frequency Count**

👉 **Used when checking duplicates or counting occurrences.**

**Example: Find first repeating element in an array**

```python
def first_repeating(arr):
    seen = set()
    
    for num in arr:
        if num in seen:
            return num
        seen.add(num)
    
    return -1  # No repeating element

arr = [2, 3, 4, 2, 5, 6, 3]
print(first_repeating(arr))  # Output: 2
```

✅ **Hashing is useful in:**

- Finding duplicates
- Checking if two arrays have common elements
- Frequency-based problems

------

### **(5) Kadane’s Algorithm (Maximum Subarray Sum)**

👉 **Used for problems like "Find the largest sum of contiguous subarray".**

```python
def max_subarray_sum(arr):
    max_sum = cur_sum = arr[0]
    
    for num in arr[1:]:
        cur_sum = max(num, cur_sum + num)
        max_sum = max(max_sum, cur_sum)
    
    return max_sum

arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
print(max_subarray_sum(arr))  # Output: 6 (subarray: [4, -1, 2, 1])
```

✅ **Kadane’s Algorithm is useful in:**

- Maximum sum subarray
- Finding subarray with maximum product

------

## **4. Sorting Tricks for Arrays**

Sorting is often used as a preprocessing step.

```python
arr = [3, 1, 4, 1, 5, 9, 2]
arr.sort()  # In-place sorting (O(n log n))
print(arr)  # [1, 1, 2, 3, 4, 5, 9]

sorted_arr = sorted(arr, reverse=True)  # Sorting in descending order
print(sorted_arr)  # [9, 5, 4, 3, 2, 1, 1]
```

✅ **Sorting helps in:**

- Binary search problems
- Finding median, mode, and duplicate elements efficiently

------

## **5. Advanced Patterns**

### **Binary Search in an Array (O(log n))**

Used in problems like:

- Finding the first/last occurrence of an element
- Searching in a sorted rotated array

```python
import bisect

arr = [1, 3, 5, 7, 9]
index = bisect.bisect_left(arr, 5)  # Returns index of first occurrence
print(index)  # Output: 2
```

------

## **Summary of Array Tricks**

| **Pattern**            | **Use Case**                    |
| ---------------------- | ------------------------------- |
| **Sliding Window**     | Subarray problems               |
| **Two Pointers**       | Sorted array problems           |
| **Prefix Sum**         | Range sum queries               |
| **Hashing**            | Finding duplicates              |
| **Kadane’s Algorithm** | Maximum subarray sum            |
| **Sorting**            | Searching, range-based problems |
| **Binary Search**      | Efficient searching             |
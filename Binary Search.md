# **Binary Search in Python **

## **1. What is Binary Search?**

Binary Search is an **O(log n)** algorithm used to find an element in a **sorted array** by repeatedly dividing the search space in half.

------

## **2. How Binary Search Works?**

1. **Sort the array** (if not already sorted).
2. Find the middle element (`mid`)
   - If `arr[mid] == target`, return `mid` (found).
   - If `arr[mid] < target`, search in the **right half**.
   - If `arr[mid] > target`, search in the **left half**.
3. Repeat until the left and right pointers overlap.

------

## **3. Binary Search Implementation in Python**

### **(1) Standard Binary Search (Iterative)**

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2  # Middle index
        
        if arr[mid] == target:
            return mid  # Target found
        elif arr[mid] < target:
            left = mid + 1  # Search in right half
        else:
            right = mid - 1  # Search in left half
    
    return -1  # Target not found

arr = [1, 3, 5, 7, 9, 11]
target = 7
print(binary_search(arr, target))  # Output: 3 (index of 7)
```

✅ **Time Complexity:** **O(log n)**
 ✅ **Space Complexity:** **O(1)** (no extra memory used)

------

### **(2) Recursive Binary Search**

```python
def binary_search_recursive(arr, left, right, target):
    if left > right:
        return -1  # Base case: not found
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search_recursive(arr, mid + 1, right, target)  # Right half
    else:
        return binary_search_recursive(arr, left, mid - 1, target)  # Left half

arr = [2, 4, 6, 8, 10]
target = 6
print(binary_search_recursive(arr, 0, len(arr) - 1, target))  # Output: 2
```

✅ **Time Complexity:** **O(log n)**
 ✅ **Space Complexity:** **O(log n)** (due to recursion stack)

------

## **4. Variants of Binary Search**

### **(1) Find First Occurrence of a Number**

👉 **Useful for problems with duplicate elements**

```python
def first_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid  # Store index
            right = mid - 1  # Continue searching left side
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

arr = [1, 2, 2, 2, 3, 4]
target = 2
print(first_occurrence(arr, target))  # Output: 1 (index of first 2)
```

✅ **Use Case:** **Searching first occurrence in a sorted array**

------

### **(2) Find Last Occurrence of a Number**

👉 **Similar to first occurrence but move `left` pointer**

```python
def last_occurrence(arr, target):
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            result = mid
            left = mid + 1  # Continue searching right side
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

arr = [1, 2, 2, 2, 3, 4]
target = 2
print(last_occurrence(arr, target))  # Output: 3 (index of last 2)
```

✅ **Use Case:** **Finding the last index of a repeated element**

------

### **(3) Find Smallest Element Greater than Target (Upper Bound)**

👉 **Find the smallest element that is greater than `target`**

```python
import bisect

def upper_bound(arr, target):
    index = bisect.bisect_right(arr, target)  # Find insertion point
    return arr[index] if index < len(arr) else -1

arr = [1, 3, 5, 7, 9]
target = 5
print(upper_bound(arr, target))  # Output: 7
```

✅ **Use Case:** **Finding the next greater element**

------

### **(4) Find Largest Element Smaller than Target (Lower Bound)**

👉 **Find the largest element that is smaller than `target`**

```python
import bisect

def lower_bound(arr, target):
    index = bisect.bisect_left(arr, target)  # Find insertion point
    return arr[index - 1] if index > 0 else -1

arr = [1, 3, 5, 7, 9]
target = 5
print(lower_bound(arr, target))  # Output: 3
```

✅ **Use Case:** **Finding the next smaller element**

------

## **5. Special Problems Using Binary Search**

### **(1) Search in a Rotated Sorted Array (LeetCode 33)**

👉 **Array is rotated, find the target in O(log n)**

```python
def search_rotated(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid  # Found
        
        if arr[left] <= arr[mid]:  # Left half is sorted
            if arr[left] <= target < arr[mid]:
                right = mid - 1
            else:
                left = mid + 1
        else:  # Right half is sorted
            if arr[mid] < target <= arr[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1

arr = [4, 5, 6, 7, 0, 1, 2]
target = 0
print(search_rotated(arr, target))  # Output: 4
```

✅ **Use Case:** **Efficient search in rotated sorted arrays**

------

### **(2) Find Square Root of a Number (Using Binary Search)**

👉 **Find `√x` without using `math.sqrt()`**

```python
def square_root(n):
    left, right = 0, n
    ans = -1
    
    while left <= right:
        mid = (left + right) // 2
        if mid * mid == n:
            return mid
        elif mid * mid < n:
            ans = mid  # Store potential answer
            left = mid + 1
        else:
            right = mid - 1
            
    return ans  # Return floor value

print(square_root(10))  # Output: 3 (since √10 ≈ 3.16)
```

✅ **Use Case:** **Finding integer square root efficiently**

------

## **6. Summary of Binary Search Concepts**

| **Concept**                         | **Use Case**                         |
| ----------------------------------- | ------------------------------------ |
| **Standard Binary Search**          | Finding an element in sorted array   |
| **First & Last Occurrence**         | Finding repeated elements            |
| **Upper & Lower Bound**             | Finding next greater/smaller element |
| **Rotated Sorted Array Search**     | Searching in rotated arrays          |
| **Square Root Using Binary Search** | Finding square root efficiently      |

------

## **7. Why Use Binary Search in Competitive Programming?**

 ✅ **O(log n) Time Complexity** (Very efficient for large inputs)
 ✅ **Used in a variety of problems** (searching, optimization, etc.)
 ✅ **Works with Sorted Arrays & Monotonic Functions**
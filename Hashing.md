# Hashing in Python 

## **What is Hashing?**

Hashing is a technique used to store and retrieve data in **O(1)** or **O(log n)** time complexity using hash tables or dictionaries. It is widely used for:

- **Fast lookups**
- **Duplicate detection**
- **Counting frequency**
- **Mapping data efficiently**

In Python, we primarily use **dictionaries (`dict`) and sets (`set`)** for hashing because they have an **average time complexity of O(1)** for insertions, deletions, and lookups.

------

## **1. Types of Hashing**

### **1️⃣ Direct Hashing (Using Python Dictionary)**

A **dictionary (hash table)** maps keys to values efficiently.

```python
hash_map = {}  # Empty dictionary
hash_map["apple"] = 5  # Assigning a value
hash_map["banana"] = 3

print(hash_map["apple"])  # Output: 5
print(hash_map.get("grape", "Not Found"))  # Output: Not Found
```

✅ **Use Case:** Storing key-value pairs like frequency count, mapping, etc.

------

### **2️⃣ Hash Set (Using Python Set)**

A **set** is useful for storing **unique elements** with O(1) average-time operations.

```python
hash_set = set()
hash_set.add(10)
hash_set.add(20)
hash_set.add(10)  # Duplicate will not be added

print(10 in hash_set)  # Output: True
print(15 in hash_set)  # Output: False
```

✅ **Use Case:** Finding duplicates, checking element existence.

------

## **2. Common Hashing Problems & Solutions**

### **(1) Frequency Count Using Hashing**

👉 **Find the frequency of each number in an array**

```python
def frequency_count(arr):
    freq = {}
    for num in arr:
        freq[num] = freq.get(num, 0) + 1  # Increment count
    return freq

arr = [1, 2, 2, 3, 3, 3, 4]
print(frequency_count(arr))  # Output: {1: 1, 2: 2, 3: 3, 4: 1}
```

✅ **Use Case:** Counting occurrences of elements efficiently.

------

### **(2) Find First Repeating Element**

👉 **Return the first element that appears more than once in an array**

```python
def first_repeating(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return num  # First repeated element
        seen.add(num)
    return -1  # No repeating element found

arr = [4, 5, 6, 3, 5, 6]
print(first_repeating(arr))  # Output: 5
```

✅ **Use Case:** Identifying the first duplicate efficiently.

------

### **(3) Find Intersection of Two Arrays**

👉 **Find common elements in two arrays**

```python
def array_intersection(arr1, arr2):
    set1 = set(arr1)
    set2 = set(arr2)
    return list(set1 & set2)  # Set intersection

arr1 = [1, 2, 3, 4]
arr2 = [3, 4, 5, 6]
print(array_intersection(arr1, arr2))  # Output: [3, 4]
```

✅ **Use Case:** Finding common elements in two lists in O(n).

------

### **(4) Two Sum Problem (LeetCode 1)**

👉 **Find two numbers that add up to a target**

```python
def two_sum(arr, target):
    hash_map = {}  # Store number and index
    for i, num in enumerate(arr):
        diff = target - num
        if diff in hash_map:
            return [hash_map[diff], i]
        hash_map[num] = i  # Store the number with its index
    return []

arr = [2, 7, 11, 15]
target = 9
print(two_sum(arr, target))  # Output: [0, 1]
```

✅ **Use Case:** Fast lookup for pairs in O(n) time.

------

### **(5) Check If Array Has Duplicates**

👉 **Find if there is any duplicate element in the list**

```python
def has_duplicate(arr):
    return len(arr) != len(set(arr))

arr = [1, 2, 3, 4, 5, 3]
print(has_duplicate(arr))  # Output: True
```

✅ **Use Case:** Detecting duplicates in O(n).

------

### **(6) Longest Consecutive Sequence (LeetCode 128)**

👉 **Find the length of the longest sequence of consecutive numbers**

```python
def longest_consecutive(arr):
    num_set = set(arr)
    longest = 0

    for num in num_set:
        if num - 1 not in num_set:  # Start of a sequence
            length = 1
            while num + length in num_set:
                length += 1
            longest = max(longest, length)

    return longest

arr = [100, 4, 200, 1, 3, 2]
print(longest_consecutive(arr))  # Output: 4 (sequence: [1, 2, 3, 4])
```

✅ **Use Case:** Finding longest sequences in O(n).

------

## **3. Hashing Tricks**

### **(1) Using `collections.Counter` for Quick Frequency Count**

```python
from collections import Counter

arr = [1, 2, 2, 3, 3, 3]
freq = Counter(arr)
print(freq)  # Output: Counter({3: 3, 2: 2, 1: 1})
```

✅ **Faster alternative to a manual frequency dictionary**

------

### **(2) Hashing with Default Dictionary (Avoid KeyErrors)**

```python
from collections import defaultdict

freq = defaultdict(int)  # Default value = 0
arr = [1, 2, 2, 3]
for num in arr:
    freq[num] += 1

print(freq)  # Output: {1: 1, 2: 2, 3: 1}
```

✅ **Automatically initializes missing keys**

------

### **(3) Using `setdefault()` for Default Values in Hashmap**

```python
hash_map = {}
hash_map.setdefault("apple", 0)
hash_map["apple"] += 1
print(hash_map)  # Output: {'apple': 1}
```

✅ **Avoids KeyError when accessing missing keys**

------

## **4. Summary of Hashing Concepts**

| **Concept**                      | **Use Case**                    |
| -------------------------------- | ------------------------------- |
| **Dictionary (`dict`)**          | Key-value storage               |
| **Set (`set`)**                  | Fast membership checking        |
| **Frequency Count**              | Counting occurrences            |
| **First Repeating Element**      | Detecting duplicates early      |
| **Two Sum (LeetCode 1)**         | Finding pairs efficiently       |
| **Set Intersection**             | Finding common elements         |
| **Longest Consecutive Sequence** | Detecting sequences efficiently |

------

## **5. Why Use Hashing in Competitive Programming?**

✅ **O(1) Average Time Complexity** (for insertion, deletion, lookup)
 ✅ **Easy to Implement & Readable**
 ✅ **Works Well with Other Data Structures**

------


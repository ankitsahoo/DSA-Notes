# **Linked List**

A **Linked List** is a data structure where elements (nodes) are stored **non-contiguously** in memory, and each node points to the next. Unlike arrays, linked lists offer **efficient insertions and deletions** but have slower access times.

------

## **1. Types of Linked Lists**

### **1️⃣ Singly Linked List (SLL)**

- Each node has **two** parts: `data` & `next` (pointer to the next node).
- Can only traverse **forward**.

### **2️⃣ Doubly Linked List (DLL)**

- Each node has **three** parts: `data`, `prev`, and `next`.
- Can traverse **forward and backward**.

### **3️⃣ Circular Linked List (CLL)**

- Last node points back to the **first node**, forming a circle.

------

## **2. Node Structure in Python**

A **node** is a fundamental unit of a linked list.

```python
class ListNode:
    def __init__(self, value):
        self.value = value  # Store the data
        self.next = None  # Pointer to next node
```

✅ **Each node stores a value and a pointer to the next node.**

------

## **3. Implementing a Singly Linked List**

### **(1) Creating a Linked List**

```python
class ListNode:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None  # Head points to first node

    def append(self, value):
        """Insert a node at the end"""
        new_node = ListNode(value)
        if not self.head:
            self.head = new_node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = new_node  # Link new node

    def display(self):
        """Print the linked list"""
        temp = self.head
        while temp:
            print(temp.value, end=" -> ")
            temp = temp.next
        print("None")

# Example Usage
ll = LinkedList()
ll.append(1)
ll.append(2)
ll.append(3)
ll.display()  # Output: 1 -> 2 -> 3 -> None
```

✅ **Time Complexity:**

- **Insertion at End:** **O(n)**
- **Traversal:** **O(n)**

------

### **(2) Insert at the Beginning**

```python
def insert_at_beginning(self, value):
    new_node = ListNode(value)
    new_node.next = self.head
    self.head = new_node
```

✅ **Time Complexity: O(1)** (Directly updates `head` pointer)

------

### **(3) Delete a Node by Value**

```python
def delete(self, value):
    if not self.head:
        return

    if self.head.value == value:
        self.head = self.head.next  # Remove head
        return

    temp = self.head
    while temp.next and temp.next.value != value:
        temp = temp.next

    if temp.next:
        temp.next = temp.next.next  # Remove node

# Usage
ll.delete(2)
ll.display()  # Output: 1 -> 3 -> None
```

✅ **Time Complexity: O(n)** (Needs traversal)

------

### **(4) Search for an Element**

```python
def search(self, target):
    temp = self.head
    while temp:
        if temp.value == target:
            return True
        temp = temp.next
    return False
```

✅ **Time Complexity: O(n)**

------

### **(5) Reverse a Linked List (Iterative)**

👉 **Reverses the order of nodes (LeetCode 206).**

```python
def reverse(self):
    prev = None
    current = self.head
    while current:
        next_node = current.next
        current.next = prev  # Reverse pointer
        prev = current
        current = next_node
    self.head = prev

# Usage
ll.reverse()
ll.display()  # Output: 3 -> 2 -> 1 -> None
```

✅ **Time Complexity: O(n)**
 ✅ **Space Complexity: O(1)**

------

### **(6) Detect a Cycle in a Linked List (Floyd’s Cycle Detection)**

👉 **Checks if a cycle (loop) exists in a linked list.**

```python
def has_cycle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True  # Cycle detected

    return False
```

✅ **Time Complexity: O(n)**
 ✅ **Space Complexity: O(1)**
 ✅ **Use Case:** **Checking infinite loops in linked lists.**

------

### **(7) Find the Middle of a Linked List (Two Pointers)**

👉 **Finds the middle node in a single pass (LeetCode 876).**

```python
def find_middle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next  # Moves twice as fast

    return slow  # Middle node
```

✅ **Time Complexity: O(n)**
 ✅ **Space Complexity: O(1)**
 ✅ **Use Case:** **Finding the midpoint efficiently.**

------

### **(8) Merge Two Sorted Linked Lists (LeetCode 21)**

👉 **Merges two sorted linked lists into one sorted list.**

```python
def merge_sorted(l1, l2):
    dummy = ListNode(0)
    current = dummy

    while l1 and l2:
        if l1.value < l2.value:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next

    current.next = l1 or l2  # Append remaining nodes
    return dummy.next
```

✅ **Time Complexity: O(n + m)** (Merging takes linear time)
 ✅ **Use Case:** **Sorting and merging linked lists.**

------

### **(9) Remove N-th Node from End (LeetCode 19)**

👉 **Deletes the N-th last node in one pass using two pointers.**

```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0)
    dummy.next = head
    first = second = dummy

    for _ in range(n + 1):  # Move first pointer n+1 steps
        first = first.next

    while first:
        first = first.next
        second = second.next

    second.next = second.next.next  # Remove node
    return dummy.next
```

✅ **Time Complexity: O(n)**
 ✅ **Use Case:** **Efficient deletion from end.**

------

## **4. Doubly Linked List (DLL)**

**In a DLL, each node has `prev` and `next` pointers.**

```python
class DoublyListNode:
    def __init__(self, value):
        self.value = value
        self.prev = None
        self.next = None
```

✅ **DLL allows backward traversal.**
 ✅ **More flexible than singly linked lists.**

------

## **5. Summary of Linked List Concepts**

| **Operation**             | **Time Complexity** | **Use Case**            |
| ------------------------- | ------------------- | ----------------------- |
| **Insert at Beginning**   | O(1)                | Stack-like behavior     |
| **Insert at End**         | O(n)                | Appending elements      |
| **Delete by Value**       | O(n)                | Removing specific nodes |
| **Search for an Element** | O(n)                | Checking existence      |
| **Reverse Linked List**   | O(n)                | Inverting order         |
| **Find Middle Node**      | O(n)                | Midpoint detection      |
| **Detect Cycle**          | O(n)                | Floyd’s cycle detection |
| **Merge Two Lists**       | O(n + m)            | Sorting & merging       |

------

## **6. Why Use Linked Lists in Competitive Programming?**

 ✅ **Efficient Insertions & Deletions** (Unlike arrays)
 ✅ **Dynamic Size Allocation** (Avoids resizing issues)
 ✅ **Useful for Stacks, Queues, Hashing (Chaining in HashTables)**


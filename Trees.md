# **Trees**

## **1. What is a Tree?**

A **Tree** is a hierarchical data structure where each **node** has a **parent** and **children**.

✅ **Key Terms:**

- **Root** – The topmost node.
- **Parent & Child** – Nodes connected directly.
- **Leaf Node** – A node with **no children**.
- **Height** – The **longest path** from root to leaf.
- **Depth** – Distance of a node from the root.

✅ **Types of Trees:**

1. **Binary Tree (BT)** – Each node has at most **two children**.
2. **Binary Search Tree (BST)** – A **sorted** binary tree where **left child ≤ parent ≤ right child**.

------

# **2. Binary Tree (BT)**

A **Binary Tree** is a tree where each node has at most **two children**.

## **(1) Node Structure for a Binary Tree**

```python
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
```

## **(2) Creating a Binary Tree**

```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
root.left.right = TreeNode(5)
```

✅ **Tree Structure:**

```
      1
     / \
    2   3
   / \
  4   5
```

------

## **(3) Binary Tree Traversal**

### **(a) Inorder Traversal (Left → Root → Right)**

```python
def inorder(root):
    if root:
        inorder(root.left)
        print(root.value, end=" ")
        inorder(root.right)

inorder(root)  # Output: 4 2 5 1 3
```

✅ **Used in:** **Retrieving sorted elements in BST**

### **(b) Preorder Traversal (Root → Left → Right)**

```python
def preorder(root):
    if root:
        print(root.value, end=" ")
        preorder(root.left)
        preorder(root.right)

preorder(root)  # Output: 1 2 4 5 3
```

✅ **Used in:** **Tree serialization**

### **(c) Postorder Traversal (Left → Right → Root)**

```python
def postorder(root):
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.value, end=" ")

postorder(root)  # Output: 4 5 2 3 1
```

✅ **Used in:** **Deleting a tree from memory**

### **(d) Level Order Traversal (BFS)**

```python
from collections import deque

def level_order(root):
    if not root:
        return
    queue = deque([root])
    while queue:
        node = queue.popleft()
        print(node.value, end=" ")
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

level_order(root)  # Output: 1 2 3 4 5
```

✅ **Used in:** **Shortest path problems (Graph BFS)**

------

## **(4) Height of a Binary Tree**

```python
def height(root):
    if not root:
        return 0
    return 1 + max(height(root.left), height(root.right))

print(height(root))  # Output: 3
```

✅ **Used in:** **Tree balancing & depth calculations**

------

# **3. Binary Search Tree (BST)**

A **Binary Search Tree (BST)** is a binary tree where:

- Left subtree **≤ root**
- Right subtree **≥ root**

✅ **BST Example:**

```
      10
     /  \
    5   15
   / \    \
  3   7   18
```

------

## **(1) Insert into a BST**

```python
def insert(root, value):
    if not root:
        return TreeNode(value)
    if value < root.value:
        root.left = insert(root.left, value)
    else:
        root.right = insert(root.right, value)
    return root

bst_root = None
values = [10, 5, 15, 3, 7, 18]
for v in values:
    bst_root = insert(bst_root, v)
```

✅ **Time Complexity:** O(log n) (Balanced BST), O(n) (Unbalanced)

------

## **(2) Search in a BST**

```python
def search(root, value):
    if not root or root.value == value:
        return root
    if value < root.value:
        return search(root.left, value)
    return search(root.right, value)

print(search(bst_root, 7))  # Output: TreeNode(7)
print(search(bst_root, 20))  # Output: None
```

✅ **Time Complexity:** O(log n) (Balanced BST)

------

## **(3) Delete a Node in BST (LeetCode 450)**

```python
def delete(root, key):
    if not root:
        return root
    if key < root.value:
        root.left = delete(root.left, key)
    elif key > root.value:
        root.right = delete(root.right, key)
    else:
        if not root.left:
            return root.right
        elif not root.right:
            return root.left
        temp = find_min(root.right)
        root.value = temp.value
        root.right = delete(root.right, temp.value)
    return root

def find_min(root):
    while root.left:
        root = root.left
    return root

bst_root = delete(bst_root, 7)
```

✅ **Time Complexity:** O(log n)

------

## **(4) Check if a Tree is a Valid BST (LeetCode 98)**

```python
def is_valid_bst(root, min_val=float('-inf'), max_val=float('inf')):
    if not root:
        return True
    if not (min_val < root.value < max_val):
        return False
    return is_valid_bst(root.left, min_val, root.value) and is_valid_bst(root.right, root.value, max_val)

print(is_valid_bst(bst_root))  # Output: True
```

✅ **Use Case:** **Tree validation for search operations**

------

# **4. Summary of Trees (BT & BST)**

| **Operation**         | **Binary Tree**      | **Binary Search Tree (BST)** |
| --------------------- | -------------------- | ---------------------------- |
| **Insertion**         | O(n)                 | O(log n)                     |
| **Search**            | O(n)                 | O(log n)                     |
| **Deletion**          | O(n)                 | O(log n)                     |
| **Inorder Traversal** | No Order             | Sorted Order                 |
| **Use Case**          | General Tree Storage | Efficient Searching          |

------

# **5. Applications of Trees**

✅ **Binary Tree Applications:**

- **Hierarchical data storage (File System, HTML/XML)**
- **Expression trees (Arithmetic expressions parsing)**
- **Heaps (Priority Queues)**

✅ **Binary Search Tree (BST) Applications:**

- **Efficient searching (O(log n) operations)**
- **Self-balancing BSTs (AVL, Red-Black Trees)**
- **Databases (Indexing)**


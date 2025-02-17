# **Tries (Prefix Trees)**

## **1. What is a Trie?**

A **Trie**, also known as a **Prefix Tree**, is a tree-like data structure that stores a dynamic set of strings, where each node represents a character in the string. It is primarily used for tasks involving **prefix matching**, **autocomplete**, **spell checking**, and **dictionary operations**.

### **Key Features of Tries:**

- **Each edge represents a character** in a string.
- **Nodes store a part of the string**, and the path from the root to a node represents a prefix of some string.
- **Efficient prefix searches**: Tries allow fast searching, inserting, and deleting of strings based on their prefixes.
- **Common Prefix Sharing**: Common prefixes among words are stored only once, making Tries space-efficient for certain use cases.

------

## **2. Trie Data Structure Overview**

### **(1) Basic Trie Node Structure**

Each node in a Trie contains:

- **Children**: A dictionary of child nodes (or an array if there are a fixed number of characters, e.g., lowercase English letters).
- **IsEndOfWord**: A boolean flag to indicate if the current node represents the end of a word.

#### Trie Node Class (Python)

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end_of_word = False
```

### **(2) Trie Data Structure**

The Trie class typically includes operations like **insert**, **search**, and **delete**.

#### Trie Class (Python)

```python
class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    # Insert a word into the Trie
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True
    
    # Search for a word in the Trie
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end_of_word
    
    # Search for a prefix in the Trie
    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

------

## **3. Trie Operations**

### **(1) Insert Operation**

- The insert operation involves adding each character of the string to the Trie, creating new nodes as necessary.
- Once the last character of the string is added, we mark that node as the end of the word.

#### Example:

Inserting the word `"apple"`:

```
            root
           /    \
          a      p
         /        \
        p          p
       /            \
      l              l
     /                \
    e                  (end of word)
```

### **(2) Search Operation**

- To search for a word, we follow the characters of the word from the root.
- If at any point, the character does not exist, the word is not present.
- After traversing all the characters of the word, if we reach the end node (i.e., `is_end_of_word = True`), the word is found.

#### Example:

Searching for the word `"apple"` will traverse through `root -> a -> p -> p -> l -> e` and return **True** if `is_end_of_word` is marked as **True**.

### **(3) StartsWith Operation**

- This operation checks if there is any word in the Trie that starts with a given prefix.
- We perform the same steps as in the search, but instead of checking for `is_end_of_word`, we just check if the prefix exists.

#### Example:

Searching for the prefix `"app"` will return **True** if any word in the Trie starts with `"app"`, such as `"apple"`.

------

## **4. Time Complexity of Trie Operations**

- **Insert**: O(m) where `m` is the length of the word being inserted.
- **Search**: O(m) where `m` is the length of the word being searched.
- **StartsWith**: O(m) where `m` is the length of the prefix.
- **Space Complexity**: O(m * n) where `n` is the number of words, and `m` is the average length of each word in the Trie.

------

## **5. Applications of Tries**

### **(1) Autocomplete/Auto-suggestions**

Tries are commonly used in autocomplete systems. Given a partially typed word, Tries can efficiently provide suggestions by looking for all words that share the same prefix.

#### Example:

If the user types `"app"`, the system might suggest:

- `"apple"`
- `"application"`
- `"apply"`

### **(2) Spell Checking**

Tries can be used in spell-checking applications to check if a word exists in the dictionary. Searching for a word is efficient and quick in a Trie.

### **(3) Prefix Matching**

Trie-based algorithms are highly efficient when you need to find all words that start with a given prefix.

### **(4) Dictionary Operations**

Tries are well-suited for operations like:

- Checking if a word exists.
- Finding all words with a given prefix.
- Finding the longest common prefix.

### **(5) IP Routing and Data Compression**

Tries are used in **IP routing** where nodes represent possible IP addresses and their prefixes. They are also used in **data compression algorithms** for storing common prefixes efficiently.

------

## **6. Trie vs Hash Map**

| **Aspect**           | **Trie**                              | **Hash Map**                          |
| -------------------- | ------------------------------------- | ------------------------------------- |
| **Space Efficiency** | Efficient for storing common prefixes | Stores full strings, uses more memory |
| **Time Complexity**  | O(m) for operations (m = word length) | O(1) for average cases                |
| **Use Case**         | Prefix matching, autocomplete         | General key-value lookups             |
| **Structure**        | Tree-like structure                   | Array/Hash table                      |

------

## **7. Summary of Tries**

- **Trie** is an efficient tree-based data structure used to store strings and perform prefix-based operations.
- Operations like **search**, **insert**, and **prefix match** are fast, with time complexity proportional to the length of the word or prefix.
- Tries are useful in applications like **autocomplete**, **spell checking**, and **dictionary lookups**.
- They efficiently share common prefixes, making them space-efficient for datasets with many words having common prefixes.

In summary, Tries are essential for efficiently solving problems that involve prefix matching and autocomplete, and they can significantly improve performance for such tasks compared to other data structures like arrays or hash maps.
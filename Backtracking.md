# Backtracking

## **1. What is Backtracking?**

Backtracking is a **brute-force algorithm** used for solving problems where we explore all possible solutions and backtrack when a solution fails.

🔹 **Key Concept:**

1. **Choose** – Pick a possible option.
2. **Explore** – Move forward with the choice.
3. **Backtrack** – Undo the choice if it leads to failure.

✅ **Used in problems involving:**

- **Subsets & Permutations**
- **N-Queens Problem**
- **Sudoku Solver**
- **Graph Problems (Hamiltonian Cycle, Maze Solver)**

------

## **2. How Backtracking Works?**

👉 **Recursive approach where we explore choices and undo them if they don't work.**

**Example:** **Printing all subsets of `{1, 2, 3}`**

```python
def subsets(nums, index=0, path=[]):
    if index == len(nums):  
        print(path)  # Print the subset
        return

    subsets(nums, index + 1, path + [nums[index]])  # Include nums[index]
    subsets(nums, index + 1, path)  # Exclude nums[index]

subsets([1, 2, 3])
```

**🔹 Output:**

```
[1, 2, 3]  
[1, 2]  
[1, 3]  
[1]  
[2, 3]  
[2]  
[3]  
[]  
```

✅ **Time Complexity: O(2ⁿ) (Each element has 2 choices: include or exclude)**

------

## **3. Backtracking vs Recursion**

| **Recursion**                          | **Backtracking**                                   |
| -------------------------------------- | -------------------------------------------------- |
| Calls itself with smaller subproblems  | Calls itself but **removes last choice** if needed |
| Solves problems using divide & conquer | Used to explore all possibilities                  |
| Used in **Fibonacci, Factorial**       | Used in **Sudoku, N-Queens, Subsets**              |

------

## **4. Common Backtracking Problems**

### **(1) Generate All Permutations of an Array (LeetCode 46)**

👉 **Find all possible orderings of `[1, 2, 3]`**

```python
def permute(nums, path=[], used=[]):
    if len(path) == len(nums):  
        print(path)  # Found a permutation
        return

    for num in nums:
        if num not in used:
            used.append(num)
            permute(nums, path + [num], used)
            used.pop()  # Backtrack

permute([1, 2, 3])
```

✅ **Time Complexity: O(n!)** (All orderings are explored)

------

### **(2) N-Queens Problem (LeetCode 51)**

👉 **Place `N` queens on an `N × N` chessboard so that no two attack each other.**

```python
def solve_n_queens(n):
    def is_safe(board, row, col):
        for i in range(row):
            if board[i] == col or abs(board[i] - col) == row - i:
                return False
        return True

    def backtrack(row, board):
        if row == n:
            result.append(board[:])
            return

        for col in range(n):
            if is_safe(board, row, col):
                board[row] = col
                backtrack(row + 1, board)
                board[row] = -1  # Backtrack

    result = []
    backtrack(0, [-1] * n)
    return result

print(solve_n_queens(4))
```

✅ **Time Complexity: O(N!)**
 ✅ **Use Case:** Solving constraint problems like **chessboard puzzles**

------

### **(3) Sudoku Solver (LeetCode 37)**

👉 **Fill a 9×9 board with digits 1-9 while following Sudoku rules.**

```python
def solve_sudoku(board):
    def is_valid(board, row, col, num):
        box_x, box_y = row // 3 * 3, col // 3 * 3
        return all(num != board[row][j] for j in range(9)) and \
               all(num != board[i][col] for i in range(9)) and \
               all(num != board[i][j] for i in range(box_x, box_x + 3) for j in range(box_y, box_y + 3))

    def backtrack():
        for i in range(9):
            for j in range(9):
                if board[i][j] == ".":
                    for num in map(str, range(1, 10)):
                        if is_valid(board, i, j, num):
                            board[i][j] = num
                            if backtrack():
                                return True
                            board[i][j] = "."  # Backtrack
                    return False
        return True

    backtrack()
```

✅ **Time Complexity: O(9⁸)** (Worst case: fill 81 cells)

------

### **(4) Word Search (LeetCode 79)**

👉 **Find if a word exists in a 2D grid moving up, down, left, or right.**

```python
def exist(board, word):
    def dfs(i, j, index):
        if index == len(word): return True
        if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]) or board[i][j] != word[index]:
            return False

        temp, board[i][j] = board[i][j], "#"  # Mark as visited
        found = dfs(i + 1, j, index + 1) or dfs(i - 1, j, index + 1) or \
                dfs(i, j + 1, index + 1) or dfs(i, j - 1, index + 1)
        board[i][j] = temp  # Backtrack
        return found

    return any(dfs(i, j, 0) for i in range(len(board)) for j in range(len(board[0])))

board = [['A', 'B', 'C', 'E'],
         ['S', 'F', 'C', 'S'],
         ['A', 'D', 'E', 'E']]
word = "ABCCED"
print(exist(board, word))  # Output: True
```

✅ **Time Complexity: O(4ⁿ) (Each cell has 4 choices)**
 ✅ **Use Case:** **Path-finding problems in a matrix/grid.**

------

## **5. Optimizations for Backtracking**

🔹 **Pruning:** Stop exploring unnecessary branches early
 🔹 **Memoization:** Store previously computed results
 🔹 **Bitmasking:** Represent state efficiently using bits

------

## **6. Summary of Backtracking**

| **Problem Type**        | **Example**                    |
| ----------------------- | ------------------------------ |
| **Subsets**             | Generate all subsets of a set  |
| **Permutations**        | Arrange elements in all orders |
| **Constraint Problems** | N-Queens, Sudoku               |
| **Graph Problems**      | Hamiltonian Path, Word Search  |
| **Grid Problems**       | Maze Solver                    |

✅ **Why Use Backtracking?**

- **Efficient pruning of invalid paths**
- **Used when brute force is too slow**
- **Solves constraint-based problems elegantly**

------

## **7. When NOT to Use Backtracking?**

🔴 **When an iterative solution is possible** (Sorting, Binary Search)
 🔴 **When recursion depth is too large** (Stack Overflow risk)
 🔴 **When an optimization technique (like DP) is faster**
# **Recursion**

## **1. What is Recursion?**

**Recursion** is a technique where a function **calls itself** to solve a smaller subproblem.
 It is mainly used when the problem can be divided into **smaller, similar subproblems**.

✅ **Two Main Parts of Recursion:**

1. **Base Case:** Stops the recursion (prevents infinite loop).
2. **Recursive Case:** Function calls itself with a smaller input.

------

## **2. Basic Example of Recursion**

### **Printing Numbers from `n` to `1` Using Recursion**

```python
def print_numbers(n):
    if n == 0:  # Base case
        return
    print(n)  # Print current number
    print_numbers(n - 1)  # Recursive call

print_numbers(5)
```

**🔹 Output:**

```
5  
4  
3  
2  
1  
```

✅ **Recursion reduces complex loops into simple functions.**

------

## **3. Factorial Using Recursion**

**Factorial Formula:** `n! = n * (n - 1)!`

```python
def factorial(n):
    if n == 0 or n == 1:  # Base case
        return 1
    return n * factorial(n - 1)  # Recursive case

print(factorial(5))  # Output: 120
```

✅ **Time Complexity:** O(n)
 ✅ **Space Complexity:** O(n) (due to recursion stack)

------

## **4. Fibonacci Series Using Recursion**

**Fibonacci Formula:** `F(n) = F(n-1) + F(n-2)`

```python
def fibonacci(n):
    if n <= 1:  # Base cases
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)  # Recursive call

print(fibonacci(6))  # Output: 8
```

✅ **Issue:** Exponential time complexity **O(2ⁿ)**
 ✅ **Solution:** Use **Memoization (Dynamic Programming).**

------

## **5. Recursion with Backtracking (Subset Generation)**

👉 **Example: Print all subsets of a given set `{1, 2, 3}`**

```python
def subsets(nums, index=0, path=[]):
    if index == len(nums):
        print(path)
        return

    subsets(nums, index + 1, path + [nums[index]])  # Include element
    subsets(nums, index + 1, path)  # Exclude element

subsets([1, 2, 3])
```

✅ **Used in:**

- Subsets (`Power Set`)
- Combinations & Permutations
- Solving puzzles like **Sudoku, N-Queens**

------

## **6. Tail Recursion vs. Non-Tail Recursion**

- **Tail Recursion:** Recursive call is the **last statement** (can be optimized).
- **Non-Tail Recursion:** Recursive call **is not last**, leading to extra stack space.

**Example: Tail Recursion for Factorial**

```python
def factorial_tail(n, result=1):
    if n == 0:
        return result
    return factorial_tail(n - 1, result * n)

print(factorial_tail(5))  # Output: 120
```

✅ **Advantage:** Uses **constant space O(1)** if optimized by Python.

------

## **7. Common Recursion Problems & Solutions**

| **Problem**    | **Recursive Formula**        |
| -------------- | ---------------------------- |
| Factorial      | `f(n) = n * f(n-1)`          |
| Fibonacci      | `f(n) = f(n-1) + f(n-2)`     |
| Power          | `xⁿ = x * xⁿ⁻¹`              |
| Reverse String | `rev(s) = rev(s[1:]) + s[0]` |
| Tower of Hanoi | `T(n) = 2T(n-1) + 1`         |

------

## **8. When to Use Recursion?**

✅ **Useful for:**

- **Divide and Conquer** (Merge Sort, Quick Sort)
- **Backtracking** (N-Queens, Sudoku Solver)
- **Tree Traversals** (Binary Trees)
- **Graph Problems** (DFS)

✅ **When NOT to Use:**

- If recursion depth is too high (**risk of stack overflow**).
- When an **iterative solution** is more memory efficient.

------

## **9. Summary**

| **Concept**        | **Explanation**                   |
| ------------------ | --------------------------------- |
| **Base Case**      | Stops recursion                   |
| **Recursive Case** | Calls itself with smaller input   |
| **Tail Recursion** | Last call is recursive            |
| **Backtracking**   | Exploring multiple solutions      |
| **Memorization**   | Optimizes overlapping subproblems |
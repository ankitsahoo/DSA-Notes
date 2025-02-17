# **Dynamic Programming (DP)**

## **1. What is Dynamic Programming?**

**Dynamic Programming (DP)** is an optimization technique used to solve problems by breaking them down into simpler subproblems and storing the results of these subproblems to avoid redundant computations. It is particularly useful for problems where the solution involves solving the same subproblems multiple times.

### **Key Concepts:**

- **Overlapping Subproblems**: The problem can be broken into subproblems that are solved multiple times.
- **Optimal Substructure**: The optimal solution to the problem can be constructed from optimal solutions of its subproblems.
- **Memoization**: Storing the result of subproblems to avoid redundant calculations.
- **Tabulation**: Building the solution iteratively from the smallest subproblems to larger ones.

### **Types of Dynamic Programming:**

1. **Top-down Approach** (Memoization): Start with the main problem and recursively solve smaller subproblems, storing results for reuse.
2. **Bottom-up Approach** (Tabulation): Solve all subproblems starting from the simplest (base cases) and iteratively build the solution.

------

## **2. Steps in Solving DP Problems**

1. **Identify the problem as a DP problem**: Check for overlapping subproblems and optimal substructure.
2. **Define the state**: Decide on the parameters that will define the subproblem.
3. **Recurrence relation**: Write down the relation that expresses the solution to the problem in terms of its subproblems.
4. **Base case**: Define the base case(s) for the simplest scenario.
5. **Compute the solution**: Using memoization or tabulation, compute the solution based on the recurrence relation.

------

## **3. Example: Fibonacci Sequence**

The Fibonacci sequence is a classic example of a problem that can be solved using DP.

The **Fibonacci Sequence** is defined as:

- F(0) = 0
- F(1) = 1
- F(n) = F(n-1) + F(n-2) for n ≥ 2

Without DP, a naive recursive solution would have exponential time complexity. With DP, we can optimize it.

### **(1) Top-down Approach (Memoization)**

In this approach, we start solving the problem recursively and store the results for reuse.

#### Code:

```python
def fib_top_down(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_top_down(n-1, memo) + fib_top_down(n-2, memo)
    return memo[n]

# Example usage
print(fib_top_down(10))  # Output: 55
```

### **(2) Bottom-up Approach (Tabulation)**

In this approach, we solve the problem iteratively starting from the base cases.

#### Code:

```python
def fib_bottom_up(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]

# Example usage
print(fib_bottom_up(10))  # Output: 55
```

### **Time Complexity**: O(n)

### **Space Complexity**:

- **Memoization**: O(n) due to the dictionary storing the results.
- **Tabulation**: O(n) due to the DP array.

------

## **4. Key Patterns in Dynamic Programming**

### **(1) 0/1 Knapsack Problem**

Given a set of items, each with a weight and value, determine the maximum value that can be achieved with a weight capacity limit.

- **State**: `dp[i][w]` represents the maximum value attainable using the first `i` items with a weight limit of `w`.
- **Recurrence**: dp[i][w]=max⁡(dp[i−1][w],dp[i−1][w−weight[i]]+value[i])dp[i][w] = \max(dp[i-1][w], dp[i-1][w-\text{weight}[i]] + \text{value}[i])

### **(2) Longest Common Subsequence (LCS)**

Given two sequences, find the length of the longest subsequence common to both.

- **State**: `dp[i][j]` represents the length of the LCS of the first `i` characters of string A and the first `j` characters of string B.
- **Recurrence**: dp[i][j]={dp[i−1][j−1]+1if A[i]=B[j]max⁡(dp[i−1][j],dp[i][j−1])if A[i]≠B[j]dp[i][j] =  \begin{cases} dp[i-1][j-1] + 1 & \text{if } A[i] = B[j] \\ \max(dp[i-1][j], dp[i][j-1]) & \text{if } A[i] \neq B[j] \end{cases}

### **(3) Coin Change Problem**

Given a set of coins and a target amount, find the minimum number of coins required to make the amount.

- **State**: `dp[x]` represents the minimum number of coins needed to make amount `x`.
- **Recurrence**: dp[x]=min⁡(dp[x−coin]+1)dp[x] = \min(dp[x - \text{coin}] + 1)

### **(4) Matrix Chain Multiplication**

Given a sequence of matrices, determine the most efficient way to multiply them together (minimizing the number of scalar multiplications).

- **State**: `dp[i][j]` represents the minimum number of scalar multiplications required to multiply matrices from index `i` to `j`.
- **Recurrence**: dp[i][j]=min⁡(dp[i][k]+dp[k+1][j]+dimensions[i]∗dimensions[k+1]∗dimensions[j])dp[i][j] = \min(dp[i][k] + dp[k+1][j] + \text{dimensions}[i] * \text{dimensions}[k+1] * \text{dimensions}[j])

------

## **5. When to Use Dynamic Programming?**

DP is useful in situations where:

- The problem can be broken down into smaller overlapping subproblems.
- You can store the result of these subproblems to avoid recomputing them.
- The problem exhibits optimal substructure, meaning the optimal solution to the problem can be derived from optimal solutions of its subproblems.

------

## **6. Common DP Problems and Solutions**

### **(1) Longest Increasing Subsequence (LIS)**

Given an array of integers, find the length of the longest increasing subsequence.

- **State**: `dp[i]` represents the length of the longest increasing subsequence that ends at index `i`.
- **Recurrence**: dp[i]=max⁡(dp[j]+1)for j<i and arr[j]<arr[i]dp[i] = \max(dp[j] + 1) \quad \text{for } j < i \text{ and } arr[j] < arr[i]

### **(2) Edit Distance (Levenshtein Distance)**

Given two strings, find the minimum number of operations (insertions, deletions, and substitutions) required to convert one string into another.

- **State**: `dp[i][j]` represents the minimum number of operations to convert the first `i` characters of string A to the first `j` characters of string B.
- **Recurrence**: dp[i][j]=min⁡(dp[i−1][j−1]+cost,dp[i−1][j]+1,dp[i][j−1]+1)dp[i][j] = \min(dp[i-1][j-1] + \text{cost}, dp[i-1][j] + 1, dp[i][j-1] + 1) where cost = 0 if `A[i] == B[j]`, otherwise 1.

------

## **7. Summary of Dynamic Programming**

| **Operation**               | **Time Complexity** | **Space Complexity** |
| --------------------------- | ------------------- | -------------------- |
| **Fibonacci (Memoization)** | O(n)                | O(n)                 |
| **Knapsack Problem**        | O(nW)               | O(nW)                |
| **LCS**                     | O(mn)               | O(mn)                |
| **Coin Change**             | O(n * amount)       | O(amount)            |

------

## **8. Applications of Dynamic Programming**

✅ **Real-world Applications:**

- **Bioinformatics**: Sequence alignment (LCS).
- **Operations Research**: Resource allocation problems (Knapsack).
- **Game Theory**: Optimal strategy games (Minimax with DP).
- **Text Processing**: Spell-checking, string matching (Edit Distance).
- **Economics**: Portfolio optimization, investment problems.

------

In summary, Dynamic Programming is a powerful technique for solving problems that can be broken down into smaller overlapping subproblems. By storing and reusing the results of these subproblems, DP helps in optimizing time complexity and making the solution efficient.
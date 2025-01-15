# Lab 08: Dynamic Programming Basics

## Overview
Dynamic Programming (DP) is a problem-solving paradigm used to solve optimization and decision-making problems by breaking them down into overlapping subproblems. It stores the solutions to subproblems to avoid redundant computations.

This lab introduces the basics of dynamic programming, including concepts, principles, and implementation of common DP problems.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the concept of overlapping subproblems and optimal substructure.
2. Learn to implement dynamic programming using **memoization** and **tabulation**.
3. Solve fundamental DP problems like Fibonacci sequence, coin change, and knapsack problem.
4. Analyze the time and space complexity of DP algorithms.

---

## Lab Outline

### 1. **What is Dynamic Programming?**
Dynamic Programming is based on:
- **Optimal Substructure**: A problem has optimal substructure if an optimal solution can be constructed from optimal solutions of its subproblems.
- **Overlapping Subproblems**: The problem can be divided into subproblems, which are reused multiple times.

### 2. **Two Approaches to DP**
1. **Memoization (Top-Down Approach)**:
   - Solve the problem recursively.
   - Cache results of subproblems for reuse.

2. **Tabulation (Bottom-Up Approach)**:
   - Solve the problem iteratively.
   - Build a table to store results of all subproblems.

---

## Tasks

### Task 1: Fibonacci Sequence (Recursive, Memoization, and Tabulation)
Implement the Fibonacci sequence using all three approaches.

#### Example
Fibonacci sequence:
$$
F(n) = F(n-1) + F(n-2), \quad F(0) = 0, \, F(1) = 1
$$

#### Implementation
```python
# Recursive Approach
def fib_recursive(n):
    if n <= 1:
        return n
    return fib_recursive(n - 1) + fib_recursive(n - 2)

# Memoization Approach
def fib_memoization(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memoization(n - 1, memo) + fib_memoization(n - 2, memo)
    return memo[n]

# Tabulation Approach
def fib_tabulation(n):
    if n <= 1:
        return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]
    return dp[n]
```

---

### Task 2: Coin Change Problem
Find the minimum number of coins required to make a given amount using a set of denominations.

#### Example
Input: `coins = [1, 2, 5], amount = 11`  
Output: `3` (11 = 5 + 5 + 1)

#### Implementation
```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    for coin in coins:
        for i in range(coin, amount + 1):
            dp[i] = min(dp[i], dp[i - coin] + 1)
    return dp[amount] if dp[amount] != float('inf') else -1
```

---

### Task 3: 0/1 Knapsack Problem
Given weights and values of `n` items, find the maximum value that can be obtained in a knapsack of capacity `W`.

#### Example
Input: `weights = [1, 3, 4], values = [15, 50, 60], capacity = 5`  
Output: `65` (Items: 3, 1)

#### Implementation
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    for i in range(1, n + 1):
        for w in range(1, capacity + 1):
            if weights[i - 1] <= w:
                dp[i][w] = max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1])
            else:
                dp[i][w] = dp[i - 1][w]
    return dp[n][capacity]
```

---

### Task 4: Longest Common Subsequence (LCS)
Find the length of the longest subsequence common to two strings.

#### Example
Input: `str1 = "abcde", str2 = "ace"`  
Output: `3` ("ace")

#### Implementation
```python
def lcs(str1, str2):
    m, n = len(str1), len(str2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if str1[i - 1] == str2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1] + 1
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])
    return dp[m][n]
```

---

## Bonus Task: Subset Sum Problem
Determine if a subset of numbers exists that sums to a given target.

#### Example
Input: `nums = [3, 34, 4, 12, 5, 2], target = 9`  
Output: `True` (Subset: [4, 5])

#### Implementation
```python
def subset_sum(nums, target):
    n = len(nums)
    dp = [[False] * (target + 1) for _ in range(n + 1)]
    for i in range(n + 1):
        dp[i][0] = True
    for i in range(1, n + 1):
        for j in range(1, target + 1):
            if nums[i - 1] <= j:
                dp[i][j] = dp[i - 1][j] or dp[i - 1][j - nums[i - 1]]
            else:
                dp[i][j] = dp[i - 1][j]
    return dp[n][target]
```

---

## Submission Instructions
1. Save your solutions in `dynamic_programming_basics.py`.
2. Ensure each function includes appropriate comments explaining the logic.
3. Submit the file via Canvas before the deadline.

---

## Additional Resources
- [MIT OpenCourseWare: Dynamic Programming](https://ocw.mit.edu)
- [GeeksforGeeks: Dynamic Programming Basics](https://www.geeksforgeeks.org)
- [LeetCode: DP Problems](https://leetcode.com/tag/dynamic-programming/)
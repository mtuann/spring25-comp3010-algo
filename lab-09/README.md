# Lab 09: Advanced Dynamic Programming

## Overview
Building on the basics of dynamic programming, this lab focuses on advanced concepts, techniques, and problem-solving strategies. These include multi-dimensional DP, state optimization, and solving complex problems such as matrix chain multiplication, shortest paths in weighted graphs, and more.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand advanced DP techniques like multi-dimensional DP and state optimization.
2. Solve complex DP problems that require creative state representation and transitions.
3. Analyze and optimize time and space complexity for advanced DP problems.

---

## Lab Outline

### 1. **Advanced DP Concepts**
- **Multi-dimensional DP**: Representing states with multiple parameters.
- **State Optimization**: Reducing space complexity by reusing state values.
- **Iterative vs Recursive**: Comparing approaches for complex DP problems.

### 2. **Problems and Techniques**
The lab includes problems that demonstrate practical applications of advanced DP techniques.

---

## Tasks

### Task 1: Matrix Chain Multiplication
Given a sequence of matrices, find the minimum number of scalar multiplications needed to multiply them.

#### Problem
Input: Dimensions of matrices, `p = [1, 2, 3, 4]` (matrix `i` has dimensions `p[i-1] x p[i]`).  
Output: Minimum scalar multiplications.

#### Implementation
```python
def matrix_chain_order(p):
    n = len(p) - 1
    dp = [[0] * n for _ in range(n)]
    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            dp[i][j] = float('inf')
            for k in range(i, j):
                cost = dp[i][k] + dp[k + 1][j] + p[i] * p[k + 1] * p[j + 1]
                dp[i][j] = min(dp[i][j], cost)
    return dp[0][n - 1]
```

---

### Task 2: Longest Increasing Subsequence (LIS)
Find the length of the longest subsequence in an array such that all elements are sorted in increasing order.

#### Problem
Input: `nums = [10, 9, 2, 5, 3, 7, 101, 18]`  
Output: `4` (Subsequence: [2, 3, 7, 101]).

#### Implementation
```python
def lis(nums):
    n = len(nums)
    dp = [1] * n
    for i in range(n):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)
```

---

### Task 3: Edit Distance (Levenshtein Distance)
Calculate the minimum number of operations (insertions, deletions, replacements) required to convert one string to another.

#### Problem
Input: `word1 = "kitten", word2 = "sitting"`  
Output: `3` (kitten → sitten → sittin → sitting).

#### Implementation
```python
def edit_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    for i in range(m + 1):
        for j in range(n + 1):
            if i == 0:
                dp[i][j] = j
            elif j == 0:
                dp[i][j] = i
            elif word1[i - 1] == word2[j - 1]:
                dp[i][j] = dp[i - 1][j - 1]
            else:
                dp[i][j] = 1 + min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1])
    return dp[m][n]
```

---

### Task 4: Subset Sum with Count
Find the number of subsets of a given array that sum up to a target.

#### Problem
Input: `nums = [1, 2, 3], target = 4`  
Output: `2` (Subsets: [1, 3] and [4]).

#### Implementation
```python
def subset_sum_count(nums, target):
    dp = [0] * (target + 1)
    dp[0] = 1
    for num in nums:
        for t in range(target, num - 1, -1):
            dp[t] += dp[t - num]
    return dp[target]
```

---

### Task 5: Minimum Path Sum in a Grid
Find the minimum path sum to reach the bottom-right corner of a grid from the top-left corner.

#### Problem
Input: 
```
grid = [
    [1, 3, 1],
    [1, 5, 1],
    [4, 2, 1]
]
```
Output: `7` (Path: 1 → 3 → 1 → 1 → 1).

#### Implementation
```python
def min_path_sum(grid):
    m, n = len(grid), len(grid[0])
    dp = [[0] * n for _ in range(m)]
    dp[0][0] = grid[0][0]
    for i in range(1, m):
        dp[i][0] = dp[i - 1][0] + grid[i][0]
    for j in range(1, n):
        dp[0][j] = dp[0][j - 1] + grid[0][j]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]
    return dp[m - 1][n - 1]
```

---

## Bonus Task: Traveling Salesman Problem (TSP)
Solve the TSP using DP with bit masking.

#### Problem
Input: A graph represented as a distance matrix.  
Output: Minimum cost of visiting all cities and returning to the starting city.

#### Hint
Use a bitmask to represent the visited cities and a DP table `dp[mask][i]` to store the cost of visiting all cities in `mask` ending at city `i`.

---

## Submission Instructions
1. Save your solutions in `advanced_dynamic_programming.py`.
2. Include comments explaining the logic behind each solution.
3. Submit the file via Canvas before the deadline.

---

## Additional Resources
- [TopCoder: Advanced Dynamic Programming](https://www.topcoder.com/community/competitive-programming)
- [GeeksforGeeks: Advanced DP Problems](https://www.geeksforgeeks.org)
- [LeetCode: Hard DP Problems](https://leetcode.com/tag/dynamic-programming/)
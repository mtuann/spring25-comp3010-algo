# Dynamic Programming – Principles & Applications

This document provides an overview of **Dynamic Programming (DP)**, including key principles, pseudocode, and applications like **Weighted Interval Scheduling** and **Segmented Least Squares**.

---

## **1. Principles of Dynamic Programming**
### **What is Dynamic Programming?**
Dynamic Programming (DP) is an optimization technique used to solve problems by breaking them into **overlapping subproblems** and solving each subproblem only once, storing the results.

### **Key Characteristics**
1. **Optimal Substructure** – The solution to a problem **can be built** from solutions to its subproblems.
2. **Overlapping Subproblems** – The problem **reuses** previously computed results.

### **Steps for Dynamic Programming**
1. **Define the state**: Identify the variables that uniquely represent a subproblem.
2. **Recurrence relation**: Express the solution in terms of smaller subproblems.
3. **Base cases**: Define trivial cases where the solution is known.
4. **Compute and store results**: Use **memoization (top-down)** or **tabulation (bottom-up)**.
5. **Reconstruct the solution (if needed)**.

### **Example: Fibonacci Numbers**
#### **Recursive Approach (Exponential Time)**
```
Fib(n):
    if n == 0 or n == 1:
        return n
    return Fib(n-1) + Fib(n-2)
```
🚫 **O(2ⁿ) – Exponential Complexity**  

#### **Memoized (Top-Down) Approach**
```
memo = {}

Fib(n):
    if n in memo:
        return memo[n]
    if n == 0 or n == 1:
        return n
    memo[n] = Fib(n-1) + Fib(n-2)
    return memo[n]
```
✅ **O(n) – Linear Complexity**  

#### **Tabulation (Bottom-Up) Approach**
```
Fib(n):
    dp = [0] * (n+1)
    dp[0] = 0, dp[1] = 1
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```
✅ **O(n) – Iterative and Efficient**  

---

## **2. Weighted Interval Scheduling**
### **Problem Statement**
Given `n` intervals `(s_i, f_i, v_i)` (start, finish, value), find a subset of **non-overlapping intervals** that maximizes the total value.

### **Steps**
1. **Sort intervals by finish time**.
2. **Define `p(i)`**: The largest index `j < i` where `f_j ≤ s_i`.
3. **Recurrence Relation**:
   ```
   OPT(i) = max( v_i + OPT(p(i)), OPT(i-1) )
   ```
   - **Include interval i** → add `v_i` + best solution before `p(i)`.
   - **Exclude interval i** → use `OPT(i-1)`.
4. **Use memoization or tabulation**.

### **Pseudocode**
```
ComputeP(intervals):
    for i from 1 to n:
        p[i] = largest index j < i such that finish[j] ≤ start[i]

WeightedIntervalScheduling(intervals):
    sort intervals by finish time
    ComputeP(intervals)
    dp = [0] * (n+1)
    
    for i from 1 to n:
        dp[i] = max(value[i] + dp[p[i]], dp[i-1])
    
    return dp[n]
```
✅ **O(n log n) – Efficient using sorting and binary search**.

### **Applications**
✔ **Job scheduling**  
✔ **Resource allocation**  
✔ **Maximizing event attendance**  

---

## **3. Segmented Least Squares**
### **Problem Statement**
Given `n` data points **(x_i, y_i)**, fit them with piecewise linear functions while minimizing **sum of squared errors (SSE) + penalty for adding segments**.

### **Key Idea**
Instead of fitting one global line, **use dynamic programming to minimize error + penalty cost**.

### **Steps**
1. **Compute the SSE for every possible segment**.
2. **Define `OPT(j)`: The minimum error cost for fitting points [1, j]**.
3. **Recurrence Relation**:
   ```
   OPT(j) = min( SSE(i, j) + c + OPT(i-1) )   for all i ≤ j
   ```
   - **SSE(i, j)** = error if we fit a line from `i` to `j`.
   - **c** = penalty for adding a segment.

### **Pseudocode**
```
SegmentedLeastSquares(points, c):
    compute SSE(i, j) for all 1 ≤ i ≤ j ≤ n
    dp = [∞] * (n+1)
    dp[0] = 0
    
    for j from 1 to n:
        for i from 1 to j:
            dp[j] = min(dp[j], SSE(i, j) + c + dp[i-1])
    
    return dp[n]
```
✅ **O(n²) using precomputed SSE**.

### **Applications**
✔ **Data compression**  
✔ **Curve fitting in statistics**  
✔ **Stock price trend analysis**  

---

## **Summary Table**
| **Problem** | **DP Recurrence** | **Time Complexity** |
|-------------|-----------------|-------------------|
| **Fibonacci** | `F(n) = F(n-1) + F(n-2)` | O(n) |
| **Weighted Interval Scheduling** | `OPT(i) = max(v_i + OPT(p(i)), OPT(i-1))` | O(n log n) |
| **Segmented Least Squares** | `OPT(j) = min(SSE(i,j) + c + OPT(i-1))` | O(n²) |

---

## **Practice Problems**
1. Implement **Weighted Interval Scheduling** using DP.
2. Implement **Segmented Least Squares** and experiment with different penalties.
3. Modify **Fibonacci DP** to return the **entire sequence**.

---

## **References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Algorithm Design – Jon Kleinberg & Éva Tardos**.
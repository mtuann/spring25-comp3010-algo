# Dynamic Programming II: Subset Sums, Knapsacks, and Sequence Alignment

This document covers advanced **Dynamic Programming (DP)** problems: **Subset Sum, Knapsack, and Sequence Alignment**, including problem formulations, recurrence relations, pseudocode, and real-world applications.

---

## **1. Subset Sum Problem**
### **Problem Statement**
Given a set of `n` positive integers and a target sum `S`, determine if there is a subset whose sum equals `S`.

### **Key Idea**
Use DP to check **if a subset sum can be formed using the first `i` elements**.

### **Recurrence Relation**
```
dp[i][s] = True  if s == 0  (empty subset)
dp[i][s] = dp[i-1][s] OR dp[i-1][s - A[i]]   if A[i] ≤ s
dp[i][s] = dp[i-1][s]   otherwise
```
- **Include `A[i]`** → Check `dp[i-1][s - A[i]]`.
- **Exclude `A[i]`** → Check `dp[i-1][s]`.

### **Pseudocode**
```
SubsetSum(A, S):
    n = len(A)
    dp = [[False] * (S+1) for _ in range(n+1)]
    
    for i in range(n+1):
        dp[i][0] = True
    
    for i in range(1, n+1):
        for s in range(1, S+1):
            if A[i-1] <= s:
                dp[i][s] = dp[i-1][s] or dp[i-1][s - A[i-1]]
            else:
                dp[i][s] = dp[i-1][s]
    
    return dp[n][S]
```
✅ **O(nS) time complexity**.

### **Applications**
✔ **Partitioning sets**  
✔ **Cryptography**  
✔ **Resource allocation**  

---

## **2. 0/1 Knapsack Problem**
### **Problem Statement**
Given `n` items, each with weight `w_i` and value `v_i`, and a knapsack with capacity `W`, find the **maximum value** that can be obtained by selecting items without exceeding `W`.

### **Key Idea**
Use DP to decide **whether to include each item**.

### **Recurrence Relation**
```
dp[i][w] = max( dp[i-1][w], dp[i-1][w - w_i] + v_i )   if w_i ≤ w
dp[i][w] = dp[i-1][w]   otherwise
```
- **Include `i`** → Add `v_i` to `dp[i-1][w - w_i]`.
- **Exclude `i`** → Keep `dp[i-1][w]`.

### **Pseudocode**
```
Knapsack(W, weights, values, n):
    dp = [[0] * (W+1) for _ in range(n+1)]
    
    for i in range(1, n+1):
        for w in range(1, W+1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], values[i-1] + dp[i-1][w - weights[i-1]])
            else:
                dp[i][w] = dp[i-1][w]
    
    return dp[n][W]
```
✅ **O(nW) time complexity**.

### **Applications**
✔ **Resource allocation**  
✔ **Investment decisions**  
✔ **Network routing optimization**  

---

## **3. Sequence Alignment**
### **Problem Statement**
Given two strings `X` and `Y`, find the optimal way to align them **by inserting gaps** such that the **cost is minimized**.

### **Key Idea**
Use DP to compute the **minimum cost of transforming X into Y**.

### **Cost Model**
1. **Match** → No cost if `X[i] == Y[j]`.
2. **Mismatch** → Cost `M` if `X[i] ≠ Y[j]`.
3. **Insertion/Deletion (Gap)** → Cost `G`.

### **Recurrence Relation**
```
dp[i][j] = min( 
    dp[i-1][j-1] + mismatchCost(X[i], Y[j]),   # Match/Mismatch
    dp[i-1][j] + G,   # Deletion (gap in Y)
    dp[i][j-1] + G    # Insertion (gap in X)
)
```

### **Pseudocode**
```
SequenceAlignment(X, Y, M, G):
    m, n = len(X), len(Y)
    dp = [[0] * (n+1) for _ in range(m+1)]
    
    for i in range(m+1):
        dp[i][0] = i * G
    for j in range(n+1):
        dp[0][j] = j * G
    
    for i in range(1, m+1):
        for j in range(1, n+1):
            match = dp[i-1][j-1] + (0 if X[i-1] == Y[j-1] else M)
            insert = dp[i][j-1] + G
            delete = dp[i-1][j] + G
            dp[i][j] = min(match, insert, delete)
    
    return dp[m][n]
```
✅ **O(mn) time complexity**.

### **Applications**
✔ **DNA sequence comparison**  
✔ **Plagiarism detection**  
✔ **Speech recognition**  

---

## **Summary Table**
| **Problem** | **Recurrence Relation** | **Time Complexity** |
|-------------|-------------------------|---------------------|
| **Subset Sum** | `dp[i][s] = dp[i-1][s] OR dp[i-1][s - A[i]]` | O(nS) |
| **0/1 Knapsack** | `dp[i][w] = max(dp[i-1][w], v_i + dp[i-1][w - w_i])` | O(nW) |
| **Sequence Alignment** | `dp[i][j] = min(dp[i-1][j-1] + mismatchCost, dp[i-1][j] + G, dp[i][j-1] + G)` | O(mn) |

---

## **Practice Problems**
1. Implement **Subset Sum** and modify it to find **all possible subsets**.
2. Implement **Knapsack Problem** and find the **items included in the optimal solution**.
3. Modify **Sequence Alignment** to return the **aligned strings**.

---

## **References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Algorithm Design – Jon Kleinberg & Éva Tardos**.
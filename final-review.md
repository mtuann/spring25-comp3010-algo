# 📚 Final Exam Revision: Algorithm Design (Post-Midterm Topics)

This document summarizes key topics covered **after the midterm**, including **Dynamic Programming, Graph Algorithms, Network Flows, NP-Completeness, and Approximation Algorithms**. Each section includes definitions, pseudocode, applications, and practice problems.

---

## **1. Principles of Dynamic Programming**
### **Definition**
- **Dynamic Programming (DP)** solves problems by **breaking them into subproblems** and using their solutions to build the final answer.
- **Two approaches**:
  1. **Top-down (Memoization)**
  2. **Bottom-up (Tabulation)**

### **Example: Fibonacci Numbers**
```python
def fibonacci(n):
    dp = [0] * (n+1)
    dp[1] = 1
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]
```

✅ **Used in:** Scheduling, shortest paths, bioinformatics.

---

## **2. Weighted Interval Scheduling**
### **Problem**
- Given `n` intervals `(s_i, f_i, v_i)`, find a **set of non-overlapping intervals** that **maximizes the sum of their values**.

### **DP Recurrence**
```
OPT(j) = max(v_j + OPT(p(j)), OPT(j-1))
```
where `p(j)` is the latest interval that does not overlap.

✅ **Used in:** Job scheduling, resource allocation.

---

## **3. Segmented Least Squares**
### **Problem**
- Given `n` points, fit them with the **minimum number of line segments** to minimize the total error.

### **DP Approach**
```
E(i, j) = error of fitting points i to j in a single segment
OPT(j) = min {OPT(i) + E(i+1, j) + C} for i < j
```
where `C` is the penalty for adding a new segment.

✅ **Used in:** Data compression, curve fitting.

---

## **4. Subset Sums and Knapsacks**
### **0/1 Knapsack Problem**
- Given `n` items `(value, weight)`, maximize **total value** under a weight limit `W`.

### **DP Recurrence**
```
dp[i][w] = max(dp[i-1][w], value_i + dp[i-1][w - weight_i])
```
✅ **Used in:** Resource allocation, cryptography.

---

## **5. Sequence Alignment**
### **Problem**
- Align two DNA sequences by **minimizing edit distance**.

### **DP Recurrence**
```
dp[i][j] = min(
    dp[i-1][j-1] + cost(match/mismatch),
    dp[i-1][j] + cost(delete),
    dp[i][j-1] + cost(insert)
)
```
✅ **Used in:** Bioinformatics, text similarity.

---

## **6. Max-Flow Problem & Ford-Fulkerson Algorithm**
### **Definition**
- Given a **directed graph** where edges have **capacities**, find the **maximum flow from source to sink**.

### **Algorithm (Ford-Fulkerson)**
```
While there exists an augmenting path:
    Find the path with BFS/DFS
    Augment flow along the path
    Update residual capacities
```

✅ **Used in:** Network routing, image segmentation.

---

## **7. Maximum Flows and Minimum Cuts**
### **Definition**
- The **max-flow min-cut theorem** states:
  ```
  Maximum flow = Minimum capacity cut
  ```
- Find **min-cut** by identifying **full edges in the residual graph**.

✅ **Used in:** Image processing, bipartite matching.

---

## **8. NP, NP-Completeness, and co-NP**
### **Definition**
- **P:** Problems solvable in polynomial time.
- **NP:** Problems verifiable in polynomial time.
- **NP-Complete (NPC):** Hardest problems in NP.
- **co-NP:** Problems whose complements are in NP.

✅ **Used in:** Cryptography, optimization.

---

## **9. Polynomial-Time Reductions**
### **Definition**
- **A problem `A` reduces to `B` if a solution to `B` gives a solution to `A`.**

✅ **Used in:** Proving NP-Completeness.

---

## **10. Approximation Algorithms**
### **Load Balancing**
- Assign `n` jobs to `m` machines **randomly** to balance load.
```
GreedyLoadBalancing():
    Assign each job to the least-loaded machine
```
✅ **Guarantees `2 - 1/m` approximation**.

### **LP Rounding for Knapsack**
- Solve **fractional knapsack** with **linear programming**, then round up.

✅ **Used in:** Scheduling, resource allocation.

---

## **11. Graph Coloring & Partitioning**
### **Problem**
- Assign **minimum colors** to a graph **such that no adjacent nodes share the same color**.

### **Greedy Algorithm**
```
for each vertex:
    Assign the smallest available color not used by neighbors
```

✅ **Used in:** Scheduling, register allocation.

---

## **12. Universal Hashing**
- **Randomized hashing method** to minimize collisions.
- Example:
```
h(x) = (ax + b) mod p mod m
```
✅ **Used in:** Data structures, cryptography.

---

## **13. Chernoff Bounds**
- **Probabilistic bound** on sum of independent random variables.

✅ **Used in:** Load balancing, randomized algorithms.

---

## **15. Final Exam Practice Problems**
1. **Implement weighted interval scheduling using DP**.
2. **Solve the max-flow problem on a given network**.
3. **Prove NP-completeness of 3-SAT**.
4. **Implement stable matching using Gale-Shapley**.
5. **Use LP rounding to approximate knapsack**.
6. **Analyze load balancing with Chernoff Bounds**.

---

## **16. Summary Table**
| **Topic** | **Algorithm** | **Use Case** |
|-----------|--------------|--------------|
| **Dynamic Programming** | Knapsack, Sequence Alignment | Optimization, Bioinformatics |
| **Max-Flow** | Ford-Fulkerson | Network Routing |
| **NP-Completeness** | 3-SAT, Reduction Proofs | Complexity Theory |
| **Approximation** | Load Balancing, LP Rounding | Resource Allocation |

---

## **17. References**
- 📖 **Algorithm Design – Kleinberg & Tardos**
- 📖 **Introduction to Algorithms – Cormen et al.**
- 📖 **Computational Complexity – Papadimitriou**
- 🔗 [NP-Completeness (Wikipedia)](https://en.wikipedia.org/wiki/NP-completeness)

🚀 **Good luck with your final exam!**
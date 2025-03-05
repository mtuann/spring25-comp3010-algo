# Polynomial-time Reductions; Sequencing Problem, Partitioning Problems, Graph Coloring, Numerical Problems

This document covers **polynomial-time reductions**, fundamental **NP-hard problems**, and common problem types such as **sequencing, partitioning, graph coloring, and numerical problems**. We explore definitions, algorithmic approaches, and pseudocode.

---

## **1. Polynomial-time Reductions**
### **Definition**
A problem **A** is **polynomial-time reducible** to a problem **B** (written as `A ≤p B`) if:
1. There exists a polynomial-time algorithm to transform any instance of **A** into an instance of **B**.
2. A solution to **B** provides a solution to **A**.

### **Why is Reduction Important?**
- Helps classify problems into **P, NP, NP-hard, and NP-complete**.
- Shows that solving one problem efficiently means another can also be solved efficiently.
- Used for proving **NP-completeness**.

### **Example: Reducing 3-SAT to CLIQUE**
- Convert a **Boolean formula** into a **graph**.
- Find a **clique** of size `k` that corresponds to a satisfying assignment.

### **Pseudocode for Reduction**
```
Reduce_3SAT_to_Clique(φ):
    Construct a graph G based on the formula φ
    Each clause corresponds to a set of vertices
    Connect vertices if they represent different literals in different clauses
    Return (G, k) where k is the number of clauses
```

---

## **2. Sequencing Problems**
### **Definition**
Sequencing problems involve **ordering tasks** subject to constraints like **deadlines, weights, or dependencies**.

### **Examples**
1. **Job Scheduling on a Single Machine**  
   - Given `n` jobs with processing times and deadlines, minimize **lateness**.
   - **Greedy Algorithm**: Schedule **earliest deadline first**.
   
2. **Weighted Job Scheduling with Deadlines**  
   - Maximize total weight while respecting deadlines.
   - Uses **Dynamic Programming**.

### **Pseudocode: Earliest Deadline First Scheduling**
```
EarliestDeadlineFirst(Jobs):
    Sort Jobs by increasing deadline
    Schedule each job sequentially
    Return the job order that minimizes lateness
```

✅ **Time Complexity:** O(n log n) (due to sorting).

---

## **3. Partitioning Problems**
### **Definition**
Partitioning problems involve dividing a set into **subsets** while optimizing some function.

### **Examples**
1. **Partition Problem**  
   - Can we split a set into two subsets of **equal sum**?  
   - **Subset Sum Reduction → NP-complete**.

2. **K-way Partitioning**  
   - Partition `n` elements into `k` subsets minimizing/maximizing sum differences.  
   - **Applications**: Load balancing, clustering.

### **Pseudocode: Dynamic Programming for Partition Problem**
```
Partition(A):
    total_sum = sum(A)
    if total_sum is odd:
        return False
    return SubsetSum(A, total_sum / 2)
```

✅ **Time Complexity:** O(n * sum) using DP.

---

## **4. Graph Coloring**
### **Definition**
Assign colors to **vertices** such that no two adjacent vertices have the same color.

### **Graph Coloring Problem (GCP)**
- **Input:** Graph `G = (V, E)`, integer `k`.
- **Output:** A valid k-coloring of `G` or report no solution.
- **Applications:** Timetabling, register allocation, Sudoku.

### **Greedy Coloring Algorithm**
```
GraphColoring(G, k):
    for each vertex v in G:
        Assign the smallest color not used by neighbors
```
✅ **Time Complexity:** O(V²) (for adjacency matrix).

### **Backtracking Approach**
```
BacktrackColoring(G, v, k):
    if all vertices are colored:
        return True
    for color in {1, ..., k}:
        if isValid(G, v, color):
            Assign color to v
            if BacktrackColoring(G, v+1, k):
                return True
            Unassign color
    return False
```
✅ **Time Complexity:** Exponential (NP-complete for `k ≥ 3`).

---

## **5. Numerical Problems**
### **Definition**
Involve **finding solutions to equations** or **optimizing numerical functions**.

### **Examples**
1. **Subset Sum Problem**  
   - Given a set `{a1, a2, ..., an}` and a target sum `S`, determine if a subset exists such that the sum equals `S`.
   - **NP-complete**.

2. **Knapsack Problem**  
   - **0/1 Knapsack**: Maximize total value without exceeding weight limit.
   - **Fractional Knapsack**: Greedy approach works.

### **Pseudocode: Subset Sum using Dynamic Programming**
```
SubsetSum(A, S):
    DP[0] = True
    for num in A:
        for j = S to num:
            DP[j] = DP[j] OR DP[j - num]
    return DP[S]
```
✅ **Time Complexity:** O(nS).

---

## **6. Summary Table**
| **Problem Type** | **Definition** | **Example Algorithm** | **Time Complexity** |
|-----------------|---------------|----------------------|---------------------|
| **Polynomial-time Reduction** | Converts problem A → B in poly-time | Reduction to CLIQUE, SAT → 3-SAT | O(poly(n)) |
| **Sequencing Problems** | Ordering tasks with constraints | Greedy (Earliest Deadline First) | O(n log n) |
| **Partitioning Problems** | Split elements into subsets | Dynamic Programming | O(n * sum) |
| **Graph Coloring** | Assign colors to vertices | Greedy / Backtracking | O(V²) / Exponential |
| **Numerical Problems** | Solve numeric constraints | Subset Sum DP | O(nS) |

---

## **7. Applications**
✔ **Polynomial-time Reductions** – Used in **NP-completeness proofs**.  
✔ **Sequencing Problems** – Task scheduling, manufacturing, CPU scheduling.  
✔ **Partitioning Problems** – Load balancing, clustering.  
✔ **Graph Coloring** – Timetabling, Sudoku, frequency assignment.  
✔ **Numerical Problems** – Cryptography, optimization.

---

## **8. Practice Problems**
1. Implement **Graph Coloring** using greedy & backtracking.
2. Solve the **Partition Problem** using **Dynamic Programming**.
3. Prove **Subset Sum ≤p Partition Problem**.
4. Apply **polynomial-time reduction** to transform **SAT → CLIQUE**.

---

## **9. References**
- 📖 **Introduction to Algorithms – CLRS**.
- 📖 **Computers and Intractability – Garey & Johnson**.

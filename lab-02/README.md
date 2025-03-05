# Algorithm Design Paradigms, Efficiency, and Run-time Analysis

## Overview
Algorithm design is a crucial aspect of computer science that focuses on **creating efficient solutions** to computational problems. This module explores:
1. **Motivation for Algorithm Design Paradigms**
2. **Concepts of Algorithmic Efficiency**
3. **Run-time Analysis of Algorithms**

---

## 1. **Motivation for Algorithm Design Paradigms**
### Why Study Algorithm Design?
- **Efficiency Matters**: Poorly designed algorithms can be **exponentially slower**.
- **Scalability**: Algorithms must handle **large inputs** efficiently.
- **Computational Resources**: Optimization saves **time, memory, and processing power**.

### **Common Algorithm Design Paradigms**
1. **Divide and Conquer** – Breaks a problem into smaller subproblems and combines solutions.  
   📌 **Example**: Merge Sort, Quick Sort, Binary Search.  
2. **Greedy Algorithms** – Makes locally optimal choices at each step.  
   📌 **Example**: Huffman Coding, Activity Selection.  
3. **Dynamic Programming (DP)** – Solves subproblems once and stores results to avoid recomputation.  
   📌 **Example**: Fibonacci, Knapsack, Floyd-Warshall Algorithm.  
4. **Backtracking & Branch and Bound** – Used for combinatorial problems by searching through possibilities.  
   📌 **Example**: N-Queens, Traveling Salesman Problem (TSP).  

Each paradigm has **strengths and weaknesses**, and selecting the right approach is **key** to solving problems efficiently.

---

## 2. **Concepts of Algorithmic Efficiency**
Efficiency is measured by analyzing **how an algorithm’s resource consumption scales** with input size.

### **Time Complexity**
- **Definition**: Measures how the execution time of an algorithm increases as input size `n` grows.
- **Big-O Notation**: Expresses the upper bound of an algorithm’s growth rate.

| Complexity | Notation | Example Algorithm |
|------------|----------|------------------|
| Constant   | O(1)  | Hash table lookup |
| Logarithmic | O(log n) | Binary Search |
| Linear     | O(n)  | Linear Search |
| Linearithmic | O(n log n) | Merge Sort, Quick Sort (avg) |
| Quadratic  | O(n²)  | Bubble Sort, Selection Sort |
| Exponential | O(2ⁿ)  | Recursive Fibonacci |
| Factorial  | O(n!)  | Brute force TSP |

📌 **Example:**  
Finding an element in an **unsorted array** → **O(n)** (linear search).  
Finding an element in a **sorted array** → **O(log n)** (binary search).

### **Space Complexity**
- **Definition**: Measures the memory an algorithm needs.
- **In-place algorithms**: Use **O(1) or O(log n)** extra space.
- **Recursive algorithms**: Often use **O(n)** stack space.

---

## 3. **Run-time Analysis of Algorithms**
### **Types of Algorithm Analysis**
1. **Worst-case analysis** (Big-O) – Maximum runtime for **any** input of size `n`.
2. **Best-case analysis** (Omega-Ω) – Minimum runtime (not very useful for practical optimization).
3. **Average-case analysis** (Theta-Θ) – Expected runtime for **random inputs**.

📌 **Example: QuickSort**  
- **Worst-case**: O(n²) (when pivot selection is poor).  
- **Best-case**: O(n log n) (ideal pivot selection).  
- **Average-case**: O(n log n) (randomized pivot).  

### **Asymptotic Growth Comparison**
For large `n`:
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)
```
This means **choosing the right algorithm** can significantly impact performance.

---

## **Pseudocode for Time Complexity Analysis**
To illustrate **run-time analysis**, let’s analyze some algorithms.

### **1. Linear Search (O(n))**
```
LinearSearch(arr, target):
    for i = 0 to arr.length - 1:
        if arr[i] == target:
            return i
    return -1  # Not found
```
**Analysis**:
- **Worst-case**: O(n) (target is last or absent).
- **Best-case**: O(1) (target is first element).
- **Space complexity**: O(1) (no extra memory used).

---

### **2. Binary Search (O(log n))**
```
BinarySearch(arr, target, low, high):
    if low > high:
        return -1
    mid = (low + high) / 2
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return BinarySearch(arr, target, low, mid - 1)
    else:
        return BinarySearch(arr, target, mid + 1, high)
```
**Analysis**:
- **Worst-case**: O(log n) (logarithmic search space reduction).
- **Best-case**: O(1) (target found at `mid` in the first check).
- **Space complexity**: O(log n) (recursive calls).

---

### **3. Merge Sort (O(n log n))**
```
MergeSort(arr):
    if arr.length ≤ 1:
        return arr
    mid = arr.length / 2
    left = MergeSort(arr[0:mid])
    right = MergeSort(arr[mid:])
    return Merge(left, right)
```
**Analysis**:
- **Worst-case**: O(n log n) (recursive divide and merge).
- **Best-case**: O(n log n).
- **Space complexity**: O(n) (extra space for merging).

---

## **Practical Examples**
1. **Searching Algorithms**:
   - **O(n) for linear search** vs. **O(log n) for binary search**.
2. **Sorting Algorithms**:
   - **O(n log n) (Merge Sort, Quick Sort)** vs. **O(n²) (Bubble Sort)**.
3. **Graph Algorithms**:
   - **O(V + E) (BFS/DFS for connectivity)**.
   - **O(V²) (Floyd-Warshall for shortest path)**.

---

## **Learning Outcomes**
✔ Understand **algorithmic paradigms** and their motivations.  
✔ Analyze **time complexity** and **asymptotic growth**.  
✔ Differentiate between **best, worst, and average-case runtimes**.  
✔ Apply **efficient algorithms** to real-world problems.  

---

## **Resources**
- 📖 **Introduction to Algorithms (CLRS)** - Chapter on **Algorithm Analysis**.
- 📖 **Algorithm Design** - Jon Kleinberg & Éva Tardos.
- 🔗 **Big-O Complexity Cheat Sheet**: [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)
- 🔗 **Sorting Algorithm Visualizations**: [Sorting Visualizer](https://visualgo.net/en/sorting)

---

## **Exercises**
1. Implement **linear search** and **binary search**; compare their runtimes.
2. Implement **Merge Sort** and **QuickSort**; analyze their performance.
3. Solve problems on **time complexity and efficiency**.
4. Compare different sorting algorithms using **real-world datasets**.
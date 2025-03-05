# Divide and Conquer: Merge Sort & Counting Inversions

## Overview
This module covers:
1. **The Divide-and-Conquer Paradigm** – A fundamental algorithmic strategy.
2. **Merge Sort** – An efficient sorting algorithm based on divide-and-conquer.
3. **Counting Inversions** – A problem that can be solved using merge sort.

---

# 1. **Divide-and-Conquer Algorithm Paradigm**

### **Definition**
The **Divide-and-Conquer** approach consists of three steps:
1. **Divide**: Break the problem into smaller subproblems of the same type.
2. **Conquer**: Solve the subproblems recursively.
3. **Combine**: Merge the solutions of the subproblems into a final solution.

📌 **Applications**:
- Sorting (**Merge Sort, Quick Sort**)
- Searching (**Binary Search**)
- Matrix multiplication (**Strassen's Algorithm**)
- Closest pair of points in computational geometry.

### **General Pseudocode**
```
DivideAndConquer(problem):
    if problem is small enough:
        solve it directly
    else:
        divide problem into subproblems
        recursively solve each subproblem
        combine solutions
```

### **Time Complexity Analysis**
If a problem of size **n** is divided into **b** subproblems of size **n/b**, and each step takes **O(f(n))**, we get:
```
T(n) = b * T(n/b) + f(n)
```
Solving this recurrence using **Master Theorem** gives different complexities based on **f(n)**.

---

# 2. **Merge Sort Algorithm**

### **Definition**
Merge Sort is a **divide-and-conquer** sorting algorithm that:
- **Divides** the array into two halves.
- **Recursively sorts** each half.
- **Merges** the two sorted halves into a single sorted array.

📌 **Properties**:
- **Stable** sorting algorithm.
- **Time Complexity**: **O(n log n)** (worst, average, and best case).
- **Space Complexity**: **O(n)** (requires extra space).

### **Steps**
1. **Divide** the array into two halves.
2. **Recursively sort** each half.
3. **Merge** the two halves.

### **Pseudocode**
```
MergeSort(arr, left, right):
    if left >= right:
        return
    mid = (left + right) / 2
    MergeSort(arr, left, mid)
    MergeSort(arr, mid+1, right)
    Merge(arr, left, mid, right)
```
```
Merge(arr, left, mid, right):
    Create temp arrays Left[] and Right[]
    Copy data into Left[] and Right[]
    Merge Left[] and Right[] into arr[]
```

📌 **Example**
```
Input:  [5, 2, 4, 7, 1, 3, 6, 8]
Step 1: [5, 2, 4, 7]  [1, 3, 6, 8]   (Split)
Step 2: [2, 5] [4, 7]  [1, 3] [6, 8] (Sort each half)
Step 3: [2, 4, 5, 7]  [1, 3, 6, 8]   (Merge sorted halves)
Step 4: [1, 2, 3, 4, 5, 6, 7, 8]     (Final merge)
```

### **Comparison with Other Sorting Algorithms**
| Algorithm   | Time Complexity | Space Complexity | Stability |
|------------|---------------|----------------|-----------|
| Merge Sort | O(n log n)    | O(n)           | ✅ Stable |
| Quick Sort | O(n log n) (avg) / O(n²) (worst) | O(log n) | ❌ Unstable (in some cases) |
| Bubble Sort | O(n²)        | O(1)           | ✅ Stable |

---

# 3. **Counting Inversions using Merge Sort**
### **Definition**
An **inversion** in an array **A** of size **n** is a **pair (i, j)** such that:
- **i < j**, but **A[i] > A[j]**.

📌 **Example**:
```
Input:  [2, 4, 1, 3, 5]
Inversions: (2,1), (4,1), (4,3)
Output: 3
```

### **Naïve Approach**
A **brute-force** solution iterates over all pairs **(i, j)** in **O(n²)** time.

### **Efficient Approach (Merge Sort)**
Instead of **brute-force**, we count inversions **while merging** in Merge Sort:
- When merging two halves, **if an element from the right half is smaller**, it means all remaining elements in the left half form an inversion.

### **Steps**
1. **Divide** the array.
2. **Recursively count inversions** in both halves.
3. **Count split inversions** while merging.

### **Pseudocode**
```
CountInversions(arr, left, right):
    if left >= right:
        return 0
    mid = (left + right) / 2
    leftInversions = CountInversions(arr, left, mid)
    rightInversions = CountInversions(arr, mid+1, right)
    splitInversions = MergeAndCount(arr, left, mid, right)
    return leftInversions + rightInversions + splitInversions
```
```
MergeAndCount(arr, left, mid, right):
    Create temp arrays Left[] and Right[]
    Count pairs where Left[i] > Right[j]
    Merge Left[] and Right[] back into arr[]
```

📌 **Example**
```
Input:  [5, 2, 4, 1, 3]
Step 1: Divide into [5, 2, 4] and [1, 3]
Step 2: Count inversions in [5, 2, 4] -> (5,2), (5,4)
Step 3: Count inversions in [1, 3] -> 0
Step 4: Count split inversions while merging -> (5,1), (5,3), (2,1), (4,1)
Total Inversions: 6
```

### **Time Complexity**
- **O(n log n)** (efficient compared to **O(n²)** brute-force).

---

# **Summary**
✔ **Divide-and-Conquer**: Breaks problems into smaller parts, solves recursively, and merges results.  
✔ **Merge Sort**: An **O(n log n) stable sorting algorithm** using **divide-and-conquer**.  
✔ **Counting Inversions**: Uses **merge sort** to efficiently count **pairs (i, j) where A[i] > A[j]**.  

---

# **Exercises**
1. Implement **Merge Sort** and analyze its runtime for different inputs.
2. Implement **Counting Inversions using Merge Sort**.
3. Modify Merge Sort to **count the number of swaps** needed to sort an array.
4. Solve **inversion counting problems** on Codeforces, LeetCode, and AtCoder.

---

# **Resources**
- 📖 **Introduction to Algorithms (CLRS)** - Merge Sort & Inversions.
- 📖 **Algorithm Design** - Jon Kleinberg & Éva Tardos.
- 🔗 **Merge Sort Visualization**: [Sorting Visualizer](https://visualgo.net/en/sorting)
# Divide and Conquer II: Integer Multiplication & Closest Pair of Points

## Overview
This module covers:
1. **Efficient Integer Multiplication** using Divide and Conquer.
2. **Closest Pair of Points** problem and its solution using Divide and Conquer.

---

# 1. **Integer Multiplication using Divide and Conquer**

### **Problem Statement**
Given two large integers **X** and **Y**, we want to compute their product efficiently.

### **Naïve Approach (School Multiplication)**
- Multiply each digit of **X** with each digit of **Y**.
- Time Complexity: **O(n²)**.

### **Divide-and-Conquer Approach**
Using recursion, we can break multiplication into smaller subproblems.

📌 **Example**  
Let **X = 1234**, **Y = 5678**, and split them into two halves:
```
X = 12 | 34    (A | B)
Y = 56 | 78    (C | D)
```
Then:
```
X * Y = (A * C) * 10^n + ((A * D) + (B * C)) * 10^(n/2) + (B * D)
```
This reduces the problem into **4 smaller multiplications**.

### **Karatsuba Algorithm (Optimized Version)**
Karatsuba reduces the number of multiplications from **4** to **3**:
```
X * Y = (A * C) * 10^n + ((A + B) * (C + D) - A*C - B*D) * 10^(n/2) + (B * D)
```
📌 **Time Complexity**: **O(n^log₂3) ≈ O(n^1.58)**  
📌 **Space Complexity**: **O(n)**  

### **Pseudocode**
```
Karatsuba(X, Y):
    if X or Y is small enough:
        return X * Y
    n = max(length of X, length of Y)
    m = n / 2
    A, B = split X into two halves
    C, D = split Y into two halves
    AC = Karatsuba(A, C)
    BD = Karatsuba(B, D)
    AD_BC = Karatsuba(A + B, C + D) - AC - BD
    return AC * 10^n + AD_BC * 10^(n/2) + BD
```

📌 **Comparison**
| Algorithm          | Time Complexity  | Space Complexity |
|-------------------|-----------------|------------------|
| Naïve Multiplication | O(n²)         | O(1)            |
| Karatsuba         | O(n^1.58)       | O(n)            |
| Strassen's Algorithm (Matrix Multiplication) | O(n^2.81) | O(n²) |

---

# 2. **Closest Pair of Points Problem**

### **Problem Statement**
Given **n** points on a 2D plane, find the pair with the **smallest Euclidean distance**.

### **Naïve Approach (Brute Force)**
Compute all **n(n-1)/2** pairwise distances.

📌 **Time Complexity**: **O(n²)**  
📌 **Space Complexity**: **O(1)**  

### **Divide-and-Conquer Approach**
1. **Sort the points by X-coordinate.**
2. **Recursively find the closest pair** in both halves.
3. **Check for closest pairs across the split line.**

📌 **Time Complexity**: **O(n log n)**  
📌 **Space Complexity**: **O(n)**  

### **Pseudocode**
```
ClosestPair(P):
    if size of P is small:
        return brute force solution
    Sort P by x-coordinates
    mid = |P| / 2
    leftHalf = P[:mid]
    rightHalf = P[mid:]
    d1 = ClosestPair(leftHalf)
    d2 = ClosestPair(rightHalf)
    d = min(d1, d2)
    strip = Points within distance d from mid-line
    return min(d, ClosestSplitPair(strip, d))
```

```
ClosestSplitPair(strip, d):
    Sort strip by y-coordinate
    for each point p in strip:
        check only next 6 points for a closer pair
    return minimum distance found
```

📌 **Why Check Only 6 Points?**
- Due to geometric properties, there can be at most **6 points** within distance **d** of any given point in the strip.

📌 **Example**
```
Input:  [(1,2), (3,6), (4,5), (7,8), (10,12)]
Output: Closest pair (3,6) and (4,5) with distance 1.41
```

### **Comparison**
| Algorithm          | Time Complexity  | Space Complexity |
|-------------------|-----------------|------------------|
| Brute Force      | O(n²)           | O(1)            |
| Divide & Conquer | O(n log n)      | O(n)            |

---

# **Summary**
✔ **Karatsuba Algorithm** reduces integer multiplication from **O(n²) to O(n^1.58)**.  
✔ **Closest Pair Algorithm** improves from **O(n²) to O(n log n)**.  
✔ **Divide-and-Conquer** helps solve these problems **efficiently**.  

---

# **Exercises**
1. Implement **Karatsuba Multiplication** for large numbers.
2. Implement **Closest Pair of Points using Divide and Conquer**.
3. Compare **Karatsuba vs Naïve Multiplication** on large inputs.
4. Solve **Closest Pair of Points** problems on Codeforces, LeetCode.

---

# **Resources**
- 📖 **Introduction to Algorithms (CLRS)** - Divide & Conquer.
- 📖 **Algorithm Design** - Jon Kleinberg & Éva Tardos.
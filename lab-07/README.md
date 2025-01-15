# Lab 07: Advanced Divide and Conquer

## Overview
This lab explores **Advanced Divide and Conquer** techniques, a cornerstone of efficient algorithm design. Divide and conquer breaks a problem into smaller sub-problems, solves them recursively, and combines their solutions to solve the original problem. Advanced techniques often involve applying divide and conquer to more complex scenarios.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand advanced applications of the divide and conquer paradigm.
2. Implement algorithms such as the **Fast Fourier Transform (FFT)**, **Closest Pair of Points**, and **Matrix Multiplication** using divide and conquer.
3. Analyze the time complexity of advanced divide and conquer algorithms.
4. Recognize the importance of recurrence relations in analyzing these algorithms.

---

## Lab Outline

### 1. **What is Advanced Divide and Conquer?**
Divide and conquer algorithms follow these steps:
1. **Divide**: Split the problem into smaller sub-problems.
2. **Conquer**: Solve the sub-problems recursively.
3. **Combine**: Merge the results to solve the original problem.

Advanced techniques apply this method to:
- Multi-dimensional data.
- Numerical algorithms.
- Geometric problems.

### 2. **Importance of Recurrence Relations**
Many divide and conquer algorithms' complexities are analyzed using recurrence relations, e.g., **T(n) = aT(n/b) + O(n^d)**. 

Use the **Master Theorem** for analysis:
- $a$: Number of sub-problems.
- $b$: Division factor.
- $d$: Cost of combining solutions.

---

## Tasks

### Task 1: Implementing Fast Fourier Transform (FFT)
The **FFT** algorithm efficiently computes the discrete Fourier transform of a sequence, often used in signal processing.

#### Algorithm Outline
1. If the input size $n$ is 1, return the input.
2. Split the sequence into even and odd indices.
3. Compute FFT recursively on both parts.
4. Combine results using the formula:
$$
   X[k] = E[k] + W_k \cdot O[k], \quad W_k = e^{-2\pi i k / n}
$$

#### Example Implementation
```python
import cmath

def fft(a):
    n = len(a)
    if n == 1:
        return a
    w_n = cmath.exp(-2j * cmath.pi / n)
    w = 1
    a_even = fft(a[0::2])
    a_odd = fft(a[1::2])
    y = [0] * n
    for k in range(n // 2):
        y[k] = a_even[k] + w * a_odd[k]
        y[k + n // 2] = a_even[k] - w * a_odd[k]
        w *= w_n
    return y
```

---

### Task 2: Closest Pair of Points (2D Plane)
Given a set of points in a 2D plane, find the pair of points with the smallest distance using divide and conquer.

#### Algorithm Outline
1. Sort points by x-coordinates.
2. Divide points into two halves.
3. Find the closest pair in each half recursively.
4. Combine results by checking pairs across the dividing line.

#### Steps
- Use the Euclidean distance formula.
- Maintain a "strip" of points close to the dividing line.

#### Example Implementation
```python
import math

def distance(p1, p2):
    return math.sqrt((p1[0] - p2[0])**2 + (p1[1] - p2[1])**2)

def closest_pair(points):
    if len(points) <= 3:
        return min((distance(p1, p2), (p1, p2)) 
                   for i, p1 in enumerate(points) 
                   for p2 in points[i+1:])
    
    mid = len(points) // 2
    mid_point = points[mid]
    
    dl = closest_pair(points[:mid])
    dr = closest_pair(points[mid:])
    d = min(dl, dr)
    
    strip = [p for p in points if abs(p[0] - mid_point[0]) < d[0]]
    strip.sort(key=lambda p: p[1])
    
    for i in range(len(strip)):
        for j in range(i + 1, len(strip)):
            if strip[j][1] - strip[i][1] >= d[0]:
                break
            d = min(d, (distance(strip[i], strip[j]), (strip[i], strip[j])))
    return d
```

---

### Task 3: Matrix Multiplication (Strassen's Algorithm)
Strassen's algorithm improves matrix multiplication time complexity from $O(n^3)$ to approximately $O(n^{2.81})$.

#### Algorithm Outline
1. Split two $n \times n$ matrices into $n/2 \times n/2$ submatrices.
2. Compute 7 products recursively instead of 8.
3. Combine results to get the final matrix.

#### Example Implementation
```python
def add_matrix(A, B):
    return [[A[i][j] + B[i][j] for j in range(len(A))] for i in range(len(A))]

def subtract_matrix(A, B):
    return [[A[i][j] - B[i][j] for j in range(len(A))] for i in range(len(A))]

def strassen(A, B):
    n = len(A)
    if n == 1:
        return [[A[0][0] * B[0][0]]]
    
    mid = n // 2
    A11 = [row[:mid] for row in A[:mid]]
    A12 = [row[mid:] for row in A[:mid]]
    A21 = [row[:mid] for row in A[mid:]]
    A22 = [row[mid:] for row in A[mid:]]
    
    B11 = [row[:mid] for row in B[:mid]]
    B12 = [row[mid:] for row in B[:mid]]
    B21 = [row[:mid] for row in B[mid:]]
    B22 = [row[mid:] for row in B[mid:]]
    
    M1 = strassen(add_matrix(A11, A22), add_matrix(B11, B22))
    M2 = strassen(add_matrix(A21, A22), B11)
    M3 = strassen(A11, subtract_matrix(B12, B22))
    M4 = strassen(A22, subtract_matrix(B21, B11))
    M5 = strassen(add_matrix(A11, A12), B22)
    M6 = strassen(subtract_matrix(A21, A11), add_matrix(B11, B12))
    M7 = strassen(subtract_matrix(A12, A22), add_matrix(B21, B22))
    
    C11 = add_matrix(subtract_matrix(add_matrix(M1, M4), M5), M7)
    C12 = add_matrix(M3, M5)
    C21 = add_matrix(M2, M4)
    C22 = add_matrix(subtract_matrix(add_matrix(M1, M3), M2), M6)
    
    return [C11[i] + C12[i] for i in range(mid)] + [C21[i] + C22[i] for i in range(mid)]
```

---

## Bonus Task: Recurrence Relation Practice
1. Solve recurrence relations using the Master Theorem.
2. Analyze FFT, Closest Pair, and Strassen algorithms.

---

## Submission Instructions
1. Save your solutions in `advanced_divide_conquer.py`.
2. Submit via Canvas by the deadline.
3. Include comments and analysis of each algorithm.

---

## Additional Resources
- [MIT OpenCourseWare: Divide and Conquer](https://ocw.mit.edu)
- [Master Theorem](https://en.wikipedia.org/wiki/Master_theorem)
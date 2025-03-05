# Lab 01: Introduction and Stable Matching

## Overview
Welcome to the first lab of **COMP 3010: Algorithm Design and Analysis**! In this lab, you'll be introduced to the basics of Python programming in the context of algorithm design. The main focus of this lab is to understand and implement the **Stable Matching** problem using the Gale-Shapley algorithm.

---

## Learning Objectives
By the end of this lab, you should be able to:
1. Familiarize yourself with Python basics, including input/output, loops, and lists.
2. Understand the Stable Matching problem and its significance.
3. Implement the Gale-Shapley algorithm to solve the Stable Matching problem.

---

## Lab Outline
### 1. **Introduction to Python**
   - Basic syntax and data structures:
     - Lists, dictionaries, and sets.
   - Control flow:
     - `if`, `for`, and `while` statements.
   - Functions in Python.
   - Input and output operations.

### 2. **The Stable Matching Problem**
   - Understand the problem statement:
     - Matching two groups (e.g., men and women) with preferences while ensuring stability.
   - Learn the Gale-Shapley algorithm:
     - **Key Idea:** Iteratively propose matches to find a stable pairing.

### 3. **Implementation Tasks**
   - Write Python code to implement the Gale-Shapley algorithm.
   - Test your implementation with sample inputs.

---

## Getting Started

### Prerequisites
- Ensure Python (>= 3.8) is installed on your system.
- A code editor such as VSCode, PyCharm, or Jupyter Notebook is recommended.

### Files Provided
1. `preferences_input.txt` - A sample input file containing preferences for two groups.
2. `gale_shapley.py` - A template file for your implementation.
3. `README.md` - This instruction file.

---

# The Stable Matching Problem

## Overview
This module covers:
1. **Definition of the Stable Matching Problem**.
2. **Gale-Shapley Algorithm** for finding a **stable matching**.
3. **Proof of Stability & Properties**.
4. **Applications in real-world scenarios**.

---

# 1. **Stable Matching Problem**

### **Problem Statement**
We are given two equal-sized sets:
- **n men** and **n women**.
- Each person ranks all members of the opposite group **in order of preference**.

📌 **Goal**: Find a **stable matching**, where no two people prefer each other over their assigned partners.

### **Example**
Consider **3 men** and **3 women**:

| Man  | Preferences       | Woman | Preferences       |
|------|------------------|-------|------------------|
| A    | X > Y > Z        | X     | B > A > C        |
| B    | Y > X > Z        | Y     | C > A > B        |
| C    | Z > X > Y        | Z     | A > C > B        |

### **What is Stability?**
A matching is **unstable** if:
- A man **M** and a woman **W** prefer each other over their assigned partners.

📌 **Example of an Unstable Pair**:
- Suppose **A is matched with Z** and **B is matched with X**.
- If **A prefers X over Z** and **X prefers A over B**, this creates an **unstable pair**.

📌 **Goal**: Find a matching where **no unstable pairs exist**.

---

# 2. **Gale-Shapley Algorithm (Deferred Acceptance)**

### **Idea**
Men propose to women in rounds, and women **tentatively accept** the best option.

### **Pseudocode**
```
GaleShapley(menPreferences, womenPreferences):
    while there is an unengaged man:
        m proposes to his favorite woman w who hasn't rejected him
        if w is free:
            match (m, w)
        else:
            if w prefers m over her current partner m':
                match (m, w)
                unengage(m')
            else:
                w rejects m
```
📌 **Time Complexity**: **O(n²)**  
📌 **Space Complexity**: **O(n)**  

### **Step-by-Step Example**
#### **Input**
Men’s preferences:
```
A: X > Y > Z
B: Y > X > Z
C: Z > X > Y
```
Women’s preferences:
```
X: B > A > C
Y: C > A > B
Z: A > C > B
```

#### **Execution**
1. **Round 1**:  
   - **A proposes to X** (X tentatively accepts A).  
   - **B proposes to Y** (Y tentatively accepts B).  
   - **C proposes to Z** (Z tentatively accepts C).

2. **Round 2**:  
   - **A gets rejected by X (since X prefers B)**.
   - **A now proposes to Y**.
   - **Y prefers A over B, so B is rejected**.
   - **B now proposes to X again**.

3. **Final Matching**
   ```
   A → Y
   B → X
   C → Z
   ```

---

# 3. **Properties of the Gale-Shapley Algorithm**
✅ **Always finds a stable matching**.  
✅ **Men-optimal (each man gets the best possible stable match)**.  
✅ **Women-pessimal (each woman gets the worst stable match for her)**.  
✅ **Time Complexity: O(n²), Efficient for large inputs**.

📌 **Proof of Stability**
- If there were an **unstable pair (M, W)**, then W **must have rejected M earlier**, meaning she **already has a better match**.

---

# 4. **Applications of Stable Matching**
The Stable Matching Problem has real-world applications in:
1. **College Admissions** → Students & Universities.  
2. **Residency Matching** → Medical students & hospitals (NRMP).  
3. **Job Recruitment** → Companies & candidates.  
4. **Online Dating & Marriage Algorithms**.

---

# **Exercises**
1. Implement the **Gale-Shapley Algorithm**.
2. Modify the algorithm for **women-proposing** instead of men.
3. Prove that the Gale-Shapley Algorithm always terminates in **O(n²)** time.
4. Explore **real-world applications** of stable matching (e.g., NRMP, college admissions).

---

# **Resources**
- 📖 **Introduction to Algorithms (CLRS)** – Chapter on Stable Matching.
- 📖 **Algorithm Design – Jon Kleinberg & Éva Tardos**.
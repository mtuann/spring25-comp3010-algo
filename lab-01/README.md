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

## Task 1: Setup and Warm-Up
1. Open the `gale_shapley.py` file.
2. Read the comments and understand the structure of the code template.
3. Implement a function `read_preferences(filename)` to read preferences from the `preferences_input.txt` file. The format is:
   ```
   Group A:
   A1: B2, B1, B3
   A2: B1, B2, B3
   A3: B3, B2, B1

   Group B:
   B1: A1, A2, A3
   B2: A3, A2, A1
   B3: A2, A1, A3
   ```

---

## Task 2: Implement the Gale-Shapley Algorithm
1. Write the function `gale_shapley(men, women)` that:
   - Accepts two dictionaries: `men` and `women`, where each key is an individual, and the value is a list of preferences.
   - Returns a stable matching as a dictionary.
2. Key steps:
   - Initialize all members of one group as free.
   - Iteratively propose matches based on preferences.
   - Update matchings until all individuals are matched.

---

## Task 3: Testing and Debugging
1. Use the sample data provided in `preferences_input.txt`.
2. Verify your implementation by running `gale_shapley.py` with:
   ```bash
   python gale_shapley.py
   ```
3. Confirm that the output is a stable matching.

---

## Sample Input and Output

### Input (`preferences_input.txt`):
```
Group A:
A1: B1, B2, B3
A2: B2, B1, B3
A3: B3, B1, B2

Group B:
B1: A1, A2, A3
B2: A2, A3, A1
B3: A3, A1, A2
```

### Expected Output:
```
Stable Matching:
A1 -> B1
A2 -> B2
A3 -> B3
```

---

## Submission Instructions
1. Save your implementation in `gale_shapley.py`.
2. Include test cases and outputs in a separate file named `test_results.txt`.
3. Submit your files on Canvas by the deadline.

---

## Additional Resources
- [Gale-Shapley Algorithm on Wikipedia](https://en.wikipedia.org/wiki/Stable_marriage_problem)
- Python documentation: [https://docs.python.org/3/](https://docs.python.org/3/)

---

## Notes
- Pay attention to edge cases, such as when preferences are incomplete or cyclic.
- Ensure your code is well-commented and follows Python best practices.
- If you have any questions, contact the lab TA during office hours.
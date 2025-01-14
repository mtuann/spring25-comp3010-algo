# Lab 04: Greedy Algorithms

## Overview
In **Lab 04: Greedy Algorithms**, you will explore one of the most intuitive algorithmic paradigms—**Greedy Algorithms**. These algorithms make locally optimal choices at each step, aiming to find the global optimum. You will implement classic greedy algorithms and analyze their correctness and efficiency.

---

## Learning Objectives
By the end of this lab, you will:
1. Understand the principles of the **Greedy Algorithm paradigm**.
2. Implement and apply greedy algorithms to solve classical optimization problems.
3. Evaluate when greedy algorithms work and their limitations.
4. Analyze time and space complexity of greedy solutions.

---

## Lab Outline

### 1. **Introduction to Greedy Algorithms**
   - Definition and properties:
     - Local vs. global optima.
     - Greedy-choice property.
     - Optimal substructure.
   - When greedy algorithms work:
     - Problems with specific constraints or structures.

---

## Getting Started

### Prerequisites
- Ensure Python (>= 3.8) is installed.
- Familiarity with basic programming constructs like loops, lists, and sorting.
- Review of sorting algorithms (e.g., merge sort, quick sort).

### Files Provided
1. `greedy_algorithms.py` - A template file to implement greedy algorithms.
2. `sample_input.txt` - Input examples for testing.
3. `README.md` - This instruction file.

---

## Tasks

### Task 1: Implement a Greedy Algorithm Template
1. Open `greedy_algorithms.py`.
2. Implement a generic function template:
   ```python
   def greedy_algorithm(problem_instance):
       # Define the selection criteria.
       # Perform the selection iteratively.
       # Construct the solution incrementally.
       return solution
   ```

---

### Task 2: Classic Greedy Problems

#### 2.1: **Activity Selection Problem**
- **Problem**: Given `n` activities with start and finish times, select the maximum number of non-overlapping activities.
- **Input**: A list of tuples `(start, finish)` for each activity.
- **Output**: A list of selected activities.

- **Steps**:
  1. Sort activities by their finish times.
  2. Select the first activity.
  3. Iterate through the remaining activities, selecting only those that do not overlap.

- **Example**:
  ```python
  activities = [(1, 4), (3, 5), (0, 6), (5, 7), (8, 9)]
  result = activity_selection(activities)
  print("Selected activities:", result)
  ```

---

#### 2.2: **Huffman Coding**
- **Problem**: Construct a binary tree to encode characters with variable-length binary strings based on their frequencies.
- **Input**: A list of character-frequency pairs.
- **Output**: A dictionary mapping each character to its binary code.

- **Steps**:
  1. Use a priority queue (min-heap) to iteratively merge the two smallest frequencies.
  2. Construct the binary tree.
  3. Traverse the tree to generate codes.

- **Example**:
  ```python
  frequencies = {'a': 5, 'b': 9, 'c': 12, 'd': 13, 'e': 16, 'f': 45}
  codes = huffman_coding(frequencies)
  print("Huffman Codes:", codes)
  ```

---

#### 2.3: **Fractional Knapsack Problem**
- **Problem**: Given items with weights and values, maximize the value of items in a knapsack with a weight limit. Fractional items are allowed.
- **Input**: Lists of values, weights, and a knapsack weight limit.
- **Output**: Maximum value and the fractions of items included.

- **Steps**:
  1. Calculate the value-to-weight ratio for each item.
  2. Sort items by the ratio in descending order.
  3. Fill the knapsack greedily by selecting items or fractions of items.

- **Example**:
  ```python
  values = [60, 100, 120]
  weights = [10, 20, 30]
  capacity = 50
  result = fractional_knapsack(values, weights, capacity)
  print("Maximum value:", result)
  ```

---

### Task 3: Analyze Greedy Algorithm Properties
1. For each problem, explain:
   - Why the greedy approach works.
   - How the greedy-choice property and optimal substructure apply.
   - Any limitations of the approach.

2. Example for the **Activity Selection Problem**:
   - **Greedy-choice property**: Always select the activity that finishes the earliest, as it leaves the most room for other activities.
   - **Optimal substructure**: The problem reduces to smaller subproblems after selecting an activity.

---

### Bonus Task: Coin Change Problem
- **Problem**: Find the minimum number of coins needed to make a given amount using denominations `[d1, d2, ..., dn]`.
- **Input**: A list of coin denominations and a target amount.
- **Output**: The number of coins and their denominations.

- **Steps**:
  1. Sort denominations in descending order.
  2. Use the largest denomination repeatedly until the amount is exhausted.
  3. If no solution exists, print an error message.

- **Example**:
  ```python
  denominations = [1, 5, 10, 25]
  amount = 63
  result = coin_change(denominations, amount)
  print("Coins used:", result)
  ```

---

## Submission Instructions
1. Save your implementation in `greedy_algorithms.py`.
2. Include your analysis of greedy algorithm properties in a file named `analysis.txt`.
3. Attach any visualizations or additional test cases in a separate folder.
4. Submit all files on Canvas by the deadline.

---

## Additional Resources
- [Greedy Algorithm Paradigm](https://en.wikipedia.org/wiki/Greedy_algorithm)
- [Huffman Coding Algorithm](https://www.geeksforgeeks.org/greedy-algorithms-set-3-huffman-coding/)
- [Fractional Knapsack Problem](https://www.geeksforgeeks.org/fractional-knapsack-problem/)

---

## Notes
- Test each function with multiple test cases, including edge cases.
- Include comments in your code explaining your logic and time complexity.
- Reach out to the TA or instructor for any clarifications.
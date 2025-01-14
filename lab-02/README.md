# Lab 02: Algorithm Analysis

## Overview
Welcome to **Lab 02: Algorithm Analysis** of COMP 3010! This lab focuses on understanding the basics of algorithm analysis, including runtime complexity (Big-O notation), space complexity, and empirical testing. You will analyze and compare the efficiency of different algorithms using Python.

---

## Learning Objectives
By the end of this lab, you will be able to:
1. Understand and describe the **time complexity** and **space complexity** of algorithms.
2. Use **Big-O notation** to express algorithmic efficiency.
3. Compare algorithms both theoretically and empirically through Python implementation.
4. Visualize and interpret the results of algorithm analysis using basic plotting techniques.

---

## Lab Outline

### 1. **Introduction to Algorithm Analysis**
   - Review of **asymptotic notation**: Big-O, Omega (Ω), and Theta (Θ).
   - Examples of common time complexities:
     - Constant: $O(1)$
     - Logarithmic: $O(\log n)$
     - Linear: $O(n)$
     - Quadratic: $O(n^2)$
     - Exponential: $O(2^n)$
   - Understanding **best-case**, **average-case**, and **worst-case** scenarios.

### 2. **Runtime Complexity Analysis**
   - Analyzing simple iterative and recursive algorithms.
   - Measuring the runtime of Python functions using the `time` module.

### 3. **Space Complexity**
   - Identifying memory usage for variables, arrays, and function calls.
   - Examples of space complexity in iterative vs. recursive algorithms.

### 4. **Empirical Analysis**
   - Writing Python code to measure the performance of algorithms.
   - Plotting runtime comparisons using libraries like `matplotlib`.

---

## Getting Started

### Prerequisites
- Ensure Python (>= 3.8) and `matplotlib` are installed on your system.
  ```bash
  pip install matplotlib
  ```
- A code editor such as VSCode, PyCharm, or Jupyter Notebook is recommended.

### Files Provided
1. `algorithm_analysis.py` - A template file for implementing and analyzing algorithms.
2. `README.md` - This instruction file.
3. `example_data.txt` - Sample input data for testing.

---

## Task 1: Analyze Basic Algorithms

### Task 1.1: Linear Search
1. Open `algorithm_analysis.py` and locate the `linear_search(arr, target)` function.
2. Implement the algorithm:
   - Input: A list `arr` and a target value `target`.
   - Output: The index of the target value if found, otherwise `-1`.
3. Analyze the time complexity of this algorithm in the worst-case scenario.

### Task 1.2: Binary Search
1. Locate the `binary_search(arr, target)` function in the same file.
2. Implement the algorithm:
   - Input: A sorted list `arr` and a target value `target`.
   - Output: The index of the target value if found, otherwise `-1`.
3. Analyze the time complexity of binary search and compare it to linear search.

---

## Task 2: Compare Iterative vs. Recursive Algorithms

### Task 2.1: Factorial Calculation
1. Implement the factorial function using:
   - Iteration (`factorial_iterative(n)`).
   - Recursion (`factorial_recursive(n)`).
2. Analyze and compare the runtime and space complexity of both implementations.

### Task 2.2: Fibonacci Sequence
1. Implement the Fibonacci sequence calculation using:
   - Recursion (`fibonacci_recursive(n)`).
   - Dynamic programming (`fibonacci_dp(n)`).
2. Compare the efficiency of the recursive approach vs. the dynamic programming approach.

---

## Task 3: Empirical Analysis and Visualization

### Task 3.1: Measure Runtime
1. Use the `time` module to measure the runtime of your algorithms with varying input sizes.
2. Write a function `measure_runtime(func, *args)` that takes an algorithm and its arguments, then returns the time it takes to execute.

### Task 3.2: Plot Runtime
1. Use `matplotlib` to plot the runtime of different algorithms.
   - Example: Plot the runtime of linear search vs. binary search for input sizes ranging from 1000 to 100000.
2. Include appropriate labels, legends, and titles in your plot.

---

## Sample Code

### Example: Measuring and Plotting Runtime
```python
import time
import matplotlib.pyplot as plt

def measure_runtime(func, *args):
    start_time = time.time()
    func(*args)
    return time.time() - start_time

def example_plot():
    sizes = [10**i for i in range(1, 6)]
    runtimes = []

    for size in sizes:
        arr = list(range(size))
        runtimes.append(measure_runtime(linear_search, arr, size - 1))
    
    plt.plot(sizes, runtimes, label="Linear Search")
    plt.xlabel("Input Size")
    plt.ylabel("Runtime (s)")
    plt.title("Algorithm Runtime Analysis")
    plt.legend()
    plt.show()
```

---

## Submission Instructions
1. Save your implementation in `algorithm_analysis.py`.
2. Include plots and runtime results in a file named `runtime_analysis.pdf`.
3. Submit your files on Canvas by the deadline.

---

## Additional Resources
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)
- Python documentation: [https://docs.python.org/3/](https://docs.python.org/3/)
- `matplotlib` documentation: [https://matplotlib.org/](https://matplotlib.org/)

---

## Notes
- Test your algorithms with a range of input sizes to ensure correctness and efficiency.
- Add comments to your code to explain the time and space complexity of each function.
- Reach out to the TA if you encounter any issues.
## Project: Analysis of the Deterministic QuickSelect Algorithm (Θ(n)) 📊

### 1. Overview

This project presents a **rigorous asymptotic time complexity analysis** of the **Deterministic QuickSelect (Median of Medians)** algorithm for finding the k-th smallest element in an unordered list. The primary goal is to prove its time complexity through both theoretical derivation and experimental simulation.

The analysis conclusively demonstrates that the algorithm's performance scales **linearly** with the input size $n$, placing it firmly in the **Theta $\Theta(n)$** complexity class, a significant improvement over the average-case $\Theta(n)$ and worst-case $\Theta(n^2)$ of the standard QuickSelect algorithm.

***

### 2. Theoretical Analysis: Why $\Theta(n)$?

The power of the Deterministic QuickSelect algorithm lies in its clever pivot selection strategy, which guarantees a "good" partition in the worst case. This avoids the quadratic runtime that plagues simpler selection algorithms. The process follows a recursive structure:

1.  **Divide:** The input array of size $n$ is divided into $\lfloor n/5 \rfloor$ groups of 5 elements each (and one optional group with the remaining $n \pmod 5$ elements).
2.  **Conquer (Medians):** The median of each 5-element group is found. This results in a new list of $\lceil n/5 \rceil$ medians.
3.  **Conquer (Pivot Selection):** The algorithm recursively calls itself to find the true median of the list of medians. This median-of-medians is chosen as the pivot.
4.  **Partition:** The original array is partitioned around this pivot.
5.  **Recurse:** The algorithm makes a final recursive call on the subarray that is guaranteed to contain the k-th element.

This pivot selection guarantees that the next recursive call will be on an array of size at most $\approx \frac{7n}{10}$. This leads to the recurrence relation:

$$T(n) \le T(\lceil n/5 \rceil) + T(7n/10) + O(n)$$

This recurrence, unlike the one for standard QuickSelect, mathematically solves to a linear time complexity. Therefore, the total operation count $T(n)$ is:

$$\mathbf{T(n) = \Theta(n)}$$

The experimental data confirms this: the operation count $T(n)$ is directly proportional to the input size $n$, meaning $T(n) \approx C \cdot n$, where $C$ is a constant factor.

***

### 3. Execution and Results

The full simulation, analysis tables, and corresponding plots are available in the provided Google Colab notebook.

#### **Execute the Project**

Click the button below to open and run the complete Python code:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1LTx9zE6L50qyyLV4Rvwp1sRwyZl6DrEM?usp=sharing)

#### **Expected Outputs**

1.  **Analysis Table:** Shows the exact operation count $T(n)$ versus the input size $n$, clearly demonstrating the linear relationship between the two and calculating the **Scaling Constant ($C$)**.
2.  **Simulation Data:** Presents data for large inputs (e.g., up to $n=10^7$) to confirm the stability of the $\Theta(n)$ behavior as $n \to \infty$.
3.  **Plots:** Visual confirmation that both the Operation Count ($T(n)$) and the Execution Time are **linear** functions of the input size $n$.

***

### 4. Code Structure

| Section | Code Component | Description |
| :--- | :--- | :--- |
| **Algorithm** | `deterministic_quickselect(arr, k)` | The main function under test. Returns the k-th smallest element. |
| **Analysis** | `generate_analysis_table()` | Generates a table comparing the measured operation count $T(n)$ to the theoretical $C \cdot n$. |
| **Simulation** | `run_large_scale_simulation()` | Executes the algorithm for large $n$ to gather asymptotic performance data. |
| **Visualization** | `plot_complexity(df)` | Uses `seaborn` and `matplotlib` to plot $T(n)$ vs. $n$, showing a straight-line relationship. |

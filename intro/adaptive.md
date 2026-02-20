# Adaptive Sorting Strategy

## Objective
The objective of this assignment is to analyze how input order affects sorting algorithm performance and to apply that analysis to make an adaptive algorithmic decision. 

---

The following are the O(N) notations of the following sorting algorithms.

|                | Best case | Average case | Worst case |
| -------------- | --------- | ------------ | ---------- |
| Selection sort | $N^2$       | $N^2$          | $N^2$        |
| Insertion sort | N           | $N^2$          | $N^2$        |

## Part A: Adaptive Sorting Selection

1. Create an array of **50 integers**.
2. Implement both sorting algorithms:
   - **Selection Sort**
   - **Insertion Sort**

3. Your program must analyze the initial ordering of the array and determine which scenario it represents (best, average, or worst) based on a **clearly defined threshold** that you assume.

4. Based on your analysis, your program should automatically choose the more appropriate sorting algorithm.

### Example:

- If the array is **already sorted in ascending order** (or nearly sorted based on your defined threshold), your program should choose **Insertion Sort**, since Insertion Sort runs in linear time `O(n)` in the best case, whereas Selection Sort still performs $O(n^2)$ comparisons regardless of input order.

- If the array is in **strictly descending order** and the goal is to sort in ascending order, your program may decide to use **Selection Sort**, assuming under your defined threshold that it performs more consistently than Insertion Sort in this scenario.

Your decision logic must be clearly implemented in your code.

---

## Part B: Case Classification Without Sorting

Using the same threshold defined in Part A:

1. The user will input 50 integers.
2. Without actually sorting the array, your program must analyze the order of elements.
3. The program should classify the input as:
   - **Average Case**
   - **Worst Case**

The program must then display the classification result.

> No sorting should be performed in this part; only classification is required.

---

## Part C: Documentation

Provide a written explanation that includes:

- The **threshold definition** you used to differentiate between best, average, and worst cases.
- The reasoning behind your assumption.
- Why your program selects one sorting algorithm over the other in specific scenarios.
- A brief discussion of how input order affects the time complexity of Selection Sort and Insertion Sort.

Your explanation should demonstrate a clear understanding of algorithmic behavior and time complexity analysis.

---

### Submit your work on GitHub as a single Markdown file and share the repository link. Use clear and appropriate headings to organize your content.

---

# Grading Rubric (Total: 10 Points)

| Criteria | Points |
|----------|--------|
| Correct implementation of **Selection Sort** | 2 |
| Correct implementation of **Insertion Sort** | 2 |
| Proper logic to analyze array order and select appropriate algorithm (Part A) | 2 |
| Correct classification of Average/Worst case without sorting | 1 |
| Clear and reasonable threshold definition | 1 |
| Quality of documentation and explanation of time complexity | 2 |


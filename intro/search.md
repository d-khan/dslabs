# Linear and binary search

## Objective
Understand the working of linear and binary search algorithms

## Pre-requisite
Review "Searching and Big O Notations" from the book [Data Structures in C++](https://d-khan.github.io/ds)

## Task
1. How many steps would it take to perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13]? - **1 pt**

2. How many steps would binary search take for the previous example? - **1 pt**

3. What is the maximum number of steps it would take to perform a binary search on an array of size 100,000? - **1 pt**

4. Write a C++ program that implements both linear search and binary search algorithms using an array of 100,000 elements. The program should record and report the number of steps (comparisons) performed during each search operation. In addition, analyze and justify the observed behavior by providing a theoretical explanation using Big-O notation, demonstrating why linear search exhibits $O(N)$ complexity and binary search exhibits $O(\log N)$ complexity. - **2 pts**

5.
Write pseudocode for a randomized search algorithm that searches for a given key by randomly selecting indices __without repetition__. Use a dataset of 100,000 distinct elements, stored in a vector. Each element may be examined __at most__ once during the search. Analyze and state the best-case, average-case, and worst-case time complexities of this algorithm using Big-O notation.

Then, implement the algorithm in C++, using only the following standard headers: ```<vector>``` for data storage, ```<random>``` for random index generation, and ```<iostream>``` for input and output. The implementation should track and report the number of comparisons performed during the search.

Finally, compare and contrast the randomized search algorithm with linear search and binary search in terms of time complexity, data requirements (such as ordering), and practical efficiency. Discuss scenarios in which each approach may be preferred, highlighting the advantages and limitations of randomized search relative to linear and binary search. - **5 pts**

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://www.youtube.com/watch?v=zjY-L71A9PE)” before submission.
- Create a video explaining the functionality of your code along with your explanations. The video should also display your face on one side of the screen, preferably in the top-right or bottom-right corner. Video is mandatory for the entire assignment.

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric for question 4
| **Criteria**                 | **Description**                                              | **Points** |
| ---------------------------- | ------------------------------------------------------------ | ---------- |
| **Algorithm Implementation** | Correct implementation of both linear search and binary search on an array of 100,000 elements, including accurate step (comparison) counting | 1.0        |
| **Complexity Analysis**      | Clear and correct theoretical justification using Big-O notation, explaining why linear search is O(N) and binary search is O(\log N) | 1.0        |

## Rubric for question 5
| **Criteria**                      | **Description**                                              | **Points** |
| --------------------------------- | ------------------------------------------------------------ | ---------- |
| **Pseudocode Correctness**        | Pseudocode clearly describes a randomized search without repetition and ensures each element is examined at most once | 1.0        |
| **Time Complexity Analysis**      | Correct identification and explanation of best-, average-, and worst-case complexities using Big-O notation | 1.0        |
| **C++ Implementation**            | Working C++ implementation that correctly follows the pseudocode and problem constraints | 1.0        |
| **Constraint Compliance**         | Uses a vector of 100,000 elements and only the required headers (<vector>, <random>, <iostream>) | 1.0        |
| **Comparison with Linear Search** | Accurate comparison in terms of time complexity, data requirements, and efficiency | 0.5        |
| **Comparison with Binary Search** | Accurate comparison, including ordering requirements and practical implications |     0.5       |

## Note
Only one submission attempt is permitted for this lab. Students are not allowed to submit draft versions or request feedback for evaluation prior to the final submission. Please ensure that your work is complete, correct, and well-documented before submitting.

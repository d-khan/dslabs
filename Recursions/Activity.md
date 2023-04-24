# Recursions

## Objective
Implement recursions in C++

## Pre-requisite
Review [Recursions](https://htmlpreview.github.io/?https://github.com/d-khan/dslabs/blob/main/Recursions/Lecture.html) lecture.

## Tasks
1. The following function prints every other number from a low number to a high number. For example, if low is 0 and high is 10, it would print:
```
0
2
4
6
8
10
```
Identify the base case in the function:
```
def print_every_other(low, high) 
    return if low > high
    puts low
    print_every_other(low + 2, high)
end
```
2. My kid was playing with my computer and changed my factorial function so that it computes factorial based on (n - 2) instead of (n - 1). Predict what will happen when we run factorial(10) using this function:

```
def factorial(n)
    return 1 if n == 1
    return n * factorial(n - 2)
end
```
3. Following is a function in which we pass in two numbers called low and high. The function returns the sum of all the numbers from low to high. For example, if low is 1, and high is 10, the function will return the sum of all numbers from 1 to 10, which is 55. However, our code is missing the base case, and will run indefinitely! Fix the code by adding the correct base case:
```
def sum(low, high)
    return high + sum(low, high - 1)
end
```
4. Here is an array containing both numbers as well as other arrays, which in turn contain numbers and arrays:
```
array=[ 1, 2, 3,
               [4, 5, 6],
               7,
               [8,
                 [9, 10, 11,
                   [12, 13, 14]
] ],
               [15, 16, 17, 18, 19,
                 [20, 21, 22,
                   [23, 24, 25,
                     [26, 27, 29]
], 30, 31 ], 32
], 33 ]
```
Write a recursive function that prints all the numbers (and just numbers).

## What to submit?  

- All the explanations are saved in .txt format and uploaded in Canvas.
- Create a video that explains your solution. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). 

## How to submit it?
- Upload your work in Canvas. Remember .txt file formats are for narrative-based responses, and .cpp is for C++ code. Clearly define task numbers. __Do not compress files. Do not zip. Use mp4 format for the videos__

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the solution in detail. (10 marks).  
- The video is submitted, but the questions are partially explained. (Marks based on what you have submitted).  
- The video is not submitted, regardless of whether the solutions are submitted. (0 marks)



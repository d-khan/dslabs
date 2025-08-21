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
array=[ 1, 
        2, 
        3,
        [4, 5, 6],
        7,
        [8,
          [9, 10, 11,
            [12, 13, 14]
          ] 
        ],
        [15, 16, 17, 18, 19,
          [20, 21, 22,
            [23, 24, 25,
              [26, 27, 29]
            ], 30, 31 
          ], 32
        ], 33 
      ]
```
Write a recursive function that prints all the numbers (and just numbers).

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://sdccd-edu.zoom.us/rec/play/SVjSkOJp16n_7ii-oRt1-9auud9NZ0NrhuXrnJYf-bcQP5ipZbGONd6Jxt7h1jns5OJKIq9lgjAuBw.Tc2b6f-qrSDM8aye?eagerLoadZvaPages=sidemenu.billing.plan_management&accessLevel=meeting&canPlayFromShare=true&from=share_recording_detail&startTime=1725121532000&componentName=rec-play&originRequestUrl=https%3A%2F%2Fsdccd-edu.zoom.us%2Frec%2Fshare%2FSVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX%3FstartTime%3D1725121532000)” before submission.
- Create a video explaining the functionality of your code along with your explanations. The video should also display your face on one side of the screen, preferably in the top-right or bottom-right corner. 

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- All questions contain equal marks.
- The code is submitted with no errors, and all questions are answered correctly. (10 marks).  
- The code is submitted and the questions are partially explained. (Marks based on the correct answers and the code). 



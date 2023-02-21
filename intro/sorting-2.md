# Sorting algorithms

## Objective
Understand the working of insertion sort algorithm algorithms and evaluate the algorithm's efficiency.

## Pre-requisite
Review "Sorting algorithms" from the book [Data Structures in C++](https://d-khan.github.io/ds)

## Task
1. Proof that, under the average-case scenario, the insertion sort has a time complexity of 
   $$
   O(N^2)
   $$
   ​																																									**2 pts **

2. At the start of the insertion sort, the index of the inspected value is set to 1. Change the index of the inspected value and verify that the total number of operations equals 20. Consider the worst-case scenario. Use N=5, where N is the number of elements.  **4 its**

3. The following function returns whether or not a capital “X” is present within a string. - **4 pt**

```
function containsX(string) {
	foundX = false;
	for(let i = 0; i < string.length; i++) { 
		if (string[i] === "X") {
			foundX = true; 
		}
	}
	return foundX; 
}
```

(a) What is this function’s time complexity regarding Big O Notation?

(b) Then, modify the code to improve the algorithm’s efficiency for best- and average-case scenarios.

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

# Sorting algorithms

## Objective
Understand the working of insertion sort algorithm algorithms and evaluate the algorithm's efficiency.

## Pre-requisite
Review "Sorting algorithms" from the book [Data Structures in C++](https://d-khan.github.io/ds)

## Task
1. Proof that, under the average-case scenario, the insertion sort has a time complexity of $O(N^2)$. Draw a clear figure and show all the operations clearly.  **2 pts **

2. At the start of the insertion sort, the index of the inspected value is set to 1. Change the index of the inspected value and verify that the total number of operations equals 20. Consider the worst-case scenario. Use N=5, where N is the number of elements.  **4 pts**

3. The following function returns whether or not a capital “X” is present within a string.  **4 pt**

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

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://sdccd-edu.zoom.us/rec/play/SVjSkOJp16n_7ii-oRt1-9auud9NZ0NrhuXrnJYf-bcQP5ipZbGONd6Jxt7h1jns5OJKIq9lgjAuBw.Tc2b6f-qrSDM8aye?eagerLoadZvaPages=sidemenu.billing.plan_management&accessLevel=meeting&canPlayFromShare=true&from=share_recording_detail&startTime=1725121532000&componentName=rec-play&originRequestUrl=https%3A%2F%2Fsdccd-edu.zoom.us%2Frec%2Fshare%2FSVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX%3FstartTime%3D1725121532000)” before submission.
- Create a video explaining the functionality of your code along with your explanations. The video should also display your face on one side of the screen, preferably in the top-right or bottom-right corner. 

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the solution in detail. (10 marks).  
- The video is submitted, but the questions are partially explained. (Marks based on what you have submitted).  
- The video is not submitted, regardless of whether the solutions are submitted. (0 marks)

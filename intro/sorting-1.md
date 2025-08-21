# Sorting algorithms

## Objective
Understand the working of sorting algorithms and evaluate the efficiency of the algorithm

## Pre-requisite
Review "Sorting algorithms" from the book [Data Structures in C++](https://d-khan.github.io/ds)

## Task
1. Use Big O Notation to describe the time complexity of an algorithm that takes $4N + 16 steps.$- **1 pt**
2. Use Big O Notation to describe the time complexity of an algorithm that takes $2N^2$. **1 pt**
3. Use Big O Notation to describe the time complexity of the following function, which returns the sum of all numbers of an array after the numbers have been doubled: - **2 pt**
```
def double_then_sum(array) 
	doubled_array = []

	array.each do |number| 
		doubled_array << number *= 2
	end

	sum = 0

	doubled_array.each do |number| 
		sum += number
	end
	return sum 
end

```

4. Use Big O Notation to describe the time complexity of the following function, which accepts an array of strings and prints each string in multiple cases: - **2 pts**
```
def multiple_cases(array) 
	array.each do |string|
		puts string.upcase 
		puts string.downcase 
		puts string.capitalize
	end 
end
```

5. The next function iterates over an array of numbers, and for each number whose index is even, it prints the sum of that number plus every number in the array. What is this function’s efficiency in terms of Big O Notation? - **4 pts**
```
def every_other(array) 
	array.each_with_index do |number, index|
		if index.even?
			array.each do |other_number|
            	puts number + other_number
			end 
		end
	end 
end
```

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://sdccd-edu.zoom.us/rec/play/SVjSkOJp16n_7ii-oRt1-9auud9NZ0NrhuXrnJYf-bcQP5ipZbGONd6Jxt7h1jns5OJKIq9lgjAuBw.Tc2b6f-qrSDM8aye?eagerLoadZvaPages=sidemenu.billing.plan_management&accessLevel=meeting&canPlayFromShare=true&from=share_recording_detail&startTime=1725121532000&componentName=rec-play&originRequestUrl=https%3A%2F%2Fsdccd-edu.zoom.us%2Frec%2Fshare%2FSVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX%3FstartTime%3D1725121532000)” before submission.
- Create a video explaining the functionality of your code along with your explanations. The video should also display your face on one side of the screen, preferably in the top-right or bottom-right corner. 

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the solution in detail. (10 marks).  
- The video is submitted, but a partial explanation of the questions is submitted. (Marks based on what you have submitted).  
- The video is not submitted regardless of the solutions are submitted or not. (0 marks)

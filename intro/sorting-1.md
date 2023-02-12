# Sorting algorithms

## Objective
Understand the working of sorting algorithms and evaluate algorithm efficiency

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

5. The next function iterates over an array of numbers, and for each number whose index is even, it prints the sum of that number plus every number in the array. What is this function’s efficiency in terms of Big O Notation? - **2 pts**
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

## What to submit?  
- All the explanation are saved as .txt format and upload in Canvas.
- Code related responses are saved as .cpp and upload in Canvas.
- Create a video that explains the working of the code and your explanations. Furthermore, the video should show your face on one side of the screen (preferably the top or bottom right of the screen). 

## How to submit it?
- Upload your work in Canvas. Remember .txt file formats are for narative based responses and .cpp is for C++ code. Clearly define task numbers.  

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The video describes the code in detail. The code is working as per instruction, and the explanations of the questions are submitted (10 marks).  
- The video is submitted, and the code is working, but a partial explanation of the questions is submitted. (7+ marks).  
- The code is uploaded but not working regardless the video is submitted or not. (0 marks)

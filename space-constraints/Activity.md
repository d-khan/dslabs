# Space constraints

## Objective
How to write a space-efficient code	

## Pre-requisite
Review [Constraints](https://github.com/d-khan/dslabs/blob/main/space-constraints/Lecture.md) lecture.

## Tasks
The following exercises provide you with the opportunity to practice with space constraints.

1. Following is the 'Word Builder' algorithm. Describe its space complexity in terms of Big O.

```
function wordBuilder(array) { 
		let collection = [];
		for(let i = 0; i < array.length; i++) { 
				for(let j = 0; j < array.length; j++) {
						if (i !== j) {
								collection.push(array[i] + array[j]);
						}
				}
		}
		return collection; 
}
```

2. Following is a function that reverses an array. Describe its *space* complexity in terms of Big O:

```
function reverse(array) { 
		let newArray = [];
		for (let i = array.length - 1; i >= 0; i--) { 
				newArray.push(array[i]);
		}
		return newArray;
}
```

3. Create a new function to reverse an array that takes up just $O(1)$ extra space.
4. Following are three different implementations of a function that accepts an array of numbers and returns an array containing those numbers multiplied by 2. For example, if the input is [5, 4, 3, 2, 1], the output will be [10, 8, 6, 4, 2].

````
function doubleArray1(array) { 
	let newArray = [];

	for(let i = 0; i < array.length; i++) { 
		newArray.push(array[i] * 2);
	}
	return newArray; 
}


function doubleArray2(array) {
	for(let i = 0; i < array.length; i++) {
  	array[i] *= 2;
  }
	return array; 
}


function doubleArray3(array, index=0) { 
	if (index >= array.length) { return; }
  array[index] *= 2;
  doubleArray3(array, index + 1);
	return array; 
}
````

Fill in the table that follows to describe the efficiency of these three versions in terms of both time and space:

| Version    | Time complexity | Space complexity |
| ---------- | --------------- | ---------------- |
| Version #1 | ?               | ?                |
| Version #2 | ?               | ?                |
| Version #3 | ?               | ?                |

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**.  

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

## Rubric
- The solution is explained in detail. (10 marks)
- The solution is submitted, but the explanation is partial. (Marks based on what you have submitted)
- The solution is not submitted. (0 marks)

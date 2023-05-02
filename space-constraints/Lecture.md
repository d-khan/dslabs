# Space constraints

When analyzing the efficiency of various algorithms throughout this course, we have focused exclusively on how fast they run—their time complexity. However, another efficiency measure can also be useful: how much *memory* an algorithm consumes. This measure is known as *space complexity.*

Space complexity becomes an important factor when memory is limited. If you have an enormous amount of data, or are programming for a small device with limited memory, space complexity can matter a lot.

In a perfect world, we would always use fast and memory-efficient algorithms. However, there are times when we can’t have both, and we need to choose between the two. Each situation requires a careful analysis to know when we need to prioritize speed over memory and memory over speed.

## Big O of space complexity

Computer scientists use Big O Notation to describe space complexity just as they do for time complexity. When I introduced Big O Notation, I described Big O in terms of what I called the “key question.” For time complexity, the key question was: *if there are N data elements, how many steps will the algorithm take?*

To use Big O for space complexity, we just need to reframe the key question. When it comes to memory consumption, the key question is: *if there are N data elements, how many units of memory will the algorithm consume?*

Here’s a simple example.

Let’s say we’re writing a function that accepts an array of strings and returns an array of those strings in ALL CAPS. For example, the function would accept an array like ["tuvi", "leah", "shaya", "rami"] and return ["TUVI", "LEAH", "SHAYA", "RAMI"]. Here’s one way we can write this function:

```javascript
//Version 1
function makeUppercase(array) {
let newArray = [];
for(let i = 0; i < array.length; i++) {
    newArray[i] = array[i].toUpperCase();
  }
return newArray; }
```

In this makeUpperCase() function, we accept an array. We then create a *brand- new array* called newArray and fill it with uppercase versions of each string from the original array.

By the time this function is complete, we will have two arrays floating around in our computer’s memory. We have the original array, which contains ["tuvi", "leah", "shaya", "rami"], and we have newArray, which contains ["TUVI", "LEAH", "SHAYA", "RAMI"].

When we analyze this function in terms of space complexity, we can see that this function *creates* a brand-new array that contains N elements. This is *in addition* to the original array which also held N elements.

So, let’s return to our key question: *if there are N data elements, how many units of memory will the algorithm consume?*

Because our function generated an additional N data elements (in the form of newArray), we’d say that this function has a *space efficiency of $O(N)$.*

Now, let’s present an alternative makeUppercase() function that is more memory- efficient:

``` javascript
// Version 2
function makeUppercase(array) {
for(let i = 0; i < array.length; i++) {
    array[i] = array[i].toUpperCase();
  }
return array; }
```

In this second version, we do not create any new arrays. Instead, we modify each string within the original array *in place,* transforming them into uppercase one at a time. We then return the modified array.

This is a drastic improvement in terms of memory consumption, since our new function doesn't consume any additional memory at all.

How do we describe this in terms of Big O Notation?

Recall that with time complexity, an $O(1)$ algorithm was one whose speed remained constant no matter how large the data. Similarly, with space complexity, $O(1)$ means that the memory consumed by an algorithm is constant no matter how large the data.

Our revised makeUppercase function consumes a constant amount of additional space (zero!) no matter whether the original array contains four elements or one hundred. Because of this, this function is said to have a space efficiency of $O(1)$.

It’s worth emphasizing that when using Big O to describe space complexity, we’re only counting the *new data* the algorithm is generating. Even our second makeUppercase function deals with N elements of data in the form of the array passed into the function. However, we’re not factoring those N elements into our Big O description, since the original array exists in any case, and we’re only focused on the *extra* space the algorithm consumes. This extra space is more formally known as *auxiliary space.*

However, it’s good to know that there are some references that include the original input when calculating the space complexity, and that’s fine. We’re not including it, and whenever you see space complexity described in another resource, you need to determine whether it’s including the original input.

Let’s now compare the two versions of makeUppercase() in both time and space complexity:

| Version   | Time complexity | Space complexity |
| --------- | --------------- | ---------------- |
| Version 1 | $O(N)$          | $O(N)$           |
| Version 2 | $O(N)$          | $O(1)$           |

Both versions are $O(N)$ in time complexity, since they take N steps for N data elements. However, the second version is more memory-efficient, as it is $O(1)$ in space complexity compared to the first version’s O(N).

It turns out that Version #2 is more efficient than Version #1 in terms of space while not sacrificing any speed, which is a nice win.

## Trade-offs between Time and Space

Here’s a function that accepts an array and returns whether it contains any duplicate values.

```
function hasDuplicateValue(array) {
	for(let i = 0; i < array.length; i++) {
		for(let j = 0; j < array.length; j++) { 
			if(i !== j && array[i] === array[j]) {
				return true; 
			}
		} 	
	}
return false; 
}
```

This algorithm uses nested loops and has a time complexity of $O(N^2$). We’ll call this implementation Version #1.

Here’s a second implementation, Version #2, that employs a hash table and just a single loop:

```
function hasDuplicateValue(array) {
	let existingValues = {};
	for(let i = 0; i < array.length; i++) {
		if(!existingValues[array[i]]) { 
			existingValues[array[i]] = true;
		} else {
			return true;
		} 
	}
	return false; 
}
```

Version #2 starts out with an empty hash table called existingValues. We then iterate over each item from the array, and as we encounter each new item, we store it as a key in the existingValues hash table. (We set the value arbitrarily to true.) If, however, we encounter an item that is already a key the hash table, we return true, as it means we found a duplicate value.

Now, which of these two algorithms is more efficient? Well, it all matters whether you consider time or space. As far as time is concerned, Version #2 is much more efficient, as it’s only $O(N)$, compared with Version #1’s $O(N^2)$.

However, when it comes to *space,* Version #1 is actually more efficient than Version #2. Version #2 consumes up to $O(N)$ space, as it creates a hash table that may end up containing all N values from the array passed to the function. Version #1, however, does not consume any additional memory beyond the original array, and therefore has a space complexity of $O(1)$.

Let’s look at the complete contrast between the two versions of hasDuplicateValue():

| Version   | Time complexity | Space complexity |
| --------- | --------------- | ---------------- |
| Version 1 | $O(N^2)$        | $O(1)$           |
| Version 2 | $O(N)$          | $O(N)$           |

We can see that Version #1 more efficient when it comes to memory, but Version #2 is faster in terms of raw speed. So, how do we decide which algorithm to choose?

The answer, of course, is that it depends on the situation. If we need our application to be blazing fast and we have enough memory to handle it, then Version #2 might be preferable. If, on the other hand, we’re dealing with a hardware/data combination where we need to consume memory sparingly and speed isn’t our biggest need, then Version #1 might be the right choice. Like all technology decisions, when there are trade-offs, we need to look at the big picture.

Let’s look at a third version of this same function, and see where it falls compared to the first two versions:

```
function hasDuplicateValue(array) { 
	array.sort((a, b) => (a < b) ? -1 : 1);
		for(let i = 0; i < array.length - 1; i++) { 
			if (array[i] === array[i + 1]) {
				return true; 
			}
		}
		return false; 
}
```

This implementation, which we’ll call Version #3, begins by sorting the array. It then iterates over each value within the array and checks to see whether it’s the same as the next value. If it is, we’ve found a duplicate value. However, if we get to the end of the array and there are no two consecutive values that are the same, we know that the array contains no duplicates.

Let’s analyze the time and space efficiency of Version #3.

In terms of time complexity, this algorithm is $O(N log N)$. We can assume that sorting algorithm is one that takes $O(N log N)$, as the fastest known sorting algorithms are known to do. The additional N steps of iterating over the array are trivial beside the sorting steps, so $O(N log N)$ is the grand total when it comes to speed.

Space is a slightly more complex matter, as various sorting algorithms consume varying amounts of memory. Some of the earliest algorithms we’ve encountered in the course, like Bubble Sort and Selection Sort, consume no extra space because all the sorting happens in place. Interestingly, though, the faster sorts do take up some space for reasons you’ll see shortly. Most implementations of Quicksort actually take up $O(log N)$ space.

So, let’s see where Version #3 lands in comparison with the previous two versions:

| Version    | Time complexity | Space complexity |
| ---------- | --------------- | ---------------- |
| Version #1 | $O(N^2)$        | $O(1)$           |
| Version #2 | $O(N)$          | $O(N)$           |
| Version #3 | $O(NlogN)$      | $O(logN)$        |

It turns out Version #3 strikes an interesting balance between time and space. In terms of time, Version #3 is faster than Version #1, but slower than Version #2. When it comes to space, it’s more efficient than Version #2, but less effi- cient than Version #1.

So, when may we want to use Version #3? Well, if we’re concerned about both time *and* space, this might be our fix.

Ultimately, in each given situation, we need to know what our minimum acceptable speeds and bounds of memory are. Once we understand our constraints, we can then pick and choose from various algorithms so that we can take out acceptable efficiency for our speed and memory needs.

Up until this point, you’ve seen how our algorithms can consume extra space when they create additional pieces of data, such as new arrays or hash tables.

However, it’s possible for an algorithm to consume space even if it’s not doing any of those things. And this can come to bite us if we’re not expecting it.

## The hidden cost of recursion

Let’s look at a simple recursive function:

```python
def fun(n):
    if(n<0):return
    print(n)
    return fun(n-1)
```

This function accepts a number $n$ and counts down to 0, printing each decrementing number along the way.

It’s a pretty straightforward bit of recursion, and seems pretty harmless. Its speed is $O(N)$, as the function will run as many times as the argument $n$. And it doesn’t create any new data structures, so it doesn’t seem to take up any additional space.

You learned that each time a function recursively calls itself, an item is added to the call stack so that the computer can come back to the outer function once the inner function is complete.

If we pass the number 100 into our recurse function, it would add recurse(100) before proceeding to execute recurse(99). And it would then add recurse(99) to the call stack before executing recurse(98).

Now, even though the call stack will eventually get unwound, we do need enough memory to store these 100 items in our call stack in the first place. It emerges, then, that our recursive function *takes up O(N) space.* In this case, N is the number passed into the function; if we pass in the number 100, we need to temporarily store 100 function calls in the call stack.

An important principle emerges from all of this: *A recursive function takes up a unit of space for each recursive call it makes.* This is the sneaky way recursion can gobble up memory; even if our function does not explicitly create new data, the recursion itself adds data to the call stack.

To properly calculate how much space a recursive function takes, we always need to figure out how big the call stack would be at its peak.

For our recurse function, the call stack will be about as large as whatever number $n$ is.

At first, this may seem a bit trivial. After all, our modern computers can handle a few items on the call stack, right? 

When I pass in the number 20,000 into the recurse function on my sleek, up to-date laptop, *my computer cannot process it.* Now, 20,000 doesn’t seem like a very large number. But this is what happens when I run recurse(20000):

My computer prints the numbers from 20000 until 5387 and then terminates with the message:

```
RangeError: Maximum call stack size exceeded
```

Because the recursion lasted from 20000 until about 5000 (I’m rounding 5387 down), we can figure out that the call stack reached a size of about 15,000 when the computer ran out of memory. It turns out my computer will not tolerate a call stack that contains more than 15,000 items.

This is a *huge* limitation on recursion, as I can’t use my beautiful recurse function on a number much greater than 15,000!

Let’s contrast this to a simple loop approach:

```python
def loop(n):
    while (n>0):
        print(n)
        n=n-1
    return n
```

This function accomplishes the same goal using a basic loop instead of recursion.

Because this function does not use recursion, and does not take up any additional memory, it can run with huge number without *ever* causing the computer to run out of space. The function may take some time on huge numbers, but it’ll get the job done without giving up prematurely as the recursive function did.

With this in mind, we can now understand why Quicksort is said to take up $O(log N)$ space. Quicksort makes $O(log N)$ recursive calls, so at its peak, has a call stack that is the size of $log(N)$.

When we can implement a function using recursion, then, we need to weigh recursion’s benefits against its drawbacks. Recursion allows us to use the “magical” top-down mindset, but we also need our function to get the job done. And if we’r processing a lot of data, or even just a number like 20,000, recursion may not be suitable. Again, this isn’t to discredit recursion. It just means we need to weigh all the pros and cons of each algorithm in every situation.

## Conclusion

You’ve now learned how to measure the efficiency of our algorithms from all angles, including time *and* space. You are now armed with the analytical abilities to weigh each algorithm against the next and make informed decisions on which approach to use for our own applications.



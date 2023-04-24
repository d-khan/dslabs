# Recursions

Recursion is a key concept in computer science that will unlock the more advanced algorithms we will encounter in this section. When used correctly, recursion can be used to solve certain types of tricky problems in surprisingly simple ways. Sometimes, it even seems like magic.

But before we dive in, what happens when the example() function defined here is called?

```
function example() {
	function_body;
}
```

As you probably guessed, it will call itself infinitely since example() calls itself, which calls itself, and so on.

*Recursion* is the term for a function calling itself. Indeed, infinite recursion, as in the above example, is utterly useless. When harnessed correctly, though, recursion can be a powerful tool.

## Recurse or loop

Let’s say you work at NASA and need to program a countdown function for launching spacecraft. The function you’re asked to write should accept a number—such as 10—and display the numbers from 10 down to 0.

Take a moment and implement this function in the language of your choice. Then, when you’re done, read on.

The odds are that you wrote a simple loop based on the for keyword.

```c++
for (int i = 0; i < 5; i++) {
  cout << i << "\n";
}
```

There’s nothing wrong with this implementation, but it may have never occurred to you that you don’t *have* to use a loop. Let’s try recursion instead. Here’s a first attempt at using recursion to implement our countdown function

```
function countdown(number) {
	console.log(number);
	countdown(number-1);
}
```

Let’s walk through this code step by step.

Step 1: We call countdown(10), so the variable argument number starts as 10.

Step 2: We print the number (which contains the value 10) to the console.

Step 3: Before the countdown function is complete, it calls countdown(9) since number - 1 is 9.

Step 4: countdown(9) begins running. In it, we print the number (which is currently 9) to the console.

Step 5: Before countdown(9) is complete, it calls countdown(8).

Step 6: countdown(8) begins running. We print 8 to the console.

Before we continue stepping through the code, note how we’re using recursion to achieve our goal. We’re not using any loop constructs, but by simply having the countdown function call itself, we can count down from 10 and print each number to the console.

In almost any case where you can use a loop, you can also use recursion. Now, just because you *can* use recursion doesn’t mean that you *should* use recursion. Instead, recursion is a tool that allows for writing elegant code. In the preceding example, the recursive approach is not necessarily more beautiful or efficient than a classic for a loop. However, we will soon encounter examples in which recursion shines. In the meantime, let’s continue exploring how recursion works.

## The base case

Let’s continue our walk-through of the countdown function. We’ll skip a few steps for brevity...

Step 21: We call countdown(0).

Step 22: We print the number (that is, 0) to the console.

Step 23: We call countdown(-1).

Step 24: We print number (that is, -1) to the console.

Uh-oh. As you can see, our solution is not perfect, as we’ll end up infinitely printing negative numbers.

To perfect our solution, we need a way to end our countdown at 0 and prevent the recursion from continuing on forever.

We can solve this problem by adding a conditional statement that ensures that if the number is currently 0, we don’t call countdown() again:

```
function countdown(number) { 
		console.log(number); 
		if (number == 0) {
				return; 
		} else {
    		countdown(number - 1);
  }
}
```

Now, when the number is 0, our code will not call the countdown() function again but instead return, thereby preventing another call of countdown().

In recursion terminology, the case in which our function will *not* recurse is known as the *base case.* So, 0 is the base case for our countdown() function. Again, every recursive function needs at least one base case to prevent it from calling itself indefinitely.

## Reading recursive code

It takes time and practice to get used to recursion, and you will ultimately learn *two* sets of skills: *reading* recursive code, and *writing* recursive code. Reading recursive code is somewhat easier, so let’s get some practice with that first.

We’ll do this by looking at another example: calculating factorials. A *factorial* is best illustrated with some examples.

The factorial of 3 is:

3* 2* 1 = 6

The factorial of 5 is:

5 * 4 * 3 * 2 * 1 = 120

And so on and so forth. Here’s a recursive implementation that returns a number’s factorial using Python.

```python
def factorial(n):
    if (n==1):
        return 1
    else:
        return (n * factorial(n-1))
```

This code can look somewhat confusing at first glance. To walk through the code to see what it does, here’s the process I recommend:

1. Identify the base case.
2. Walk through the function for the base case.
3. Identify the “next-to-last” case. This is the case just before the base case, as I’ll demonstrate momentarily.
4. Walk through the function for the “next-to-last” case.
5. Repeat this process by identifying the case before the one you just analyzed and walking through the function for that case.

Let’s apply this process to the preceding code. If we analyze the code, we’ll quickly notice two paths: one path (line 3) leads to the end of the factorial function, and the other (line 5) calls for the factorial function itself. Lines 2-3 refer to the base case since this is the case in which the function does *not* call itself:

Let’s walk through the factorial method, assuming it deals with the base case, which would be factorial(1). Again, the relevant code from our method is:

```
if number == 1
		return 1
```

Well, that’s pretty simple—it’s the base case, so no recursion happens. If we call factorial(1), the method returns 1. Okay, so grab a piece of paper and write this fact down:

**factorial(1) returns 1**

Next, let’s move up to the next case, factorial(2). The relevant line of code from our method is:

``` python
else {
    		countdown(number - 1);
  }
```

So, calling factorial(2) will return 2 * factorial(1). To calculate 2 * factorial(1), we need to know what factorial(1) returns. If you check your paper, you’ll see that it returns 1. So, 2 * factorial(1) will return 2 * 1, which just happens to be 2.

Add this fact to your paper:

**factorial(2) returns 2**

**factorial(1) returns 1**

Now, what happens if we call factorial(3)? Again, the relevant line of code is the same as above.

So, that would translate into return 3 * factorial(2). What does factorial(2) return? You don’t have to figure that out again since it’s on your paper! It returns 2. So, factorial(3) will return 6 (because 3 * 2 = 6). Go ahead and add this fact to your paper.

**factorial(3) returns 6**

**factorial(2) returns 2**

**factorial(1) returns 1**

Take a moment and figure out what factorial(4) will return. As you can see, starting the analysis from the base case and building it up is a great way to reason about recursive code.

## Recursion in the eyes of the computer

To complete your understanding of recursion, we need to see how the computer itself processes a recursive function. It’s one thing for humans to reason about recursion using the earlier “napkin” method. However, the computer has to do the tricky work of calling a function from within the function itself. So, let’s break down how the computer executes a recursive function.

Say that we call factorial(3). Since 3 isn’t the base case, the computer reaches the line:

**return** number * factorial(number - 1) which launches the function factorial(2).

But there’s a catch. When the computer begins to run factorial(2), did the computer yet complete running factorial(3)?

This is what makes recursion tricky for the computer. Until the computer reaches the end keyword of factorial(3), it’s not done with factorial(3). So, we enter into a weird situation. The computer did not yet completed executing factorial(3), yet it’s starting to run factorial(2) while *still in the middle* of factorial(3).

And factorial(2) isn’t the end of the story, because factorial(2) triggers factorial(1). So, it’s a pretty crazy thing: while still in the middle of running factorial(3), the computer calls factorial(2). And while running factorial(2), the computer runs factorial (1). It turns out then, that factorial(1) runs in the middle of *both* factorial(2) and factorial(3).

How does the computer keep track of all of this? It needs some way to remember that after it finishes factorial(1), it needs to go back and finish running factorial(2). And then, it needs to remember to complete factorial(3) once it is completed factorial(2).

## The call stack

The computer uses a stack to keep track of which functions it’s in the middle of calling. This stack is known, appropriately enough, as the *call stack.* Here’s how the call stack works in the context of our factorial example. The computer begins by calling factorial(3). Before the method completes executing, however, factorial(2) gets called. To track that the computer is still in the middle of factorial(3), the computer pushes that information onto a call stack.

<img width="100" alt="image" src="https://user-images.githubusercontent.com/11669149/233851941-fa600133-d810-40f8-a950-77b2deb2b8a6.png">

This indicates that the computer is in the middle of factorial(3). (Really, the computer also needs to save which line it’s in the middle of, and some other things like variable values, but I’m keeping the diagrams simple.)

The computer then proceeds to execute factorial(2). Now, factorial(2), in turn, calls factorial(1). Before the computer dives into factorial(1), though, the computer needs to remember that it’s still in the middle of factorial(2), so it pushes that onto the call stack as well:

<img width="101" alt="image" src="https://user-images.githubusercontent.com/11669149/233851981-f6e6d9c9-2471-43a4-9b86-e912bcd8fc90.png">

The computer then executes factorial(1). Since 1 is the base case, factorial(1) completes without calling the factorial method again.

After the computer completes factorial(1), it checks the call stack to see whether it’s in the middle of any other functions. If there’s something in the call stack, the computer still has work to do, namely, wrap up some other functions it was in the middle of.

If you recall, stacks are restricted because we can only pop its top element. This is ideal for recursion since the top element will be *the most recently called function,* which the computer needs to wrap up next. It’s a LIFO situation: the function that was called last (that is, most recently), is the function we need to complete first.

The next thing the computer does is pop the top element of the call stack, which currently is factorial(2):

<img width="186" alt="image" src="https://user-images.githubusercontent.com/11669149/233876536-c9226bc7-6dbb-4033-9e79-ee5d532866ca.png">

The computer then completes its execution of factorial(2).

Now, the computer pops the next item from the stack. By this time, only factorial (3) is left on the stack, so the computer pops it and completes running factorial(3).

The stack is empty at this point, so the computer knows it’s done executing all of the methods, and the recursion is complete.

Looking back at this example from a bird’s-eye view, you’ll see that the order in which the computer calculates the factorial of 3 is as follows:

1. factorial(3) is called first. Before it’s done...
2. factorial(2) is called second. Before it’s done...
3. factorial(1) is called third.
4. factorial(1) is *completed* first.
5. factorial(2) is completed based on the result of factorial(1).
6. Finally, factorial(3) is completed based on factorial(2) results.

The factorial function is a calculation made based on recursion. The calculation is ultimately made by factorial(1) passing its result (which is 1) to factorial(2). Then, factorial(2) multiplies this 1 by 2, yielding 2, and passes this result to factorial(3). Finally, factorial(3) takes this result, and multiplies it by 3, computing the result of 6.

Some refer to this idea as *passing a value up through the call stack.* Each recursive function returns its computed value to its “parent” function. Eventually, the function that was initially called first computes the final value.

## Stack overflow

Let’s take a look back at the infinite recursion example from the beginning of the chapter. Recall that example() called itself ad infinitum. What do you think will happen to the call stack?

In the case of infinite recursion, the computer keeps pushing the same function repeatedly onto the call stack. The call stack grows until, eventually, the computer reaches a point where there’s simply no more room in its short-term memory to hold all this data. This causes an error known as *stack overflow*—the computer shuts down the recursion and says, “I refuse to call the function again because I’m running out of memory!”

## Filesystem traversal

Now that you’ve seen how recursion works, we can use it to solve certain problems that would otherwise be uncrackable. One type of problem in which recursion is a natural fit is when we need to delve into multiple layers of a problem without knowing how many layers there are.

Take the example of traversing through a filesystem. Let’s say you have a script that does something with all the contents inside a directory, such as printing all the subdirectory names. However, you don’t want the script only to handle the immediate subdirectories—you want it to act on all the sub-directories *within* the subdirectories of the directory and all their* subdirectories, and so on.

## Conclusion

As you’ve seen with the filesystem example, recursion is often a great choice for an algorithm in which the algorithm needs to dig into an arbitrary number of levels deep into something.

You’ve now seen how recursion works and how incredibly useful it can be. You’ve also learned how to walk through and read recursive code. However, most people have difficulty writing their own recursive functions when first starting out. In the next module, we’ll explore techniques to help you learn to write recursively. Along the way, you’ll discover other important use cases where recursion can be an incredible tool.
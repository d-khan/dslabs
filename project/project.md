# Project activity

## Task 1

You’re working on software that analyzes sports players. Following are two arrays of players of different sports:

```
basketball_players = [
      {first_name: "Jill", last_name: "Huang", team: "Gators"},
      {first_name: "Janko", last_name: "Barton", team: "Sharks"},
      {first_name: "Wanda", last_name: "Vakulskas", team: "Sharks"},
      {first_name: "Jill", last_name: "Moloney", team: "Gators"},
      {first_name: "Luuk", last_name: "Watkins", team: "Gators"}
]

football_players = [
      {first_name: "Hanzla", last_name: "Radosti", team: "32ers"},
      {first_name: "Tina", last_name: "Watkins", team: "Barleycorns"},
      {first_name: "Alex", last_name: "Patel", team: "32ers"},
      {first_name: "Jill", last_name: "Huang", team: "Barleycorns"},
      {first_name: "Wanda", last_name: "Vakulskas", team: "Barleycorns"}
]
```

If you look carefully, you’ll see that some players participate in more than one sport. Jill Huang and Wanda Vakulskas play both basketball *and* football.

You are to write a function that accepts two arrays of players and returns an array of the players who play in *both* sports. In this case, that would be:

`["Jill Huang", "Wanda Vakulskas"]`

While there are players who share first names and players who share last names, we can assume there’s only one person who has a particular *full* name (meaning first *and* last name).

We can use a nested-loops approach, comparing each player from one array against each player from the other array, but this would have a runtime of $O(N * M)$. 

**Your job is to optimize the function so that it can run just $O(N + M)$.**

## Task 2

You’re writing a function that accepts an array of distinct integers from 0, 1, 2, 3...up to N. However, the array will be missing one integer, and your function is to *return the missing one.*

For example, this array has all the integers from 0 to 6, but is missing the 4:

```
[2, 3, 0, 6, 1, 5]
```

Therefore, the function should return 4.

The next example has all the integers from 0 to 9, but is missing the 1:

```
[8, 2, 3, 9, 4, 7, 5, 0, 6]
```

In this case, the function should return the 1.

Using a nested-loops approach would take up to $O(N^2)$. 

**Your job is to optimize the code so that it has a runtime of $O(N)$.**

## Task 3

You’re working on some more stock-prediction software. The function you’re writing accepts an array of predicted prices for a particular stock over the course of time.

For example, this array of seven prices:

```
[10, 7, 5, 8, 11, 2, 6]
```

predicts that a given stock will have these prices over the next seven days. (On Day 1, the stock will close at \$10; on Day 2, the stock will close at $7; and so on.)

Your function should calculate the greatest profit that could be made from a single “buy” transaction followed by a single “sell” transaction.

In the previous example, the most money could be made if we bought the stock when it was worth \$5 and sold it when it was worth \$11. This yields a profit of $6 per share.

Note that we could make even more money if we buy and sell multiple times, but for now, this function focuses on the most profit that could be made from just *one* purchase followed by *one* sale.

Now, we could use nested loops to find the profit of every possible buy and sell combination. However, this would be $O(N^2)$ and too slow for our hotshot trading platform. 

**Your job is to optimize the code so that the function clocks in at just $O(N)$.**

## Task 4

1. You’re writing a function that accepts an array of numbers and computes the highest product of any two numbers in the array. At first glance, this is easy, as we can just find the two greatest numbers and multiply them. However, our array can contain negative numbers and look like this:

   ```
   [5, -10, -6, 9, 4]
   ```

   We could use nested loops to multiply every possible pair of numbers, but this would take $O(N^2)$ time. **Your job is to optimize the function so that it’s a speedy $O(N)$.**

## Task 5

You’re creating software that analyzes the data of body temperature readings taken from hundreds of human patients. These readings are taken from healthy people and range from 97.0 degrees Fahrenheit to 99.0 degrees Fahrenheit. An important point: within this application, *the decimal point never goes beyond the tenth place.*

Here’s a sample array of temperature readings:

```
[98.6, 98.0, 97.1, 99.0, 98.9, 97.8, 98.5, 98.2, 98.0, 97.1]
```

You are to write a function that sorts these readings from lowest to highest.

Using a classic sorting algorithm such as Quicksort would take $O(N log N)$. However, in this case, writing a faster sorting algorithm is possible.

Yes, that’s right. Even though you’ve learned that the fastest sorts are O(N log N), this case is different. Why? In this case, there are limited possibilities for the readings. In such a case, we can sort these values in $O(N)$. It may be $N$ multiplied by a constant, but that’s still considered $O(N)$.

## Task 6

You’re writing a function that accepts an array of unsorted integers and returns the length of the *longest consecutive sequence* among them. The sequence is formed by integers that increase by 1. For example, in the array:

```
[10, 5, 12, 3, 55, 30, 4, 11, 2]
```

the longest consecutive sequence is 2-3-4-5. These four integers form an increasing sequence because each integer is one greater than the previous one. While there’s also a sequence of 10-11-12, it’s only a sequence of three integers. In this case, the function should return 4, since that’s the length of the *longest* consecutive sequence that can be formed from this array.

One more example:

```
[19, 13, 15, 12, 18, 14, 17, 11]
```

This array’s longest sequence is 11-12-13-14-15, so the function would return 5.

**Your job is to optimize the function so that it takes $O(N)$ time.**

## Notes

- Complete the tasks using C++ programming language. 
- Submit the code in a separate .cpp file extension.
- Each task worth is 5 points.


# Binary heaps

Now that we’ve discovered the tree, we’ve unlocked many new data structures. In the previous chapter, we focused specifically on the binary search tree, but there are also many other types of trees. Like all data structures, each type of tree comes with its own benefits and drawbacks, and the trick is knowing which one to harness in a specific situation.

In this chapter, we’ll explore the heap, a type of tree data structure with special powers that can be leveraged for specific scenarios, particularly when we want to constantly keep tabs on the greatest or least data element in a dataset.

To appreciate what a heap can do, let’s take a look at a completely different data structure: the priority queue.

## Priority Queue

You learned about Queues and discovered that the queue is a list in which items are processed First In, First Out (FIFO). Essentially, this means that data is inserted only at the *end* of the queue, and data is accessed and removed only from the *front* of the queue. In accessing the queue’s data, we precede the order in which the data was inserted.

A *priority queue* is a list whose deletions and access are just like a classic queue but whose insertions are like an ordered array. We only delete and access data from the *front* of the priority queue, but when we insert data, we always make sure the data remains sorted in a specific order.

One classic example of where a priority queue is helpful is an application that manages the triage system for a hospital emergency room. In the ER, we don’t treat people strictly in the order in which they arrive. Instead, we treat people according to the severity of their symptoms. If someone suddenly arrives with a life-threatening injury, that patient will be placed at the front of the queue, even if the person with the flu had arrived hours earlier.

Let’s say our triage system ranked the severity of a patient’s condition on a scale of 1 to 10, with 10 being the most critical. Our priority queue may look like this:

<img width="372" alt="image" src="https://user-images.githubusercontent.com/11669149/229823633-5d4b684d-7b45-43cc-92d2-1cc6827c001b.png"  >

In determining the next patient to treat, we will always select the patient at the front of the priority queue, since that person’s need is the most urgent. In this case, the next patient we’d treat is Patient C.

If a new patient now arrives with a condition severity of 3, we’ll initially place this patient at the appropriate spot within the priority queue. We’ll call this person Patient E:

<img width="285" alt="image" src="https://user-images.githubusercontent.com/11669149/229824181-b7c71dc8-cd23-4c74-8403-9033819636d1.png"  >

The priority queue is an example of an abstract data type. That is, it can be implemented using other, more fundamental data structures. One straight- forward way we can implement a priority queue is by using an ordered array. That is, we use an array and apply the following constraints:

- When we insert data, we ensure we always maintain proper order.
- Data can only be removed from the end of the array. (This will represent the front of the priority queue.)

While this approach is straightforward, let’s analyze its efficiency. The priority queue has two primary operations: deletions and insertions.

We’ve seen previously that deleting from the front of an array is $O(N)$, since we have to shift all the data to fill the gap created at index 0. However, we’ve cleverly tweaked our implementation to consider the array's end as the priority queue's front. This way, we’re always deleting from the end of the array, which is $O(1)$.

With $O(1)$ deletions, our priority queue is in good shape so far. But what about insertions?

You learned that inserting into an ordered array is $O(N)$, since we have to inspect up to all N elements of the array to determine where our new data should go. (Even if we find the correct spot early, we must shift all the remaining data to the right.)

Our array-based priority queue, then, has deletions that are $O(1)$ and insertions that are $O(N)$. If we expect there to be many items in our priority queue, the $O(N)$ insertions may cause some real unwanted drag in our application.

Because of this, computer scientists discovered another data structure that serves as a more efficient foundation for the priority queue. And this data structure is the heap.

## Heaps

There are several types of heaps, but we will focus on the binary heap.

The binary heap is a specific kind of binary tree. As a reminder, a binary tree is a tree where each node has a maximum of two child nodes. (The binary *search* tree from the last chapter was one specific type of binary tree.)

Now, binary heaps come in two flavors: the max-heap and the min-heap. We’ll work with the max-heap for now, but as you’ll see later, the difference between the two is trivial.

Going forward, I will refer to this data structure simply as a heap, even though we’re specifically working with a binary max heap.

The *heap* is a binary tree that maintains the following conditions:

- The value of each node must be greater than each of its descendant nodes. This rule is known as the heap condition.
- The tree must be *complete.

Let’s break down both conditions, starting with the heap condition.

### The heap condition

The *heap condition* says that each node’s value must be greater than each and every one of its descendants.

For example, the following tree meets the heap condition since each node is greater than any of its descendants, as shown below.

<img width="222" alt="image" src="https://user-images.githubusercontent.com/11669149/229826570-7fe8179f-943c-4e7b-9c55-9a8065d905c5.png">

In this example, the root node of 100 has no descendant that is greater than it. Similarly, the 88 is greater than both of its children, and so is the 25.

The following tree isn’t a valid heap because it doesn’t meet the heap condition:

<img width="225" alt="image" src="https://user-images.githubusercontent.com/11669149/229826793-f7f44cc2-8825-49cb-914b-fb5a5c0f92e0.png">

As you can see, the 92 is greater than its parent of 88. This violates the heap condition.

Note how the heap is structured very differently than the binary search tree. Each node’s right child is greater than in a binary search tree. In a heap, however, a node *never* has any descendant that is greater than it.

We can also construct a heap with the opposite heap condition: each node must contain a *smaller* value than any of its descendants. Such a heap is known as the min-heap, which I mentioned earlier. We will continue to focus on the max-heap, where each node must be *greater* than all of its descendants. Ultimately, whether a heap is a max-heap or a min-heap is trivial, as everything else about both heaps is identical; they only have reversed heap conditions. Otherwise, the fundamental idea is the same.

### Complete trees

Let’s get to the second rule of heaps—that the tree needs to be complete.

A *complete tree* is a tree that is completely filled with nodes; no nodes are missing. So, all nodes are there if you read each tree level from left to right. However, the bottom row *can* have empty positions as long as there aren’t any nodes to the right of these empty positions. This is best demonstrat- ed with examples.

The following tree is complete since each level (meaning each row) of the tree is completely filled in with nodes:

<img width="146" alt="image" src="https://user-images.githubusercontent.com/11669149/229831827-6e1fe975-d121-405b-9c34-a7fd2f897d1e.png">

The following tree is *not* complete, since it’s missing a node on the third level:

<img width="145" alt="image" src="https://user-images.githubusercontent.com/11669149/229832043-99e2bc49-a117-40fc-8bde-f5d55c7f2e57.png">

Now, the next tree is considered complete, since its empty positions are limited to the bottom row, and there aren’t any nodes found to the right of the empty positions:

<img width="127" alt="image" src="https://user-images.githubusercontent.com/11669149/229832320-b07cd452-5592-4ae1-b4e9-6d2acad5e4dc.png">

A heap, then, is a tree that meets the heap condition *and* is also complete. Here is just one more example of a heap:

<img width="376" alt="image" src="https://user-images.githubusercontent.com/11669149/229832511-ee3e0436-7e91-437c-a823-8741221470c1.png">

This is a valid heap since each node is greater than any of its descendants, and the tree is also complete. While it does have some gaps in the bottom row, these gaps are limited to the very right of the tree.

### Heap properties

Now that you know what a heap is, let’s examine some of its interesting properties.

While the heap condition dictates that the heap be ordered a certain way, this ordering is still useless when it comes to searching for a value within the heap.

For example, let’s say that in the above heap, we want to search for the value 3. If we start at the root node of 100, should we search among its left or right descendants? In a binary search tree, we’d know that the 3 must be among the 100’s left descendants. In a heap, however, we all know that the 3 has to be a descendant of the 100 and can’t be its ancestor. But we’d have no idea which child node to search next. Indeed, the 3 is among the 100’s *right* descendants, but it could have also easily been among its left descendants.

Because of this, heaps are said to be *weakly ordered* compared to binary search trees. While heaps have *some* order, as descendants cannot be greater than their ancestors, this isn’t enough order to make heaps worth searching through.

Another property of heaps may be obvious by now but is worth calling attention to: the root node will always have the greatest value in a heap. (In a min-heap, the root will contain the smallest value.) This is why a heap is a great tool for implementing priority queues. We always want to access the value with the greatest priority in the priority queue. With a heap, we always know that we can find this in the root node. Thus, the root node will represent the item with the highest priority.

The heap has two primary operations: inserting and deleting. As we noted, searching within a heap would require us to inspect each node, so the search is not an operation usually implemented in the context of heaps. (A heap can also have an optional “read” operation, which would look at the root node's value.)

Before we move on to how the heap’s primary operations work, let me define one more term, since it’ll be used heavily in the upcoming algorithms.

The heap has something called a *last node.* A heap’s *last node* is the rightmost node in its bottom level.

In this heap, the 3 is the last node since it’s the rightmost node in the bottom row. Next, let’s get into the heap’s primary operations.

<img src="/Users/danish/Library/Application%20Support/typora-user-images/image-20230404075948478.png" alt="image-20230404075948478" style="zoom:50%;" />

### Heap insertions

To insert a new value into the heap, we perform the following algorithm:

1. We create a node containing the new value and insert it at the next available rightmost spot in the bottom level. Thus, this value becomes the heap’s last node.
2. Next, we compare this new node with its parent node.
3. If the new node is greater than its parent node, we swap the new node with the parent node.
4. We repeat Step 3, effectively moving the new node up through the heap, until it has a parent whose value is greater than it.

Let’s see this algorithm in action. Here’s what would happen if we were to insert a 40 into the heap:

Step 1: We add the 40 as the heap’s last node:

<img width="377" alt="image" src="https://user-images.githubusercontent.com/11669149/229854386-4557761b-3e52-4c1f-a0ac-f2d8eb3149b9.png">

Note that doing the following would have been incorrect:

<img width="382" alt="image" src="https://user-images.githubusercontent.com/11669149/229854540-22dae107-8134-47ae-9b70-b8813cb81da4.png">

Placing the 40 as a child of the 12 node makes the tree *incomplete,* since we’d now have a node to the right of an empty position. For a heap to remain a heap, it must always be complete.

Step 2: We compare the 40 with its parent node, which happens to be the 8. Since the 40 is greater than the 8, we swap the two nodes:

<img width="402" alt="image" src="https://user-images.githubusercontent.com/11669149/229854719-e3c523eb-069c-4e72-ad8c-1724d6cd2abe.png">

Step 3: We compare the 40 with its new parent, the 25. Since the 40 is greater than the 25, we swap them:

<img width="389" alt="image" src="https://user-images.githubusercontent.com/11669149/229854967-1e4c8774-0328-42bb-be03-cdfbf5ba1870.png">

Step 4: We compare the 40 to its parent, which is the 100. Since the 40 is smaller than the 100, we’re done!

This process of moving the new node up the heap, is called *trickling* the node up through the heap. Sometimes it moves up to the right, and sometimes to the left, but it always moves up until it settles into the correct position.

The efficiency of inserting into a heap is $O(log N)$. As discussed before, for N nodes in any binary tree, the tree is organized into about $log(N)$ rows. Since at most, we’d have to trickle the new value up to the top row, this will take $log(N)$ steps at most.

While the insertion algorithm seems pretty straightforward, there’s one little snag. The first step has us place the new value as the heap’s last node. But this begs the question: how do we find the spot that will be the last node?

Let’s take a look again at the heap before we insert the 40:

<img width="391" alt="image" src="https://user-images.githubusercontent.com/11669149/229859384-c50acd42-ce07-4e34-ae43-8056e8024f49.png">

We know by looking at the diagram that to make the 40 into the last node, we’d make it the right child of the 8, as that’s the next available spot in the bottom row.

However, a computer doesn’t have eyeballs, and doesn’t see the heap as a bunch of rows. All it sees is the root node, and can follow links to child nodes. So, how do we create an algorithm for the computer to find the spot for the new value?

Take our example heap. When we start at the root node of 100, do we tell the computer to look among the 100’s right descendants to find the next available spot for the new last node?

While it’s true that in our example heap the next available spot is among the 100’s right descendants, take a look at the following alternative heap:

<img width="307" alt="image" src="https://user-images.githubusercontent.com/11669149/229859684-37ece75a-dcba-4064-bcde-bf8f64d55bc2.png">

In this heap, the next available spot for the new last node would be the 88’s right child, which is among the 100’s *left* descendants.

Essentially, then, just as it’s impossible to search through a heap, it’s impossible to efficiently find the heap’s last node (or next available spot to hold a new last node) without having to inspect each and every node.

So, how *do* we find the next available node? I’ll explain this later on, but for now, let’s call this issue the Problem of the Last Node.

In the meantime, let’s explore the heap’s other primary operation, which is deletion.

### Heap deletion

The first thing to know about deleting a value from a heap is that *we only ever delete the root node.* This is right in line with the way a priority queue works, in that we only access and remove the highest-priority item.

The algorithm for deleting the root node of a heap is as follows:

1. Move the *last node* into where the root node was, effectively removing the original root node.
2. Trickle the root node down into its proper place. I’ll explain how trickling down works shortly.

Let’s say we’re going to remove the root node from the heap

<img width="385" alt="image" src="https://user-images.githubusercontent.com/11669149/229860946-9b407e45-f4d6-429d-86a3-73c5cdb8f561.png">

In this example, the root node is the 100. To delete it, we overwrite the root by placing the last node there instead. In this case, the last node is the 3. So, we move the 3 and place it where the 100 was:

<img width="375" alt="image" src="https://user-images.githubusercontent.com/11669149/229861128-a0cb13a6-923f-4b2f-832c-9feffae19931.png">

Now, we can’t leave the heap as is, since the heap condition has been violated and since the 3 is currently less than some (actually, most) of its descendants. To make things right again, we need to trickle the 3 down until its heap con- dition has been restored.

Trickling down is a tad more complex than trickling up, since each time we trickle a node down, we have two possible directions as to where we will trickle it down. That is, we can either swap it with its left child or its right child. (When trickling up, on the other hand, each node has only one parent to swap with.)

Here’s the algorithm for trickling *down.* For the sake of clarity, we’re going to call the node we’re trickling the “trickle node.”

1. We check both children of the trickle node and see which one is larger.
2. If the trickle node is smaller than the larger of the two child nodes, we swap the trickle node with that larger child.
3. We repeat Steps 1 and 2 until the trickle node has no children who are greater than it.

Let’s see this in action.

Step 1: The 3, which is the trickle node, currently has two children, the 88 and the 25. The 88 is larger of the two, and since the 3 is smaller than the 88, we swap the trickle node with the 88:

<img width="397" alt="image" src="https://user-images.githubusercontent.com/11669149/229861720-91ffa7e8-0843-4bee-bbf5-b183f42a9758.png">

Step 2: The trickle node now has two new children, the 87 and the 16. The 87 is the larger one, and it is greater than the trickle node. So, we swap the trickle node with the 87:

<img width="402" alt="image" src="https://user-images.githubusercontent.com/11669149/229861921-da15c997-6627-4bd7-b491-7ba81fa17060.png">

Step 3: The trickle node’s children are currently 86 and 50. The 86 is the larger of the two, and it is also greater than the trickle node, so we swap the 86 with the trickle node:

<img width="416" alt="image" src="https://user-images.githubusercontent.com/11669149/229862029-656feba8-f02e-4af3-8c45-cb9e6329259f.png">

At this point, the trickle node has no children that are greater than it. (In fact, it has no children at all.) So, we’re done, as the heap condition has been restored.

The reason why we always swap the trickle node with the *greater* of its two children is because if we swap it the with the smaller one, we’d end up violat- ing the heap condition immediately. Watch what happens when we try to swap the trickle node with smaller child.

Let’s start again with the trickle node of 3 as our root:

<img width="391" alt="image" src="https://user-images.githubusercontent.com/11669149/229862292-ea563209-52df-405d-8722-0ab58aa962fc.png">

Let’s swap the 3 with the 25, which is the smaller child:

<img width="375" alt="image" src="https://user-images.githubusercontent.com/11669149/229862476-9fa6d36c-439f-4faa-8f88-fae941cbb528.png">

We’ve now placed the 25 in a situation where it is a parent of the 88. Since the 88 is greater than its parent, the heap condition has been broken.

Like insertion, the time complexity of deletion from a heap is $O(log N)$, as we have to trickle a node from the root down through all $log(N)$ levels of the heap.

### Heap vs ordered arrays

Now that you know the efficiency of heaps, let’s see why it’s a great choice for implementing priority queues.

Here’s a side-by-side comparison of ordered arrays versus heaps:

|           | Ordered Array | Heap      |
| --------- | ------------- | --------- |
| Insertion | $O(N)$        | $O(logN)$ |
| Deletion  | $O(1)$        | $O(logN)$ |

At first glance, it seems that it’s a wash. Ordered arrays are slower than heaps regarding insertion but faster than heaps for deletion.

However, heaps are considered to be the better choice, and here’s why.

While $O(1)$ is extremely fast, $O(log N)$ is still *very* fast. And $O(N)$, by comparison, is slow. 

In this light, it becomes clearer as to why the heap is considered the better choice. We’d rather use a data structure that is consistently very fast than a data structure that is sometimes extremely fast and sometimes slow.

It’s worth pointing out that priority queues generally perform insertions and deletions equally. Consider the emergency room example, where we expect to treat everyone who comes in. So, we want both our insertions and deletions to be fast. If either operation is slow, our priority queue will be inefficient.

With a heap, we ensure that both of the priority queue’s primary operations—insertion and deletion—perform quickly.

### Last node problem

While the heap deletion algorithm seems straightforward, it once again raises the Problem of the Last Node.

I explained that the first step of deletion requires us to move the last node and turn it into the root node. But, how do we find the last node in the first place?

Before we solve the Problem of the Last Node, let’s first explore why insertion and deletion are so dependent on the last node anyway. Why couldn’t we insert new values elsewhere in the heap? And why, when deleting, can’t we replace the root node with some other node other than the last node?

Now, if you think about it, you’ll realize that if we were to use other nodes, the heap would become incomplete. But this begs the next question: why is completeness *important* for the heap?

The reason why completeness is important is because we want to ensure our heap remains *well-balanced.*

To see this clearly, let’s take another look at insertion. Let’s say we have the following heap:

<img width="310" alt="image" src="https://user-images.githubusercontent.com/11669149/229867881-a9d9254e-443f-42be-bee8-bb0a381e2dc5.png">

If we want to insert a 5 into this heap, the only way to keep the heap well- balanced is by making the 5 the last node, in this case, making it a child of the 10:

<img width="310" alt="image" src="https://user-images.githubusercontent.com/11669149/229868010-a1522549-8a68-4b47-ba59-9d66b8188193.png">

Any alternative to this algorithm would cause imbalance. Say, in an alternative universe, the algorithm was to insert the new node into the bottom leftmost node, which we could easily find by traversing the left children until we hit the bottom. This would make the 5 a child of the 15:

<img width="359" alt="image" src="https://user-images.githubusercontent.com/11669149/229868118-9b0d061d-d46d-472b-a845-21c64bc88e2c.png">

Our heap is now somewhat imbalanced, and it’s easy to see how much more imbalanced it would become if we kept inserting new nodes at the bottom leftmost spot.

Similarly, when deleting from a heap, we always turn the last node into the root because, otherwise, the heap can become imbalanced. Take again our example heap:

<img width="304" alt="image" src="https://user-images.githubusercontent.com/11669149/229868479-99a33b43-6f93-48f8-8aa3-58f880aad7fb.png">

If in our alternative universe we always moved the bottom rightmost node into the root position, the 10 would become the root node, and we’d end up with an imbalanced heap with a bunch of left descendants and zero right descendants.

Now, the reason why this balance is so important is because it’s what allows us to achieve $O(log N)$ operations. In a severely imbalanced tree like the following one, traversing it could take $O(N)$ steps instead:

<img width="217" alt="image" src="https://user-images.githubusercontent.com/11669149/229868628-133c2a96-6ce2-442e-b702-83857352636d.png">

But this brings us back to the Problem of the Last Node. What algorithm would allow us to consistently find the last node of any heap? (Again, without having to traverse all N nodes.)

And this is where our plot takes a sudden twist.

### Arrays vs heaps

Because finding the last node is so critical to the heap’s operations, and we want to make sure that finding the last node is efficient, heaps are *usually implemented using arrays.*

While until now we always assumed that every tree consists of independent nodes connected to each other with links (just like a linked list), you will now see that we can also use an array to implement a heap. That is, the heap itself can be an abstract data type that really uses an array under the hood.

The figure below shows how an array is used to store the values of a heap.

<img width="449" alt="image" src="https://user-images.githubusercontent.com/11669149/229868896-396ad187-b3e5-417a-8e27-efb22875d0ba.png">

The way this works is that we assign each node to an index within the array. In the previous diagram, the index of each node is found in a square below the node. If you look carefully, you’ll see that we assign the index of each node according to a specific pattern.

The root node is always stored at index 0. We then move down a level and go from left to right, assigning each node to the next available index in the array. So, on the second level, the left node (88) becomes index 1, and the right node (25) becomes index 2. When we reach the end of a level, we move down to the next level and repeat this pattern.

Now, we’re using an array to implement the heap because it solves the Problem of the Last Node. How?

When we implement the heap in this fashion, *the last node will always be the final element of the array.* Since we move top down and left to right when assigning each value to the array, the last node will always be the final value in the array. The previous example shows that 3, the last node, is the last value in the array.

Because the last node will always be found at the end of the array, it becomes trivial to find the last node: we need to access the final element. In addition, when we insert a new node into the heap, we do so at the end of the array in order to make it the last node.

### Traversing an Array-Based Heap

As you’ve seen, the heap’s insertion and deletion algorithms require us to be able to trickle our way through the heap. Trickling, in turn, requires us to be able to traverse the heap by accessing a node’s parent or children. But how do we move from node to node when all the values are merely stored in an array? Traversing a heap would have been straightforward if we could have simply followed each node’s links. But now that the heap is an array under the hood, how do we know which nodes are connected to each other?

There’s an interesting solution to this. It turns out that when we assign the indexes of the heap’s nodes according to the pattern described earlier, the following traits of a heap are always true:

- To find the left child of any node, we can use the formula, (index * 2) + 1
- To find the right child of any node, we can use the formula, (index * 2) + 2

Take another look at the previous diagram and focus on the 16, which is at index 4. To find its left child, we multiply its index (4) by 2 and add 1, which yields 9. This means that index 9 is the left child of the node at index 4.

Similarly, to find the right child of index 4, we multiply the 4 by 2 and add 2, which yields 10. This means that index 10 is the right child of index 4.

Because these formulas always work, we’re able to treat our array as a tree.

Let’s add these two methods to our Heap class:

```
def left_child_index(index) 
	return (index * 2) + 1
end
def right_child_index(index) 
	return (index * 2) + 2
end
```

Each of these methods accept an index within the array and return the left or right child index, respectively.

Here’s another important trait of array-based heaps:

- To find a node’s parent, we can use the formula, (index - 1) / 2

Note that this formula uses integer division, meaning we throw away any numbers beyond the decimal point. For example, 3 / 2 is considered 1, rather than the more accurate 1.5.

Again, in our example heap, focus on index 4. If we take that index, subtract 1, and then divide by 2, we get 1. And as you can see in the diagram, the parent of the node at index 4 is found at index 1.

So, now we can add another method to our Heap class:

```
def parent_index(index) 
	return (index - 1) / 2
end
```

This method accepts an index and calculates the index of its parent node.

### Example - Heap insertion

```c++
// C++ program to insert new element to Heap
 
#include <iostream>
using namespace std;
 
#define MAX 1000 // Max size of Heap
 
// Function to heapify ith node in a Heap
// of size n following a Bottom-up approach
void heapify(int arr[], int n, int i)
{
    // Find parent
    int parent = (i - 1) / 2;
 
    if (arr[parent] > 0) {
        // For Max-Heap
        // If current node is greater than its parent
        // Swap both of them and call heapify again
        // for the parent
        if (arr[i] > arr[parent]) {
            swap(arr[i], arr[parent]);
 
            // Recursively heapify the parent node
            heapify(arr, n, parent);
        }
    }
}
 
// Function to insert a new node to the Heap
void insertNode(int arr[], int& n, int Key)
{
    // Increase the size of Heap by 1
    n = n + 1;
 
    // Insert the element at end of Heap
    arr[n - 1] = Key;
 
    // Heapify the new node following a
    // Bottom-up approach
    heapify(arr, n, n - 1);
}
 
// A utility function to print array of size n
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
 
    cout << "\n";
}
 
// Driver Code
int main()
{
    // Array representation of Max-Heap
    // 10
    //    /  \
    // 5    3
    //  / \
    // 2   4
    int arr[MAX] = { 10, 5, 3, 2, 4 };
 
    int n = 5;
 
    int key = 15;
 
    insertNode(arr, n, key);
 
    printArray(arr, n);
    // Final Heap will be:
    // 15
    //    /   \
    // 5     10
    //  / \   /
    // 2   4 3
    return 0;
}
```

### Example - Heap deletion

```c++
// C++ program for implement deletion in Heaps
 
#include <iostream>
 
using namespace std;
 
// To heapify a subtree rooted with node i which is
// an index of arr[] and n is the size of heap
void heapify(int arr[], int n, int i)
{
    int largest = i; // Initialize largest as root
    int l = 2 * i + 1; // left = 2*i + 1
    int r = 2 * i + 2; // right = 2*i + 2
 
    // If left child is larger than root
    if (l < n && arr[l] > arr[largest])
        largest = l;
 
    // If right child is larger than largest so far
    if (r < n && arr[r] > arr[largest])
        largest = r;
 
    // If largest is not root
    if (largest != i) {
        swap(arr[i], arr[largest]);
 
        // Recursively heapify the affected sub-tree
        heapify(arr, n, largest);
    }
}
 
// Function to delete the root from Heap
void deleteRoot(int arr[], int& n)
{
    // Get the last element
    int lastElement = arr[n - 1];
 
    // Replace root with last element
    arr[0] = lastElement;
 
    // Decrease size of heap by 1
    n = n - 1;
 
    // heapify the root node
    heapify(arr, n, 0);
}
 
/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}
 
// Driver Code
int main()
{
    // Array representation of Max-Heap
    //     10
    //    /  \
    //   5    3
    //  / \
    // 2   4
    int arr[] = { 10, 5, 3, 2, 4 };
 
    int n = sizeof(arr) / sizeof(arr[0]);
 
    deleteRoot(arr, n);
 
    printArray(arr, n);
 
    return 0;
}
```

### Alternate heap implementations

Our heap implementation is now complete. It’s worth noting that while we did use an array to implement the heap under the hood, it *is possible* to implement a heap using linked nodes as well. (This alternative implementation uses a different trick to solve the Problem of the Last Node, one that involves binary numbers.)

However, the array implementation is the more common approach, so that is what I presented here. It’s also really interesting to see how an array can be used to implement a tree.

Indeed, it’s possible to use an array to implement any binary tree, such as the binary search tree from the previous chapter. However, the heap is the first case of a binary tree where an array implementation provides an advantage, as it helps us find the last node easily.

### Heaps as Priority Queues

Now that you understand how heaps work, we can circle back to our old friend, the priority queue.

Again, the primary function of a priority queue is to allow us immediate access to the highest-priority item in the queue. In our emergency room example, we want to first address the person with the most serious problem.

For this reason, a heap is a natural fit for priority queue implementations. The heap gives us immediate access to the highest-priority item, which can always be found at the root node. Each time we take care of the highest-priority item (and then remove it from the heap), the next-highest item floats to the top of the heap and is on deck to be addressed next. And the heap accomplishes this while maintaining very fast insertions and deletions, both of which are $O(log N)$.

Contrast this to the ordered array, which requires much slower insertions of $O(N)$ to ensure that each new value is in its proper place.

It turns out that the heap’s weak ordering *is its very advantage.* The fact that it doesn’t have to be perfectly ordered allows us to insert new values in $O(log N)$ time. At the same time, the heap is *ordered just enough* so that we can always access the one item we need at any given time—the heap’s greatest value.

## Conclusion

So far, we’ve seen how different types of trees can optimize different types of problems. Binary search trees kept search fast while minimizing the cost of insertions, and heaps were the perfect tool for building priority queues.

In the next module, we’ll explore another tree used to power some of the most common text-based operations you use daily.


# Linked lists

The following contents are in draft mode as I could not find time to finalize and include them in my book.

- Linked lists are extensions to arrays and perform better than arrays in some but not all scenarios.

- You have already noticed that data structures are costly to run in some scenarios. It is a programmer's job to select the correct data structure for the given job.

- As discussed previously that arrays require contiguous memory to store data. For example, if you have 1M data points to process, storing in arrays means that the compiler has to find a space in memory to fit the size of the array in contiguous memory cells. If memory is infinite, then this is not a problem.

- Linked lists do not require contiguous memory cells. The elements in the linked list (often called nodes) can be scattered.

- In a linked list, each node represents one item in the list. The big question is: if the nodes are not next to each other in memory, how does the computer know which nodes are part of the same linked list?

- This is the key to the linked list: each node also comes with a little extra information, namely, the memory address of the *next* node in the list.

  This extra piece of data—this pointer to the next node’s memory address—is known as a *link.* Here is a visual depiction of a linked list:

  <img width="499" alt="image" src="https://user-images.githubusercontent.com/11669149/224621864-85c4fd09-db36-415b-b2c6-955d302bb5d6.png">

- In this example, we have a linked list that contains four pieces of data: "a", "b", "c", and "d". However, it uses *eight* memory cells to store this data because each node consists of two memory cells. The first cell holds the actual data, while the second cell serves as a link indicating where the next node begins in memory. The final node’s link contains null since the linked list ends there.

  > **A linked list’s first node can also be referred to as its *head,* and its final node as its *tail.***

  If the computer knows at which memory address the linked list begins, it has all it needs to begin working with the list! Since each node contains a link to the next node, all the computer needs to do is follow each link to string together the entire list.

## Read operation

- As you know, a computer can read from an array in O(1) time. But now let’s figure out the efficiency of reading from a linked list.

- If you want to read, say, the value of the third item of a linked list, the computer cannot look it up in one step, because it wouldn’t immediately know where to find it in the computer’s memory. After all, each node of a linked list could be *anywhere* in memory! All our program knows immediately is the memory address of the *first* node of the linked list. However, it doesn’t know offhand where any of the other nodes are.

- To get to any node, then, we always need to start with the first node (the only node we initially have access to), and follow the chain of nodes until we reach the node we want.
- It turns out, then, that if we were to read from the last node in the list, it would take $N$ steps for $N$ nodes in the list. Linked lists having a worst-case read of $O(N)$ is a major disadvantage when compared with arrays that can read any element in just $O(1)$.

## Searching operation

- As you know, searching means looking for a value within the list and returning its index. We’ve seen that linear search on an array has a speed of $O(N)$, since the computer needs to inspect each value one at a time.
- Linked lists also have a search speed of $O(N)$. To search for a value, we need go through a similar process as we did with reading. That is, we begin with the first node and follow the links of each node to the next one. Along the way, we inspect each value until we find what we’re looking for.

## Insert operation

- Recall that the worst-case scenario for insertion into an array is when the program inserts data into index 0, because it first has to shift the rest of the data one cell to the right, which ends up yielding an efficiency of $O(N)$. With linked lists, however, insertion at the beginning of the list takes just one step—which is $O(1)$. Let’s see why.

<img width="348" alt="image" src="https://user-images.githubusercontent.com/11669149/224626230-e0e021ce-94ff-46bc-98e8-f99fb491b74a.png">

If we want to add "yellow" to the beginning of the list, all we have to do is create a new node and have its link point to the node containing "blue":

<img width="476" alt="image" src="https://user-images.githubusercontent.com/11669149/224626320-32808934-bacf-4327-9976-025a0dd12a7b.png">

- Inserting a node other than the start of the linked list will take $O(N)$ steps. Inserting a node at the end will take $O(N+1)$ steps, where N is to access the elements, and 1 step is to insert the element, thus, removing the constant, the efficiency will become $O(N)$.
- Adding a node other than at the beginning will require node traversing. For example, if a purple node is added between the blue and green nodes, the address of the blue node is needed. The first node address is known in the linked list, and the other node's address is known as you traverse the chain.

## Delete operation

- Recall that in an array in which deleting the first element means shifting all remaining data one cell to the left, which takes $O(N)$ time. However, deleting the last element in an array will take $$O(1)$$, because there is no shifting required.
- When deleting the *final* node of a linked list, the actual deletion takes one step—we take the second-to-last node and make its link null. However, it takes N steps to even access the second-to-last node in the first place since we need to start at the beginning of the list and follow the links until we reach it.
- While deleting from the beginning or end of a linked list is straightforward, deleting from anywhere in the middle is slightly more involved.
- Say we want to delete the value at index 2 ("purple") from our example linked list of colors as shown in the figure below

<img width="473" alt="image" src="https://user-images.githubusercontent.com/11669149/224784945-c8f8bd10-4855-4973-9689-2abd3953e555.png">



- To accomplish this, we need to first access the node immediately *preceding* the one we’re deleting ("blue”). Then, we change its link to point to the node that is immediately *after* the node we’re deleting ("green"). The following visualization demonstrates us changing the link of the "blue" node from "purple" to "green":

<img width="440" alt="image" src="https://user-images.githubusercontent.com/11669149/224785353-f734f373-2eda-476b-b908-3004d717414c.png">

> __It’s interesting to note that when we delete a node from our linked list, it still exists in memory. We remove the node from our list by ensuring no other node links to it.__

| Scenario                          | Array                       | Linked list                 |
| --------------------------------- | --------------------------- | --------------------------- |
| Reading                           | $O(1)$                      | $$O(N)$$                    |
| Search                            | $$O(N)$$                    | $$O(N)$$                    |
| Insert or delete at the beginning | $$O(N)$$                    | $$O(1)$$                    |
| Insert or delete in the middle    | Between $$O(N)$$ & $$O(1)$$ | Between $$O(N)$$ & $$O(1)$$ |
| Insert or delete at the end       | $$O(1)$$                    | $$O(N)$$                    |

## Linked list example

One case where linked lists shine is when we examine a single list and delete many elements from it. Let’s say, for example, we’re building an application that combs through existing lists of email addresses and removes any email address that has an invalid format.

No matter whether the list is an array or a linked list, we need to comb through the entire list one element at a time to inspect each email address. This, naturally, takes N steps. However, let’s examine what happens when we actually delete each email address.

With an array, each time we delete an email address, we need another O(N) steps to shift the remaining data to the left to close the gap. All this shifting will happen before we can even inspect the next email address.

Let’s assume that 1 in 10 email addresses are invalid. If we had a list of 1,000 email addresses, we’d have about 100 invalid ones. Our algorithm, then, would take 1,000 steps to read all 1,000 email addresses. On top of that, though, it might take up to an additional 100,000 steps for deletion, as for each of the 100 deleted addresses, we might shift up to 1,000 other elements.

With a linked list, however, as we comb through the list, each deletion takes just one step, as we can simply change a node’s link to point to the appropriate node and move on. For our 1,000 emails, then, our algorithm would take just 1,100 steps, as there are 1,000 reading steps, and 100 deletion steps.

It turns out, then, that linked lists are an amazing data structure for moving through an entire list while making insertions or deletions, as we never have to worry about shifting other data as we make an insertion or deletion.

## Double linked lists

Linked lists actually come in a number of different flavors. The linked list we’ve discussed until this point is the “classic” linked list, but with some slight modifications, we can grant linked lists additional superpowers.

One variant form of the linked list is the *doubly linked list.*

A doubly linked list is like a linked list except that each node has *two* links—one that points to the next node, and another that points to the *previous* node. In addition, the doubly linked list always keeps track of both the first and last nodes, instead of just the first node.

Here’s what a doubly linked list looks like:

<img width="506" alt="image" src="https://user-images.githubusercontent.com/11669149/224850865-3473f9dc-fe83-4f6f-a1c2-96251041b787.png">



Since a doubly linked list always knows where both its first and last nodes are, we can access each of them in a single step, or $$O(1)$$. So, just as we can read, insert, or delete from the beginning of the list in $$O(1)$$, we can do the same from the end of the list in $$O(1)$$ as well.

With a “classic” linked list, we can only move *forward* through the list. That is, we can access the first node and follow the links to find all the other nodes of the list. But we’re not able to move backward, as no node is aware of what the previous node is.

A doubly linked list allows for a lot more flexibility, as we can move both for- ward *and* backward through the list. In fact, we can even start with the last node and work our way backward to the first node.

### Queues as double linked lists

Because doubly linked lists have immediate access to both the front and end of the list, they can insert data on either side at $$O(1)$$ as well as delete data on either side at $$O(1)$$.

Because doubly linked lists can insert data at the end in $$O(1)$$ time and delete data from the front in $$O(1)$$ time, *they make the perfect underlying data structure for a queue.*

We looked at Queues and you’ll recall that they are lists of items in which data can only be inserted at the end and removed from the beginning. You learned there that queues are an example of an abstract data type, and that we were able to use an array to implement them under the hood.

Now, since queues insert at the end and delete from the beginning, arrays are only so good as the underlying data structure. While arrays are $$O(1)$$ for insertions at the end, they’re $$O(N)$$ for deleting from the beginning.

A doubly linked list, on the other hand, is $$O(1)$$ for both inserting at the end *and* for deleting from the beginning. That’s what makes it a perfect fit for serving as the queue’s underlying data structure.

## Conclusion

As we’ve seen, the subtle differences between arrays and linked lists unlock new ways to make our code faster than ever.

By looking at linked lists, you’ve also learned the concept of nodes. However, the linked list is only the simplest of node-based data structures. In the next chapters, you’ll learn about node-based structures that are both more complex and more interesting—and will reveal new worlds about how nodes can yield tremendous power and efficiency.

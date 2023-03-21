# Binary search trees

While we can use a sorting algorithm such as Quicksort to arrange our data into perfect ascending order, this has a cost. We’ve seen that even the fastest algorithms take $O(N log N)$ time. So, if we want our data sorted often, keep it in sorted order in the first place so that we never need to resort to it. An ordered array is a simple but effective tool for keeping data in order. It’s also fast for certain operations, as it has O(1) reads and $O(log N)$ searches (when using binary search). However, ordered arrays are relatively slow regarding insertions and deletions. Whenever a value is inserted into an ordered array, we shift all greater values to one cell to the right. Similarly, when a value is deleted from an ordered array, we shift all greater values to one cell to the left. This takes N steps in a worst-case scenario (inserting into or deleting from the first cell of the array), and $N/2$ steps on average. Either way, it’s $O(N)$, and $O(N)$ is relatively slow for a simple insertion or deletion. Now, a hash table is a great choice if we are looking for a data structure that delivers all-around amazing speed. They are $O(1)$ for search, insertion, and deletion. However, they do not maintain order, which we need for our alphabetized-list application.

## Trees

The previous chapter introduced you to node-based data structures with linked lists. In a classic linked list, each node contains a link connecting the node to another node. A *tree* is also a node-based data structure, but each node can have links to multiple nodes within a tree.

<img width="494" alt="image" src="https://user-images.githubusercontent.com/11669149/226488478-0e5bc106-3568-47f3-9a00-35b812787862.png">

In this example, each node has links that lead to two other nodes. For simplicity's sake, we can visually represent this tree without showing all the memory addresses.

<img width="186" alt="image" src="https://user-images.githubusercontent.com/11669149/226488617-d64fac60-bfea-4f03-9a8a-3825506abd92.png">

### Tree characteristics

- The uppermost node (in our example, the “j”) is called the *root.* Yes, in our picture, the root is at the *top* of the tree; it’s how trees are typically depicted.
- In our example, we’d say that the “j” is a *parent* to “m” and “b.” Conversely, “m” and “b” are *children* of “j.” Similarly, the “m” is a parent of “q” and “z,” and “q” and “z” are children of “m".
- As in a family tree, a node can have *descendants* and *ancestors.* A node’s descendants are *all* the nodes that stem from a node, while a node’s ancestors are *all* the nodes it stems from. In our example, the “j” is the ancestor of all the other nodes in the tree, and all the other nodes are, therefore, the descendants of the “j”.
- Trees are said to have *levels.* Each level is a row within the tree. Our example tree has three levels:
- One property of a tree is how *balanced* it is. A tree is balanced when its nodes’ subtrees have the same number of nodes in it.
- For instance, the above tree is said to be perfectly balanced. If you look at each node, its two subtrees have the same number of nodes. The root node (“j”) has two subtrees, which each contain three nodes. You’ll see that the same is true for every node in the tree as well. For example, the “m” node also has two subtrees where the two subtrees each contain one node.
- The following tree, on the other hand, is *imbalanced:*

<img width="176" alt="image" src="https://user-images.githubusercontent.com/11669149/226488990-b169957b-e794-4635-9dc2-863dfa026254.png">

## Binary search trees

There are many different kinds of tree-based data structures, but in this chapter, we’ll focus on a particular tree known as a *binary search tree.*

A *binary* tree is a tree in which each node has zero, one, or two children. A binary *search* tree is a binary tree that also abides by the following rules:

- Each node can have at most one “left” child and one “right” child.
- A node’s “left” descendants can only contain values less than the node itself. Likewise, a node’s “right” descendants can only contain values greater than the node itself.

Here’s an example of a binary search tree, in which the values are numbers:

<img width="208" alt="image" src="https://user-images.githubusercontent.com/11669149/226489382-8f5b463e-e4ad-4798-88d1-67b5e1f62402.png">

Note that each node has one child with a lesser value than itself, which is depicted using a left arrow, and one child with a greater value than itself, which is depicted using a right arrow.

Additionally, notice that all of the 50’s left descendants are less than it. At the same time, all of the 50’s right descendants are greater than it. The same pattern goes for each and every node.

While the following example is a binary tree, it is not a binary *search* tree:

<img width="95" alt="image" src="https://user-images.githubusercontent.com/11669149/226489737-0beedd39-5c78-4166-ae55-711f30a164f4.png">

It’s a binary tree because each node has zero, one, or two children. But it’s not a binary *search* tree because the root node has two “left” children. That is, it has two children than are less than it. For a binary search tree to be valid, it can have at most one left (lesser) child and one right (greater) child.

### Example code - Binary search tree

```python
class TreeNode:
def __init__(self,val,left=None,right=None):
        self.value = val
        self.leftChild = left
        self.rightChild = right

node1 = TreeNode(25)
node2 = TreeNode(75)
root = TreeNode(50, node1, node2)
```

### Searching

Take a look at the following example.

<img width="208" alt="image" src="https://user-images.githubusercontent.com/11669149/226489382-8f5b463e-e4ad-4798-88d1-67b5e1f62402.png">

The algorithm for searching within a binary search tree is as follows:

1. Designate a node to be the “current node.” (At the beginning of the algorithm, the root node is the first “current node.”)
2. Inspect the value at the current node.
3. If we’ve found the value we’re looking for, great!
4. If the value we’re looking for is less than the current node, search for it in its left subtree.
5. If the value we seek is greater than the current node, search for it in its right subtree.
6. Repeat Steps 1 through 5 until we find the value we’re searching for, or until we hit the bottom of the tree, in which case our value must not be in the tree.

#### Example

Say we want to search for the 61. Let’s see how many steps it would take to walk through this visually. Apply the above-mentioned algorithm. This example took us four steps to find our desired value.

<img width="506" alt="image" src="https://user-images.githubusercontent.com/11669149/226491501-eceaea21-3ade-421c-a5d3-e4c584fa6750.png">

### The Efficiency of Searching a Binary Search Tree

Looking at the steps we just walked through, you’ll notice that each step eliminates half of the remaining nodes from our search. For example, when we begin our search, we start at the root node, and our desired value may be found among any of the root’s descendants. However, when we then decide to continue the search with, say, the root’s right child, we eliminate the left child and *all of its descendants* from the search.

We’d say that searching in a binary search tree is $O(log N)$, which is the apt description for any algorithm that eliminates half of the remaining values with each step. (We’ll see soon, though, that this is only for a perfectly balanced binary search tree, which is a best-case scenario.)

Here’s yet another way of describing why search in a binary search tree is O(log N), which will reveal another property about binary trees in general: *if there are N nodes in a balanced binary tree, there will be about log N levels (that is, rows).*

To understand this, let’s assume each row in the tree is completely filled with nodes, and that there aren’t any empty positions. If you think about it, each time we add a new full level to the tree, we end up roughly doubling the number of nodes that the tree has. (Really, we’re doubling the nodes and adding one.)

For example, a binary tree with four complete levels has 15 nodes. (Go ahead, count them.) If we add a fifth complete level, that means we add two children to each of the eight nodes in the fourth level. This means we add 16 new nodes, roughly doubling the size of the tree.

It emerges that each new level doubles the size of the tree. Accordingly, *a tree containing N nodes will require log(N) levels* to hold all the nodes.

In the context of binary search, we noted that the pattern of log(N) is that we can eliminate half of the remaining data with each step of the search. The number of levels needed in a binary tree also follows this pattern.

Let’s take a binary tree that needs to hold 31 nodes. With our fifth level, we can hold 16 of those nodes. This took care of roughly half of the data, leaving us with just 15 nodes we still need to find room for. With the fourth level, we take care of eight nodes, leaving seven unaccounted for. With the third level, we take care of four nodes, and so on.

Indeed, log 31 is (approximately) 5. So, we’ve now concluded that a balanced tree with N nodes will have log(N) levels.

Since this is the case, it makes a lot of sense as to why searching a binary search tree takes up to log(N) steps: because each step of the search causes us to move down a level, we take up to as many steps as there are levels in the tree.

However, you prefer to think about it, searching a binary search tree takes O(log N).

Now, while search in a binary search tree is O(log N), so is binary search within an ordered array, in which each number we select eliminates half of the remaining possible values. In this regard, searching a binary search tree has the same efficiency as a binary search within an ordered array.

### Insertion

Binary search trees are at their best when it comes to insertion. Now we’ll see why.

Say we want to insert the number 45 into our example tree. First, we’d have to find the correct node to attach the 45 to. To begin our search, we start at the root:

<img width="341" alt="image" src="https://user-images.githubusercontent.com/11669149/226496144-e383aa91-bb66-4b2d-9bf6-38f7f8e4ac9a.png">

Since 45 is less than 50, we drill down to the left child:

<img width="230" alt="image" src="https://user-images.githubusercontent.com/11669149/226496184-a1f4f0a3-f5c6-4020-8167-b8e39fa82e5a.png">

Since 45 is greater than 25, we must inspect the right child:

<img width="216" alt="image" src="https://user-images.githubusercontent.com/11669149/226496235-8cf5d9fd-340e-4930-8bb3-ab810066c481.png">

Since 45 is greater than 33, we check the 33’s right child:

<img width="191" alt="image" src="https://user-images.githubusercontent.com/11669149/226496281-e6466350-3db5-4cc7-ad8f-a679437b63c4.png">

At this point, we’ve reached a node that has no children, so we have nowhere to go. This means we’re ready to perform our insertion.

Since 45 is greater than 40, we insert it as a right child of the 40:

<img width="210" alt="image" src="https://user-images.githubusercontent.com/11669149/226496408-3890318a-825a-4e51-8c64-1f1ac9f4ff69.png">

In this example, insertion took five steps, consisting of four search steps plus one insertion step. Insertion always takes just one extra step beyond a search, which means insertion takes $(log N) + 1$ steps. In Big O Notation, which ignores constants, this is $O(log N)$.

In an ordered array, by contrast, insertion takes $O(N)$, because in addition to search, we must shift a lot of data to the right to make room for the value we’re inserting.

> **This is what makes binary search trees so efficient. While ordered arrays have $O(log N)$ search and $O(N)$ insertion, binary search trees have $O(log N)$ search *and* $O(log N)$ insertion. This becomes critical in an application where you anticipate many changes to your data.**

#### Balanced vs imbalanced trees

Only when creating a tree out of randomly sorted data do trees usually wind up being well-balanced. However, if we insert *sorted* data into a tree, it can become imbalanced and less efficient. For example, if we were to insert the following data in this order—1, 2, 3, 4, 5—we’d end up with a tree that looks like this:

<img width="126" alt="image" src="https://user-images.githubusercontent.com/11669149/226497308-2feaf119-e644-4fcc-b10c-6bedd026821a.png">

This tree is completely linear, so searching for the 5 within this tree would take $O(N)$.

However, if we inserted the same data in the following order—3, 2, 4, 1, 5—the tree would be evenly balanced:

<img width="113" alt="image" src="https://user-images.githubusercontent.com/11669149/226497381-225735f5-b246-4e57-b033-317eb71cd8a6.png">

Only with a balanced tree does the search take $O(log N)$.

Because of this, if you ever want to convert an ordered array into a binary search tree, you’d better first randomize the order of the data.

> **It emerges that in a worst-case scenario, when a tree is completely *imbalanced,* the search is $O(N)$. In a best-case scenario, when it is perfectly balanced, the search is $O(log N)$. In the typical scenario where data is inserted randomly, a tree will be well-balanced, and the search will take about $O(log N)$.**

### Deletion

Deletion is the least straightforward operation within a binary search tree and requires some careful maneuvering.

The deletion algorithm follows these rules:

- If the node being deleted has no children, simply delete it.

- If the node being deleted has one child, delete the node and plug the child

  into the spot where the deleted node was.
- When deleting a node with two children, replace the deleted node with the *successor* node. The successor node is the child node whose value is the least of all values greater than the deleted node.
- To find the successor node: visit the right child of the deleted value, and then keep on visiting the left child of each subsequent child until there are no more left children. The bottom value is the successor node.
- If the successor node has a right child, after plugging the successor node into the spot of the deleted node, take the former right child of the suc- cessor node and turn it into the *left child of the former parent of the suc- cessor node.*

Let’s say we want to delete the 4 from this binary search tree:

<img width="213" alt="image" src="https://user-images.githubusercontent.com/11669149/226500611-af3c0ea0-cb91-478a-a69c-9343066d5497.png">

<img width="228" alt="image" src="https://user-images.githubusercontent.com/11669149/226500897-6a9db5dc-67f2-45d7-80b6-02b27aacca92.png">

Well, that was simple. But let’s see what happens when we try to delete the 10:

<img width="203" alt="image" src="https://user-images.githubusercontent.com/11669149/226500986-4f1ec99c-5760-4bb3-8658-13e89da4f1c7.png">

<img width="205" alt="image" src="https://user-images.githubusercontent.com/11669149/226501018-27825e36-fda0-4a6c-b6ef-0afece6e07a4.png">

#### Deleting a node with two children

Deleting a node that has two children is the most complex scenario. Let’s say we want to delete the 56 in this tree:

<img width="188" alt="image" src="https://user-images.githubusercontent.com/11669149/226501283-fa9837d5-8a96-4cd1-90fe-19e2508a9e98.png">

<img width="190" alt="image" src="https://user-images.githubusercontent.com/11669149/226501505-81c7d25f-1739-4ac5-8516-4e0b69605434.png">

#### Find the successor node

How does the computer find the successor node? Deleting a node high up in the tree can be tricky.

Here’s the algorithm for finding the successor node:

- Visit the right child of the deleted value, and then keep on visiting the left child of each subsequent child until there are no more left children. The bottom value is the successor node.

<img width="205" alt="image" src="https://user-images.githubusercontent.com/11669149/226501815-4f4c4dcb-b9e1-4f26-9bab-45e8bd355c59.png">

<img width="207" alt="image" src="https://user-images.githubusercontent.com/11669149/226502363-a0f839c1-e9f5-4f97-9171-2430629f9765.png">

<img width="212" alt="image" src="https://user-images.githubusercontent.com/11669149/226502416-b6e984bd-78ed-419a-b602-cba774287f8e.png">

##### Successor node with a right child

However, there is one case we haven’t accounted for yet, and that’s where the successor node has a right child of its own. Let’s recreate the preceding tree, but add a right child to the 52 as shown in the diagram below.

<img width="320" alt="image" src="https://user-images.githubusercontent.com/11669149/226514688-b6baaec4-38cd-4cbf-989d-9b7bb828ae6a.png">

<img width="303" alt="image" src="https://user-images.githubusercontent.com/11669149/226514798-25e9f3c9-fdb2-48b5-8e47-c13d1c63113a.png">

<img width="191" alt="image" src="https://user-images.githubusercontent.com/11669149/226514875-f41e237a-5132-4b32-a1f9-7e227d2ef9a7.png">



> **Like search and insertion, deleting from trees is typically $O(log N)$. Deletion requires a search and a few extra steps for hanging children. Contrast this with deleting a value from an ordered array, which is $O(N)$ due to shifting elements to the left to close the gap of the deleted value.**

### Conclusion

The binary search tree is a powerful node-based data structure that maintains order and fast search, insertion, and deletion. It’s more complex than its linked list cousin but offers tremendous value.

However, the binary search tree is just one type of tree. There are many kinds of trees, each bringing unique advantages to specialized situations. 
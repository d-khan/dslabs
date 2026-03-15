# Linked Lists in C++

## 1. Introduction

A **linked list** is a dynamic data structure consisting of a sequence
of elements called **nodes**, where each node contains:

1.  **Data** -- the value stored in the node
2.  **Pointer (link)** -- the address of the next node in the sequence

Unlike arrays, elements in a linked list **are not stored in contiguous
memory locations**.
Instead, nodes are connected using pointers.

    Head → [10 | * ] → [25 | * ] → [40 | * ] → [65 | nullptr]

Each node stores a value and a pointer to the **next node**.

------------------------------------------------------------------------

# 2. Why Linked Lists?

Linked lists solve several limitations of arrays.

### Arrays

-   Fixed size
-   Requires contiguous memory
-   Expensive insertions/deletions in the middle

### Linked Lists

-   Dynamic size
-   Efficient insertions and deletions
-   No need for contiguous memory


------------------------------------------------------------------------

# 3. Structure of a Node

In C++, a node is typically represented using a **struct or class**.

``` cpp
struct Node
{
    int data;
    Node* next;
};
```

Each node contains:

    data → stored value
    next → pointer to next node

------------------------------------------------------------------------

# 4. Creating a Node

Nodes are typically created dynamically using `new`.

``` cpp
Node* newNode = new Node;

newNode->data = 10;
newNode->next = nullptr;
```

Or more compactly:

``` cpp
Node* newNode = new Node{10, nullptr};
```

------------------------------------------------------------------------

# 5. The Head Pointer

A linked list is accessed through a pointer called the **head**.

    head → first node

Example:

``` cpp
Node* head = nullptr;
```

When the list is empty:

    head → nullptr

------------------------------------------------------------------------

# 6. Creating a Simple Linked List

Example list:

    10 → 20 → 30

``` cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* next;
};

int main()
{
    Node* head = new Node{10, nullptr};
    Node* second = new Node{20, nullptr};
    Node* third = new Node{30, nullptr};

    head->next = second;
    second->next = third;

    return 0;
}
```

Memory layout:

    head → [10 | * ] → [20 | * ] → [30 | nullptr]

------------------------------------------------------------------------

# 7. Traversing a Linked List

Traversal means visiting each node sequentially.

``` cpp
void printList(Node* head)
{
    Node* temp = head;

    while (temp != nullptr)
    {
        cout << temp->data << " ";
        temp = temp->next;
    }
}
```

Time complexity:

    O(n)

------------------------------------------------------------------------

# 8. Inserting at the Beginning

    Before:
    
    head → 20 → 30
    
    After inserting 10:
    
    head → 10 → 20 → 30

``` cpp
void insertFront(Node*& head, int value)
{
    Node* newNode = new Node{value, head};
    head = newNode;
}
```

Time complexity:

    O(1)

------------------------------------------------------------------------

# 9. Inserting at the End

``` cpp
void insertEnd(Node*& head, int value)
{
    Node* newNode = new Node{value, nullptr};

    if (head == nullptr)
    {
        head = newNode;
        return;
    }

    Node* temp = head;

    while (temp->next != nullptr)
        temp = temp->next;

    temp->next = newNode;
}
```

Time complexity:

    O(n)

------------------------------------------------------------------------

# 10. Inserting at a Specific Position

    10 → 20 → 30
    Insert 25 at position 3
    
    10 → 20 → 25 → 30

``` cpp
void insertAt(Node*& head, int value, int pos)
{
    Node* newNode = new Node{value, nullptr};

    if (pos == 1)
    {
        newNode->next = head;
        head = newNode;
        return;
    }

    Node* temp = head;

    for (int i = 1; i < pos - 1; i++)
        temp = temp->next;

    newNode->next = temp->next;
    temp->next = newNode;
}
```

------------------------------------------------------------------------

# 11. Deleting a Node

### Delete first node

    Before:
    
    head → 10 → 20 → 30
    
    After:
    
    head → 20 → 30

``` cpp
void deleteFront(Node*& head)
{
    if (head == nullptr)
        return;

    Node* temp = head;
    head = head->next;
    delete temp;
}
```

------------------------------------------------------------------------

# 12. Searching a Linked List

``` cpp
bool search(Node* head, int key)
{
    Node* temp = head;

    while (temp != nullptr)
    {
        if (temp->data == key)
            return true;

        temp = temp->next;
    }

    return false;
}
```

Time complexity:

    O(n)

------------------------------------------------------------------------

# 13. Complexity Analysis

| Operation       | Time Complexity |
| --------------- | --------------- |
| Access by index | O(n)            |
| Search          | O(n)            |
| Insert at front | O(1)            |
| Insert at end   | O(n)            |
| Delete          | O(n)            |

------------------------------------------------------------------------

# 14. Types of Linked Lists

### Singly Linked List

    10 → 20 → 30 → nullptr

Each node points to the **next node only**.

------------------------------------------------------------------------

### Doubly Linked List

    nullptr ← 10 ⇄ 20 ⇄ 30 → nullptr

``` cpp
struct Node
{
    int data;
    Node* next;
    Node* prev;
};
```

Advantages: - Traversal in both directions - Easier deletion

------------------------------------------------------------------------

### Circular Linked List

    10 → 20 → 30
    ↑         ↓
    ← ← ← ← ←
    
    last->next = head

Used in: - Round-robin scheduling - Cyclic buffers

------------------------------------------------------------------------

# 15. Memory Layout

Unlike arrays:

    Array
    
    [10][20][30][40]

Linked lists:

    Address  Data   Next
    0x1010   10     0x3050
    0x3050   20     0x1F20
    0x1F20   30     nullptr

------------------------------------------------------------------------

# 16. Comparison with Arrays

| Feature         | Array      | Linked List    |
| --------------- | ---------- | -------------- |
| Memory layout   | Contiguous | Non-contiguous |
| Size            | Fixed      | Dynamic        |
| Access time     | O(1)       | O(n)           |
| Insert/Delete   | Expensive  | Efficient      |
| Memory overhead | Low        | Higher         |

------------------------------------------------------------------------

# 17. When to Use Linked Lists

Linked lists are useful when:

-   Frequent insertions/deletions occur
-   Data size is dynamic
-   Memory reallocation should be avoided

Typical uses:

-   Hash table chaining
-   Graph adjacency lists
-   Memory management systems

------------------------------------------------------------------------

# 18. C++ Standard Library Linked List

``` cpp
#include <list>
#include <iostream>
using namespace std;

int main()
{
    list<int> numbers;

    numbers.push_back(10);
    numbers.push_back(20);
    numbers.push_back(30);

    for (int n : numbers)
        cout << n << " ";
}
```

Output:

    10 20 30

------------------------------------------------------------------------

# 19. Key Takeaways

-   Linked lists are **dynamic pointer-based data structures**
-   Each node contains **data and a pointer**
-   They allow **efficient insertion and deletion**
-   They do **not support constant-time random access**
-   Common variants include **singly, doubly, and circular linked
    lists**

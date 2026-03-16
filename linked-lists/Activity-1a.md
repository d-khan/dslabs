# Implementing a Stack Using a Linked List in C++

## Learning Objectives
By completing this lab, students will:

- Understand the **Last-In First-Out (LIFO)** behavior of stacks
- Implement a **stack data structure using a singly linked list**
- Practice **dynamic memory allocation**
- Manipulate **pointer logic safely in C++**
- Implement fundamental stack operations

## Pre-requisite
Review [Linked lists](https://htmlpreview.github.io/?https://github.com/d-khan/dslabs/blob/main/linked-lists/Linked%20lists.html) contents.  
Review [Linked lists in C++](https://github.com/d-khan/dslabs/blob/main/linked-lists/linked_lists_cpp_lecture.md)

# Stack Operations to Implement

| Operation | Description |
|----------|-------------|
| push() | Insert element on top |
| pop() | Remove top element |
| peek() | Return top element |
| isEmpty() | Check if stack is empty |
| display() | Print stack contents |

---

# Part 1: Define the Node Structure

Create the following structure.

```cpp
struct Node
{
    int data;
    Node* next;
};
```

---

# Part 2: Create the Stack Class

Create a class called `Stack`.

```cpp
class Stack
{
private:
    Node* top;

public:
    Stack();

    void push(int value);
    void pop();
    int peek();
    bool isEmpty();
    void display();
};
```

---

# Part 3: Implement the Constructor

The constructor should initialize the stack as empty.

```cpp
Stack::Stack()
{
    top = nullptr;
}
```

---

# Part 4: Implement push()

The `push()` operation:

1. Create a new node
2. Set its next pointer to current top
3. Update top pointer

Example:

```
Before push(40)

Top → 30 → 20 → 10

After push(40)

Top → 40 → 30 → 20 → 10
```

---

# Part 5: Implement pop()

The `pop()` operation:

1. Check if stack is empty
2. Remove the top node
3. Update the top pointer
4. Free the memory

Example:

```
Before pop()

Top → 40 → 30 → 20 → 10

After pop()

Top → 30 → 20 → 10
```

---

# Part 6: Implement peek()

`peek()` should return the value stored in the **top node**.

Example:

```
Top → 40 → 30 → 20

peek() returns 40
```

---

# Part 7: Implement isEmpty()

Return `true` if:

```
top == nullptr
```

Otherwise return `false`.

---

# Part 8: Implement display()

Display the stack from **top to bottom**.

Example output:

```
Stack elements:

40
30
20
10
```

---

# Part 9: Driver Program

Create a test program in `main()`.

Example test:

```cpp
int main()
{
    Stack s;

    s.push(10);
    s.push(20);
    s.push(30);
    s.push(40);

    s.display();

    s.pop();

    cout << "Top element: " << s.peek() << endl;

    s.display();

    return 0;
}
```

Expected output:

```
Stack elements:
40
30
20
10

Top element: 30

Stack elements:
30
20
10
```

---

# Part 10: Additional Requirement

Your program must handle **stack underflow**.

Example:

```
Pop from empty stack
```

Output:

```
Stack Underflow
```

---

# Submission Requirements

| File | Description |
|-----|-------------|
| stack.h | Stack class definition |
| stack.cpp | Stack implementation |
| main.cpp | Test program |
| README.md | Explanation of stack implementation |

---

# Reflection Questions

Answer the following questions in your README.

1. Why is a linked list efficient for stack implementation?
2. What is the time complexity of push and pop operations?
3. What happens if memory is not deallocated after pop?
4. Compare a stack implemented with an array versus a linked list.

---

# Grading Rubric

| Criteria | Excellent | Good | Needs Improvement | Points |
|--------|-----------|------|------------------|-------|
| Node Structure | Correct implementation | Minor issues | Incorrect structure | 1 |
| push() Implementation | Correct pointer logic | Minor logic errors | Incorrect | 2 |
| pop() Implementation | Correct memory handling | Minor errors | Incorrect | 2 |
| peek() and isEmpty() | Correct behavior | Minor issues | Incorrect | 1 |
| display() Function | Correct traversal | Minor formatting issues | Incorrect | 1 |
| Driver Program | Fully tests stack operations | Limited testing | Missing | 1 |
| Code Quality | Clear, readable, commented | Some comments | Poor readability | 1 |
| Reflection Questions | Complete and thoughtful | Partial answers | Missing | 1 |

**Total Points: 10**

---

# Challenge

Modify the program to implement:

```
template<class T>
class Stack
```

So the stack works for:

```
Stack<int>
Stack<double>
Stack<string>
```

## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://sdccd-edu.zoom.us/rec/play/SVjSkOJp16n_7ii-oRt1-9auud9NZ0NrhuXrnJYf-bcQP5ipZbGONd6Jxt7h1jns5OJKIq9lgjAuBw.Tc2b6f-qrSDM8aye?eagerLoadZvaPages=sidemenu.billing.plan_management&accessLevel=meeting&canPlayFromShare=true&from=share_recording_detail&startTime=1725121532000&componentName=rec-play&originRequestUrl=https%3A%2F%2Fsdccd-edu.zoom.us%2Frec%2Fshare%2FSVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX%3FstartTime%3D1725121532000)” before submission.

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.


# Performance evaluation

a) Use 100, 200, and 300 million elements of the same data type to compare arrays' and linked-lists' performances using C++. You might have to use profiling. 
Please research how to profile a code in C++. Evaluate the performance in terms of time and space.

For example, add elements at the beginning of the array and linked lists and  compare. Similarly, add elements at the end of the array, such as linked lists, and 
compare. The same applies to removing elements from arrays and linked lists and comparing them.

b) Compare loop iterators; for example, compare for and while loops. See the code below. 

```
for (int i = 0; i < authorsList.size(); i++) {
            authorName = authorsList.get(i);
            System.out.println(authorName);
        }

while (listIterator.hasNext()) {
            authorName = listIterator.next();
            System.out.println(authorName);
        }

```

Compare both the iterators and observe the performance. The performance is in terms  of time. The profiling code/engine itself has an overhead on the code you are evaluating. 
Make sure you include this when evaluating the performance. The documentation of parts a and b together should not exceed two pages. Use graphs where applicable and explain the findings clearly.

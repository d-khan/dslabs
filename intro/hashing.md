# Implementing a Hash Table with Separate Chaining

## Objective
By completing this lab, you will:

-   Implement a hash table from scratch in C++
-   Understand collision handling using separate chaining
-   Compute and analyze load factor
-   Implement dynamic resizing (rehashing)
-   Evaluate performance experimentally

## Pre-requisite
Review "Hash Tables" from the book [Data Structures in C++](https://d-khan.github.io/ds)

##  Problem Overview

You will implement a `HashTable` class that stores:

-   **string keys**
-   **int values**

You are NOT allowed to use:

-   `std::unordered_map`
-   `std::map`

You must implement the data structure manually.

## Part 1 -- Class Structure

Use the following internal structure:

```cpp
#include <vector>
#include <list>
#include <string>
using namespace std;

class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;

    int hashFunction(const string& key) const;
    void rehash();

public:
    HashTable(int size = 11);

    void insert(const string& key, int value);
    bool remove(const string& key);
    int search(const string& key) const;
    double loadFactor() const;
    int size() const;
    bool isEmpty() const;
    void printTable() const;
};
```

------------------------------------------------------------------------

##  Part 2 -- Hash Function

Implement a polynomial rolling hash:

```cpp
int HashTable::hashFunction(const string& key) const {
    const int prime = 31;
    long long hash = 0;

    for (char c : key) {
        hash = hash * prime + c;
    }

    return hash % capacity;
}
```

## Part 3 -- Insert & Collision Handling

-   Use separate chaining (`vector<list<>>`)
-   If inserting into a non-empty bucket, increment `collisionCount`
-   If key already exists, update value instead of duplicating

## Part 4 -- Resizing (Rehashing)

When:

    loadFactor() > 0.75

You must:

1.  Double the table capacity
2.  Reinsert all existing elements
3.  Reset collision counter appropriately

## Part 5 -- Testing Program

In `main()`:

1.  Insert at least 100 words
2.  Print:
    -   Table capacity
    -   Number of elements
    -   Load factor
    -   Total collisions
3.  Search for:
    -   Existing key
    -   Non-existing key
4.  Remove some keys and verify correctness

## Part 6 -- Experimental Analysis

Test three input types:

1.  Random strings  
2.  Sequential keys (e.g., student1, student2, ...)  
3.  Same prefix keys (e.g., data_0001, data_0002, ...)

Record:

-   Total collisions
-   Maximum bucket size
-   Average bucket length

Write a short explanation (1--2 paragraphs) describing what you observe.

## Important Notes

-   Using `std::unordered_map` results in major deduction
-   Emphasis is on correctness and understanding

# Grading Rubric (Total: 10 Points)

| Category                       | Points | Expectations                                     |
| ------------------------------ | ------ | ------------------------------------------------ |
| Correct Hash Table Structure   | 2      | Proper class design and internal storage         |
| Hash Function Implementation   | 2      | Correct polynomial hash and modulo usage         |
| Insertion & Collision Handling | 2      | Correct chaining and collision counting          |
| Search & Remove Operation      | 1.5    | Correct functionality without breaking structure |
| Load Factor & Resizing         | 1.5    | Proper threshold check and rehash logic          |
| Testing & Code Quality         | 1      | Demonstration functionality                      |


## What/how to submit?  
- Write your responses in a markdown file along with the code, upload the file to GitHub, and submit the GitHub link in Canvas. Use **appropriate headings to differentiate tasks**. Please review the guide “[Submitting Your Assignment Using GitHub](https://sdccd-edu.zoom.us/rec/play/SVjSkOJp16n_7ii-oRt1-9auud9NZ0NrhuXrnJYf-bcQP5ipZbGONd6Jxt7h1jns5OJKIq9lgjAuBw.Tc2b6f-qrSDM8aye?eagerLoadZvaPages=sidemenu.billing.plan_management&accessLevel=meeting&canPlayFromShare=true&from=share_recording_detail&startTime=1725121532000&componentName=rec-play&originRequestUrl=https%3A%2F%2Fsdccd-edu.zoom.us%2Frec%2Fshare%2FSVvlngcEn-7CaNI8FvwEVJ5ulLp4sxpqN9hnCYvXeHHcls2e0TBlU47uATNklUf-.yX4fsJjsU2nuLGeX%3FstartTime%3D1725121532000)” before submission.
- No video is required. 

## Deadline
The deadlines are posted on the Syllabus as well as on Canvas.

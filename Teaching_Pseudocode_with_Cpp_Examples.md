# How to Write Pseudocode (For C++ Programming)

## 1. What is Pseudocode?

Pseudocode is a structured, language-independent way of describing an algorithm before writing actual code.

It helps you

- Focus on logic
- Avoid syntax errors
- Think step-by-step
- Separate algorithm design from C++ syntax

Think of pseudocode as the blueprint and C++ as the construction.

------------------------------------------------------------------------

## 2. Why Use Pseudocode in C++?

People often struggle because they:

- Think about syntax first
- Forget algorithm structure
- Mix logic with formatting issues

Pseudocode forces you to identify

- Variables 
- Input
- Processing steps
- Decisions
- Loops
- Output

------------------------------------------------------------------------

## 3. General Structure of Good Pseudocode

A clean pseudocode usually follows this structure:

```txt
START

DECLARE variables

INPUT data

PROCESS data

IF / WHILE / FOR (if needed)

OUTPUT result

END
```

**Key characteristics**

- No semicolons 
- No curly braces
- No #include statements
- Use indentation
- Use clear keywords

------------------------------------------------------------------------

## 4. Common Pseudocode Keywords

------------ ---------------------
| Pseudocode | Meaning in C++      |
| ---------- | ------------------- |
| DECLARE    | int, double, etc.   |
| READ       | cin >>              |
| PRINT      | cout <<             |
| SET        | assignment (=)      |
| IF         | if                  |
| ELSE       | else                |
| WHILE      | while               |
| FOR        | for                 |
| FUNCTION   | function definition |
| RETURN     | return              |

------------------------------------------------------------------------

# Example 1 --- Conditional Statement

## Problem

Ask the user to enter a number. If the number is positive, print "Positive". If negative, print "Negative". Otherwise, print "Zero".

## Pseudocode

```txt
START

DECLARE number

PRINT "Enter a number:"
READ number

IF number > 0 THEN
    PRINT "Positive"
ELSE IF number < 0 THEN
    PRINT "Negative"
ELSE
    PRINT "Zero"
END IF

END
```

------------------------------------------------------------------------

## Equivalent C++ Code

``` cpp
#include <iostream>
using namespace std;

int main() {
    int number;

    cout << "Enter a number: ";
    cin >> number;

    if (number > 0) {
        cout << "Positive" << endl;
    }
    else if (number < 0) {
        cout << "Negative" << endl;
    }
    else {
        cout << "Zero" << endl;
    }

    return 0;
}
```



# 1. What is a function?

A **function** is a named, reusable block of code that performs a particular task.

Examples of tasks:
- Print a welcome message.
- Add two numbers.
- Calculate the square of a number.
- Find the factorial of a number.

Instead of writing the same code many times, write it once inside a function and call it whenever needed.

## Function: input → work → output

A function may receive input (arguments), perform work, and return a result.

```text
       Calling code
            |
            | sends arguments
            v
    +-------------------+
    |      FUNCTION     |
    |                   |
    |  1. Take input    |
    |  2. Do the work   |
    |  3. Return result |
    +-------------------+
            |
            | result (if return type is not void)
            v
       Calling code
```

Example in everyday terms:

```text
You give:       10 and 20
Function does:  add the two numbers
Function gives: 30
```

A function does not always need arguments or a return value. For example, a function that only prints `Hello` can use `void`.

## Why do we use functions?

1. **Code reusability:** write code once and call it many times.
2. **Modularity:** divide a large program into smaller tasks.
3. **Readability:** meaningful function names explain what code does.
4. **Testing and debugging:** individual tasks are easier to test.
5. **Maintenance:** a change can often be made in one place.

---

# 2. Basic function syntax

```c
return_type function_name(parameter_list) {
    // statements: work performed by the function
    return value; // only when appropriate for the return type
}
```

Understand each part:

| Part | Meaning |
|---|---|
| `return_type` | Type of value returned, such as `int`, `float`, or `void` |
| `function_name` | Name used to call the function |
| `parameter_list` | Inputs received by the function |
| Function body `{ }` | Statements that perform the task |
| `return` | Sends a result back to the caller |

Example:

```c
int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```

- `int`: function returns an integer.
- `add`: function name.
- `int a, int b`: two integer parameters.
- `sum = a + b`: task performed.
- `return sum`: sends the result back.

---

# 3. Three important parts of a function

A normal C function is commonly used through three parts:

1. Function prototype (declaration).
2. Function call.
3. Function definition.

## 3.1 Function prototype — tell the compiler

A **function prototype** tells the compiler the function's name, return type, and parameter types before the function is called.

Syntax:

```c
return_type function_name(parameter_types);
```

Examples:

```c
void printHello(void);
int add(int a, int b);
float calculateArea(float radius);
```

The parameter names in a prototype are optional:

```c
int add(int, int);
```

The semicolon `;` is important because this is a declaration, not the function body.

## 3.2 Function call — use the work

A **function call** transfers control to the function so its statements can execute.

```c
printHello();
int answer = add(10, 20);
```

## 3.3 Function definition — do the work

A **function definition** contains the actual code that performs the task.

```c
void printHello(void) {
    printf("Hello!\n");
}

int add(int a, int b) {
    return a + b;
}
```

## Complete diagram

```text
        FUNCTION IN C
              |
      +-------+-------+
      |       |       |
      v       v       v
  Prototype  Call  Definition
      |       |       |
      v       v       v
 Tell the   Use the  Do the
 compiler   function work
```

## Complete program: print Hello

```c
#include <stdio.h>

// 1. Function prototype
void printHello(void);

int main(void) {
    // 2. Function call
    printHello();

    return 0;
}

// 3. Function definition
void printHello(void) {
    printf("Hello!\n");
}
```

Output:

```text
Hello!
```

### How does this program execute?

```text
Program starts
      |
      v
    main()
      |
      v
 printHello() called
      |
      v
 printHello() executes
      |
      v
 printf("Hello!")
      |
      v
 Return to main()
      |
      v
 return 0
      |
      v
 Program ends
```

**Important:** Execution of a hosted C program begins at `main()`. A function can be called from `main()` or indirectly through another function that `main()` calls.

---

# 4. Function types

Functions can be grouped into two broad categories.

```text
                 C Functions
                     |
          +----------+----------+
          |                     |
          v                     v
   Library functions     User-defined functions
          |                     |
          v                     v
  Provided by C library  Written by programmer
```

## 4.1 Library functions

Library functions are provided by the C standard library (or another library).

Examples:

| Function | Purpose | Header |
|---|---|---|
| `printf()` | Formatted output | `<stdio.h>` |
| `scanf()` | Formatted input | `<stdio.h>` |
| `strlen()` | String length | `<string.h>` |
| `sqrt()` | Square root | `<math.h>` |
| `pow()` | Power | `<math.h>` |

Example:

```c
#include <stdio.h>
#include <math.h>

int main(void) {
    printf("Hello C\n");
    printf("Square root = %.2f\n", sqrt(25.0));
    return 0;
}
```

Expected output:

```text
Hello C
Square root = 5.00
```

Some systems require linking the math library when compiling, for example:

```bash
gcc main.c -o main -lm
```

## 4.2 User-defined functions

These are functions written by the programmer to perform a required task.

```c
#include <stdio.h>

int square(int number) {
    return number * number;
}

int main(void) {
    printf("%d\n", square(5));
    return 0;
}
```

Output:

```text
25
```

---

# 5. Function arguments and parameters

A function can receive values from the calling code.

## 5.1 Argument vs parameter

**Argument:** the actual value or expression passed in a function call.

**Parameter:** the variable declared in the function definition that receives the argument.

```c
int add(int a, int b) { // a and b are parameters
    return a + b;
}

int main(void) {
    int result = add(10, 20); // 10 and 20 are arguments
    return 0;
}
```

Visual:

```text
Function call:
add(10, 20)
     |   |
     v   v
  Argument values
     |   |
     v   v
Function definition:
add(int a, int b)
        |     |
        v     v
    Parameters
```

| Argument | Parameter |
|---|---|
| Value passed in the call | Variable that receives the value |
| Used in the calling expression | Declared in the function definition |
| Example: `10`, `20` | Example: `a`, `b` |

## 5.2 Function with no arguments and no return value

```c
#include <stdio.h>

void printHello(void) {
    printf("Hello!\n");
}

int main(void) {
    printHello();
    printHello();
    return 0;
}
```

Output:

```text
Hello!
Hello!
```

`void` before the function name means it does not return a value. `(void)` means it accepts no parameters.

## 5.3 Function with arguments and no return value

```c
#include <stdio.h>

void printTable(int n) {
    for (int i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", n, i, n * i);
    }
}

int main(void) {
    printTable(5);
    return 0;
}
```

Output:

```text
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
...
5 x 10 = 50
```

Here:
- `5` is the argument.
- `n` is the parameter.
- The function prints the table.
- It does not return a value.

## 5.4 Function with arguments and a return value

```c
#include <stdio.h>

int sum(int a, int b) {
    return a + b;
}

int main(void) {
    int result = sum(10, 20);
    printf("Sum = %d\n", result);
    return 0;
}
```

Output:

```text
Sum = 30
```

The function receives two values and returns one result.

## 5.5 Four common combinations

| Arguments? | Return value? | Example |
|---|---|---|
| No | No | `void greet(void)` |
| Yes | No | `void printTable(int n)` |
| No | Yes | `int getNumber(void)` |
| Yes | Yes | `int add(int a, int b)` |

Examples of each:

```c
#include <stdio.h>

// 1. No arguments, no return value
void greet(void) {
    printf("Welcome!\n");
}

// 2. Arguments, no return value
void printNumber(int n) {
    printf("Number = %d\n", n);
}

// 3. No arguments, returns a value
int getNumber(void) {
    return 100;
}

// 4. Arguments, returns a value
int multiply(int a, int b) {
    return a * b;
}

int main(void) {
    greet();
    printNumber(10);

    int number = getNumber();
    int product = multiply(4, 5);

    printf("Number = %d\n", number);
    printf("Product = %d\n", product);

    return 0;
}
```

Output:

```text
Welcome!
Number = 10
Number = 100
Product = 20
```

---

# 6. Return statement

The `return` statement ends the current function and, when the function has a non-`void` return type, sends a value back to its caller.

```c
int square(int n) {
    return n * n;
}
```

Flow:

```text
main()
  |
  | calls square(4)
  v
square(int n)
  |
  | calculates 4 * 4
  v
return 16
  |
  v
main() receives 16
```

Example:

```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int main(void) {
    int answer = square(4);
    printf("Square = %d\n", answer);
    return 0;
}
```

Output:

```text
Square = 16
```

Important:
- A `void` function does not return a value.
- A non-`void` function should return a value of the declared type on every path where a value is required.
- A function returns one value per return operation. To produce multiple results, use pointers, structures, or another suitable design (covered in later chapters).

---

# 7. Call by value

In C, ordinary function arguments are passed **by value**. This means the function receives a copy of the argument's value.

Changing the parameter does not change the original variable in the calling function.

Example:

```c
#include <stdio.h>

void changeValue(int x) {
    x = 100;
    printf("Inside function: %d\n", x);
}

int main(void) {
    int number = 10;

    changeValue(number);

    printf("Inside main: %d\n", number);
    return 0;
}
```

Output:

```text
Inside function: 100
Inside main: 10
```

## Memory-style diagram

```text
Before function call:

main() memory
+----------------+
| number = 10    |
+----------------+

        |
        | changeValue(number)
        | copy value 10
        v

Function memory
+----------------+
| x = 10         |
+----------------+
        |
        | x = 100
        v
+----------------+
| x = 100        |
+----------------+

main() memory remains unchanged
+----------------+
| number = 10    |
+----------------+
```

The function parameter `x` is a separate object from `number`.

> C does not have traditional pass-by-reference parameters. A program can pass a pointer by value to let a function modify an object in the caller; pointers are explained in Chapter 6.

---

# 8. Reusing a function multiple times

One function can be called many times with different arguments.

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main(void) {
    printf("%d\n", add(2, 3));
    printf("%d\n", add(10, 20));
    printf("%d\n", add(100, 200));

    return 0;
}
```

Output:

```text
5
30
300
```

The function is written once but reused three times.

---

# 9. Recursion

**Recursion** is a programming technique in which a function calls itself to solve a smaller version of the same problem.

A recursive function needs two important parts:

1. **Base case:** the condition that stops further recursive calls.
2. **Recursive case:** the part where the function calls itself with a smaller or simpler input.

## 9.1 Recursion diagram

```text
          factorial(4)
               |
               v
          factorial(3)
               |
               v
          factorial(2)
               |
               v
          factorial(1)
               |
               v
          factorial(0)
               |
               v
          Base case: 1
               |
               v
       Results return upward
```

Without a base case, a recursive function may keep calling itself until the program runs out of call-stack space.

## 9.2 Factorial

Factorial of a non-negative integer `n`:

\[
n! = n \times (n-1) \times \cdots \times 1
\]

Special case:

\[
0! = 1
\]

Recursive definition:

\[
factorial(n) =
\begin{cases}
1 & n = 0 \\
n \times factorial(n-1) & n > 0
\end{cases}
\]

Examples:

```text
0! = 1
1! = 1
2! = 2 x 1 = 2
3! = 3 x 2 x 1 = 6
4! = 4 x 3 x 2 x 1 = 24
5! = 5 x 4 x 3 x 2 x 1 = 120
```

## 9.3 Factorial using recursion — complete program

```c
#include <stdio.h>

// Function prototype
unsigned long long factorial(int n);

int main(void) {
    int n;

    printf("Enter a number (0 to 20): ");
    scanf("%d", &n);

    if (n < 0 || n > 20) {
        printf("Please enter a number from 0 to 20.\n");
    } else {
        printf("Factorial = %llu\n", factorial(n));
    }

    return 0;
}

// Recursive function definition
unsigned long long factorial(int n) {
    // Base case: stop recursion
    if (n == 0) {
        return 1;
    }

    // Recursive case: call factorial with a smaller value
    return (unsigned long long)n * factorial(n - 1);
}
```

Input:

```text
Enter a number (0 to 20): 5
```

Output:

```text
Factorial = 120
```

The limit 20 keeps the result within the range of a typical `unsigned long long`.

## 9.4 Factorial dry run: factorial(4)

First, the function calls itself until it reaches the base case.

**Calling / going down:**

```text
factorial(4)
    |
    v
4 * factorial(3)
        |
        v
    3 * factorial(2)
            |
            v
        2 * factorial(1)
                |
                v
            1 * factorial(0)
                    |
                    v
                return 1
```

Then results return in reverse order.

**Returning / coming up:**

```text
factorial(0) = 1
       |
       v
factorial(1) = 1 * 1 = 1
       |
       v
factorial(2) = 2 * 1 = 2
       |
       v
factorial(3) = 3 * 2 = 6
       |
       v
factorial(4) = 4 * 6 = 24
```

Final result:

```text
factorial(4) = 24
```

## 9.5 What is the call stack?

When a function is called, the program keeps information about that call (such as its local variables and where to return) in a call stack.

Each recursive call creates another active function call. When a base case is reached, calls finish one by one in reverse order.

```text
        Call stack (conceptual)

        +------------------+
Top --> | factorial(0)     |
        +------------------+
        | factorial(1)     |
        +------------------+
        | factorial(2)     |
        +------------------+
        | factorial(3)     |
        +------------------+
        | factorial(4)     |
        +------------------+
        | main()           |
        +------------------+
```

This diagram shows the calls while the base case is active. As each call returns, its stack frame is removed.

Too many recursive calls can cause **stack overflow**. Recursion should have a correct base case and should make progress toward it.

---

# 10. More recursion examples

## 10.1 Sum of numbers from 1 to n

Mathematical idea:

\[
sum(n) = n + sum(n-1)
\]

Base case:

\[
sum(0) = 0
\]

Code:

```c
#include <stdio.h>

int sum(int n) {
    if (n == 0) {
        return 0; // Base case
    }

    return n + sum(n - 1); // Recursive case
}

int main(void) {
    int n = 5;
    printf("Sum = %d\n", sum(n));
    return 0;
}
```

Output:

```text
Sum = 15
```

Call diagram:

```text
sum(5)
  |
  v
5 + sum(4)
      |
      v
  4 + sum(3)
        |
        v
    3 + sum(2)
          |
          v
      2 + sum(1)
            |
            v
        1 + sum(0)
                  |
                  v
                  0
```

Returning result: `1 + 0 = 1`, `2 + 1 = 3`, `3 + 3 = 6`, `4 + 6 = 10`, `5 + 10 = 15`.

## 10.2 Print numbers from 1 to n

```c
#include <stdio.h>

void printNumbers(int n) {
    if (n == 0) {
        return; // Base case
    }

    printNumbers(n - 1);
    printf("%d ", n);
}

int main(void) {
    printNumbers(5);
    printf("\n");
    return 0;
}
```

Output:

```text
1 2 3 4 5
```

Notice that `printf()` comes after the recursive call. This is why the numbers print in ascending order.

## 10.3 Fibonacci number using recursion

The Fibonacci sequence begins:

```text
0, 1, 1, 2, 3, 5, 8, 13, ...
```

Definition:

\[
fib(0)=0,\quad fib(1)=1
\]

\[
fib(n)=fib(n-1)+fib(n-2)
\]

Code:

```c
#include <stdio.h>

int fibonacci(int n) {
    if (n == 0) {
        return 0;
    }

    if (n == 1) {
        return 1;
    }

    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main(void) {
    int n = 6;
    printf("Fibonacci number = %d\n", fibonacci(n));
    return 0;
}
```

Output:

```text
Fibonacci number = 8
```

This simple recursive version repeats many calculations and becomes slow for larger `n`. Later, learn iteration or memoization to improve it.

---

# 11. Recursion vs iteration

**Iteration** repeats work using loops such as `for` and `while`.

**Recursion** repeats work by calling a function again.

| Recursion | Iteration |
|---|---|
| Function calls itself | Loop repeats statements |
| Needs a base case | Needs a loop-ending condition |
| Uses call-stack space for active calls | Usually uses less call-stack space |
| Can make tree-like problems easier to express | Often efficient for straightforward repetition |
| Too many calls may cause stack overflow | A wrong condition may create an infinite loop |

Both can solve many of the same problems, but recursion is not always the best choice.

## Factorial using iteration

```c
#include <stdio.h>

int main(void) {
    int n = 5;
    unsigned long long fact = 1;

    for (int i = 1; i <= n; i++) {
        fact *= (unsigned long long)i;
    }

    printf("Factorial = %llu\n", fact);
    return 0;
}
```

Output:

```text
Factorial = 120
```

The recursive and iterative solutions produce the same result.

---

# 12. Common mistakes in functions and recursion

## Mistake 1: Missing prototype

If a function is called before the compiler has seen a suitable declaration, you may get a diagnostic.

Better:

```c
#include <stdio.h>

void greet(void); // prototype

int main(void) {
    greet();
    return 0;
}

void greet(void) {
    printf("Hello\n");
}
```

Alternatively, define the function before `main()`.

## Mistake 2: Return type does not match the result

Incorrect:

```c
// void add(int a, int b) {
//     return a + b; // void function cannot return a value
// }
```

Correct:

```c
int add(int a, int b) {
    return a + b;
}
```

## Mistake 3: Forgetting the base case

Incorrect:

```c
// int count(int n) {
//     return count(n - 1); // no stopping condition
// }
```

Correct:

```c
int count(int n) {
    if (n == 0) {
        return 0;
    }
    return count(n - 1);
}
```

## Mistake 4: Recursive call does not move toward the base case

Incorrect:

```c
// int factorial(int n) {
//     if (n == 0) return 1;
//     return n * factorial(n); // n never decreases
// }
```

Correct:

```c
int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
```

## Mistake 5: Expecting call-by-value to change the original variable

```c
void update(int x) {
    x = 50;
}
```

Calling `update(number)` does not change `number`. The function changes only its local parameter copy.

---

# 13. Practice questions

Try these yourself before checking or searching for solutions.

## Beginner

1. Create a function `greet()` that prints `Welcome to C`.
2. Create a function `printName()` that prints your name.
3. Create a function `square(int n)` that returns the square of a number.
4. Create a function `cube(int n)` that returns the cube of a number.
5. Create a function `add(int a, int b)` that returns the sum.
6. Create a function `isEven(int n)` that returns `1` if even and `0` otherwise.
7. Create a function `maximum(int a, int b)` that returns the larger number.

## Intermediate

8. Create a function that prints the multiplication table of a number.
9. Create a function that calculates the area of a circle.
10. Create a function that converts Celsius to Fahrenheit.
11. Create a function that returns the factorial using a loop.
12. Create a function that checks whether a year is a leap year.
13. Demonstrate call by value by changing a parameter inside a function and printing the original variable in `main()`.

## Recursion practice

14. Find factorial of `n` using recursion.
15. Find the sum of numbers from `1` to `n` using recursion.
16. Print numbers from `n` down to `1` using recursion.
17. Print numbers from `1` to `n` using recursion.
18. Find the `n`th Fibonacci number using recursion.
19. Find the sum of digits of a positive integer using recursion.
20. Find the power `base^exponent` using recursion.

---

# 14. Selected practice solutions

## Solution 1: Square of a number

```c
#include <stdio.h>

int square(int n) {
    return n * n;
}

int main(void) {
    int number;

    printf("Enter number: ");
    scanf("%d", &number);

    printf("Square = %d\n", square(number));
    return 0;
}
```

Example: input `6` → output `Square = 36`.

## Solution 2: Check even or odd using a function

```c
#include <stdio.h>

int isEven(int n) {
    return n % 2 == 0;
}

int main(void) {
    int number;

    printf("Enter number: ");
    scanf("%d", &number);

    if (isEven(number)) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }

    return 0;
}
```

`isEven()` returns `1` when the condition is true and `0` when false.

## Solution 3: Factorial using recursion

```c
#include <stdio.h>

unsigned long long factorial(int n) {
    if (n == 0) {
        return 1;
    }

    return (unsigned long long)n * factorial(n - 1);
}

int main(void) {
    int n;

    printf("Enter a number from 0 to 20: ");
    scanf("%d", &n);

    if (n < 0 || n > 20) {
        printf("Invalid input\n");
    } else {
        printf("%llu\n", factorial(n));
    }

    return 0;
}
```

## Solution 4: Sum of digits using recursion

```c
#include <stdio.h>

int sumDigits(int n) {
    if (n == 0) {
        return 0;
    }

    return (n % 10) + sumDigits(n / 10);
}

int main(void) {
    int n;

    printf("Enter a positive integer: ");
    scanf("%d", &n);

    printf("Sum of digits = %d\n", sumDigits(n));
    return 0;
}
```

Example: `1234` → `1 + 2 + 3 + 4 = 10`.

This example expects a non-negative integer.

---

# 15. Quick revision sheet

| Term | Meaning |
|---|---|
| Function | Reusable block of code for a particular task |
| Prototype | Declaration that tells the compiler about a function |
| Function call | Executes the function |
| Function definition | Contains the function's implementation |
| Argument | Value passed in a function call |
| Parameter | Variable that receives an argument |
| Return type | Type of value a function returns |
| `void` | Indicates no return value or no parameters, depending on its position |
| Library function | Function provided by a library |
| User-defined function | Function written by the programmer |
| Call by value | Function receives a copy of an argument's value |
| Recursion | A function calling itself |
| Base case | Condition that stops recursive calls |
| Recursive case | Function call with a smaller or simpler problem |
| Call stack | Stores information about active function calls |

## Remember these patterns

```c
// Prototype
int add(int a, int b);

// Call
int answer = add(10, 20);

// Definition
int add(int a, int b) {
    return a + b;
}
```

```c
// Basic recursive pattern
int solve(int n) {
    if (n == 0) {
        return 0;       // Base case
    }

    return n + solve(n - 1); // Recursive case
}
```


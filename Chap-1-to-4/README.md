
## Topics covered

1. [Installation and Setup](#installation-and-setup)
2. [Chapter 1 — Variables, Data Types, Input and Output](#chapter-1--variables-data-types-input-and-output)
3. [Chapter 2 — Instructions and Operators](#chapter-2--instructions-and-operators)
4. [Chapter 3 — Conditional Statements](#chapter-3--conditional-statements)
5. [Chapter 4 — Loop Control Statements](#chapter-4--loop-control-statements)
6. [Practice set and answers](#practice-set)

---

# Installation and Setup

C is a compiled programming language. You write source code in a `.c` file, compile it, and then run the executable program.

## Install a compiler

- **Windows:** Install GCC using MSYS2 (MinGW-w64) or install an IDE that bundles a C compiler.
- **Ubuntu/Debian Linux:**

```bash
sudo apt update
sudo apt install build-essential
```

- **macOS:** Install Apple's command-line developer tools:

```bash
xcode-select --install
```

Check that GCC or Clang is available:

```bash
gcc --version
# or
clang --version
```

## Your first C program

Create a file named `hello.c`:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, World!\n");
    return 0;
}
```

Compile and run:

```bash
# Linux
gcc hello.c -o hello
./hello

# Windows (in a GCC terminal)
gcc hello.c -o hello.exe
./hello.exe

# macOS
clang hello.c -o hello
./hello
```

Expected output:

```text
Hello, World!
```

## How a C program runs

```text
hello.c
  |
  v
Preprocessor  --> handles #include and macros
  |
  v
Compiler      --> translates C source into lower-level code
  |
  v
Assembler     --> creates object code
  |
  v
Linker        --> combines object code and required libraries
  |
  v
Executable    --> run the program
```

A compiler toolchain often performs these stages for you when you run one `gcc` command.

---

# Chapter 1 — Variables, Data Types, Input and Output

## 1.1 What is a variable?

A **variable** is a named object that stores a value in memory. Its value can change while the program runs.

Example:

```c
int age = 22;
age = 23;
```

Conceptual memory view:

```text
Variable name       Memory value
+-------------+     +-----------+
| age         | --> |    23     |
+-------------+     +-----------+
       type: int
```

The actual memory address is managed by the program and can be accessed with `&age`.

## 1.2 Declaring and initializing variables

**Declaration** tells C the variable's name and type.

```c
int age;
```

**Initialization** gives it its first value.

```c
int age = 22;
```

**Assignment** changes its value later.

```c
age = 23;
```

More examples:

```c
int marks = 85;
float temperature = 27.5f;
char grade = 'A';

int first, second;
first = 10;
second = 20;
```

> A local variable that is declared but not initialized has an indeterminate value. Give it a value before reading it.

## 1.3 Basic data types

| Type | Stores | Example | Common `printf` / `scanf` format |
|---|---|---|---|
| `char` | A character / small integer | `'A'` | `%c` |
| `int` | Whole numbers | `25` | `%d` |
| `float` | Single-precision decimal | `3.14f` | `%f` |
| `double` | Double-precision decimal | `3.14159` | `%f` in `printf`, `%lf` in `scanf` |
| `long long` | Larger integer range | `9000000000LL` | `%lld` |

Exact type sizes and ranges depend on the compiler and platform. Use `sizeof(type)` to inspect a type's size in bytes.

```c
#include <stdio.h>

int main(void) {
    printf("int: %zu bytes\n", sizeof(int));
    printf("float: %zu bytes\n", sizeof(float));
    printf("double: %zu bytes\n", sizeof(double));
    printf("char: %zu byte(s)\n", sizeof(char));
    return 0;
}
```

## 1.4 Constants

A constant is a value that should not be changed.

```c
const float PI = 3.14159f;
```

If you try to assign another value to `PI`, the compiler will report an error.

Common kinds of literals:

```c
int count = 10;       // integer literal
float price = 12.5f;  // floating-point literal
char symbol = '#';    // character literal
```

- Integer literals: `1`, `25`, `-7`
- Floating-point literals: `1.0`, `3.14`, `-2.5`
- Character literals: `'a'`, `'Z'`, `'#'`

A character uses **single quotes**. A string uses **double quotes**: `'A'` versus `"A"`.

## 1.5 Rules for naming variables

Valid names:

```c
int age;
int student_age;
int _count;
int number2;
```

Invalid names:

```c
// int 2number;     // cannot begin with a digit
// int student age; // spaces are not allowed
// int total-marks; // '-' is an operator, not part of a name
// int float;       // float is a keyword
```

Rules:
1. A name may contain letters, digits, and underscores.
2. It cannot begin with a digit.
3. Spaces and punctuation such as `-`, `@`, and `!` are not allowed.
4. C is case-sensitive: `age`, `Age`, and `AGE` are different names.
5. Do not use C keywords as variable names.

## 1.6 Keywords

Keywords are reserved words with special meaning in C. They cannot be used as ordinary variable names.

The 32 traditional C keywords are:

```text
auto       break      case       char
const      continue   default    do
double     else       enum       extern
float      for        goto       if
int        long       register   return
short      signed     sizeof     static
struct     switch     typedef    union
unsigned   void       volatile   while
```

Modern C standards add more keywords. The list above is the traditional 32-keyword list commonly taught to beginners.

## 1.7 Comments

Comments explain code. The compiler ignores comments.

```c
// This is a single-line comment.

/*
   This is a
   multi-line comment.
*/
```

Use comments to explain *why* code does something, not to repeat every line.

## 1.8 Output with `printf()`

`printf()` displays formatted output. It is declared in `stdio.h`.

```c
#include <stdio.h>

int main(void) {
    int age = 22;
    float pi = 3.14f;
    char grade = 'A';

    printf("Age: %d\n", age);
    printf("Pi: %.2f\n", pi);
    printf("Grade: %c\n", grade);
    return 0;
}
```

Output:

```text
Age: 22
Pi: 3.14
Grade: A
```

Useful format specifiers:

| Format | Meaning |
|---|---|
| `%d` | `int` |
| `%f` | `float` / `double` in `printf` |
| `%c` | character |
| `%s` | string |
| `%lf` | `double` in `scanf` |
| `%lld` | `long long` |
| `%zu` | `size_t`, often used for `sizeof` |

`%.2f` prints two digits after the decimal point.

Escape sequences:

| Sequence | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Horizontal tab |
| `\\` | Backslash |
| `\"` | Double quote |

## 1.9 Input with `scanf()`

`scanf()` reads formatted input. For most variables, use `&` to pass the variable's address.

```c
#include <stdio.h>

int main(void) {
    int age;

    printf("Enter your age: ");
    scanf("%d", &age);

    printf("Your age is %d\n", age);
    return 0;
}
```

Input/output flow:

```text
Keyboard input
      |
      v
scanf("%d", &age)
      |
      v
+-------------+
| age = 21    |  Memory
+-------------+
      |
      v
printf("%d", age)
      |
      v
Screen displays 21
```

Why `&age`? `scanf()` needs the memory address where it should store the entered value.

For `char`, a leading space in `" %c"` skips whitespace left in the input buffer:

```c
char grade;
scanf(" %c", &grade);
```

For simple beginner programs, `scanf()` is useful. For reading a full line of text, learn `fgets()` later.

## 1.10 Example: Sum of two numbers

```c
#include <stdio.h>

int main(void) {
    int a, b;

    printf("Enter first number: ");
    scanf("%d", &a);

    printf("Enter second number: ");
    scanf("%d", &b);

    printf("Sum = %d\n", a + b);
    return 0;
}
```

Example run:

```text
Enter first number: 10
Enter second number: 20
Sum = 30
```

## 1.11 Practice examples

### A. Area of a square

Formula: `area = side * side`

```c
#include <stdio.h>

int main(void) {
    float side;

    printf("Enter side: ");
    scanf("%f", &side);

    printf("Area = %.2f\n", side * side);
    return 0;
}
```

### B. Area of a circle

Formula: `area = π * radius * radius`

```c
#include <stdio.h>

int main(void) {
    const float PI = 3.14159f;
    float radius;

    printf("Enter radius: ");
    scanf("%f", &radius);

    printf("Area = %.2f\n", PI * radius * radius);
    return 0;
}
```

### C. Convert Celsius to Fahrenheit

Formula: `F = (C * 9 / 5) + 32`

```c
#include <stdio.h>

int main(void) {
    float celsius;
    printf("Enter temperature in Celsius: ");
    scanf("%f", &celsius);

    float fahrenheit = (celsius * 9.0f / 5.0f) + 32.0f;
    printf("Fahrenheit = %.2f\n", fahrenheit);
    return 0;
}
```

---

# Chapter 2 — Instructions and Operators

## 2.1 What is an instruction?

An instruction is a statement that tells the program to perform an operation.

```c
int age = 22;       // declaration + initialization
age = age + 1;      // assignment and arithmetic
printf("%d", age);  // output
```

Most C statements end with a semicolon `;`.

## 2.2 Types of instructions

```text
                  C Instructions
                        |
          +-------------+-------------+
          |             |             |
     Declaration    Arithmetic     Control
      statements    statements    statements
                                      |
                       +--------------+-------------+
                       |              |             |
                    Sequence       Decision        Loop
```

- **Declaration:** creates variables.
- **Arithmetic:** calculates values.
- **Control:** determines which statements execute and when.

## 2.3 Type declaration and order

Declare a variable before using it.

```c
int age = 22;
int oldAge = age;
int newAge = oldAge + 2;

printf("%d\n", newAge); // 24
```

Correct declaration order:

```c
float radius = 3.0f;
float pi = 3.14f;
float area = pi * radius * radius;
```

Incorrect order because `radius` is used before it is declared:

```c
// float area = pi * radius * radius;
// float radius = 3.0f;
// float pi = 3.14f;
```

Multiple declarations and assignments:

```c
int a, b, c;
a = b = c = 10;  // valid: all become 10
```

This is different:

```c
int a, b, c = 10; // only c is initialized to 10
```

## 2.4 Arithmetic operators

| Operator | Operation | Example | Result |
|---|---|---|---|
| `+` | Addition | `8 + 2` | `10` |
| `-` | Subtraction | `8 - 2` | `6` |
| `*` | Multiplication | `8 * 2` | `16` |
| `/` | Division | `8 / 2` | `4` |
| `%` | Remainder | `8 % 3` | `2` |

The left-hand side of an assignment must be a modifiable object:

```c
int a = 5, b = 2, c;

c = a + b;  // valid
// a + b = c; // invalid: expression is not assignable
```

Important:
- Integer division drops the fractional part: `5 / 2` gives `2`.
- Floating-point division preserves the fraction: `5.0 / 2.0` gives `2.5`.
- `%` is used with integer operands.

```c
printf("%d\n", 5 / 2);       // 2
printf("%.1f\n", 5.0 / 2.0); // 2.5
printf("%d\n", 7 % 3);       // 1
printf("%d\n", -7 % 3);      // -1 in C
```

For powers, use `pow(base, exponent)` from `<math.h>`:

```c
#include <stdio.h>
#include <math.h>

int main(void) {
    double answer = pow(2.0, 3.0);
    printf("%.0f\n", answer); // 8
    return 0;
}
```

Some systems require linking the math library, for example: `gcc power.c -o power -lm`.

## 2.5 Type conversion

C may convert one numeric type to another.

**Implicit conversion** happens automatically:

```c
int a = 5;
float b = 2.0f;
float result = a / b; // a is converted for floating-point division
printf("%.2f\n", result); // 2.50
```

Be careful: if both operands are integers, division is integer division even if the result is assigned to a `float`.

```c
int a = 5, b = 2;
float wrong = a / b;          // 2.00
float correct = (float)a / b; // 2.50
```

**Explicit conversion (casting)**:

```c
float average = (float)17 / 2;
printf("%.1f\n", average); // 8.5
```

## 2.6 Operator precedence and associativity

Precedence decides which operator is evaluated first. Parentheses make the intended order clear.

Common precedence from higher to lower:

| Priority | Operators |
|---|---|
| 1 | `()` |
| 2 | Unary `!`, `++`, `--`, unary `+`, unary `-` |
| 3 | `*`, `/`, `%` |
| 4 | `+`, `-` |
| 5 | `<`, `<=`, `>`, `>=` |
| 6 | `==`, `!=` |
| 7 | `&&` |
| 8 | `||` |
| 9 | Assignment: `=`, `+=`, `-=`, etc. |

For operators with the same precedence, associativity decides the direction.

```c
int result = 5 + 2 / 2 * 3;
// / and * have equal precedence and associate left-to-right.
// 2 / 2 = 1; 1 * 3 = 3; 5 + 3 = 8
printf("%d\n", result); // 8
```

Another example:

```c
int value = 4 * 3 / 6 * 2;
// left to right: 12 / 6 = 2; 2 * 2 = 4
```

Use parentheses when an expression might be confusing.

## 2.7 Relational operators

Relational operators compare two values. A comparison produces `1` for true and `0` for false.

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

```c
#include <stdio.h>

int main(void) {
    int a = 10, b = 5;

    printf("%d\n", a == b); // 0
    printf("%d\n", a != b); // 1
    printf("%d\n", a > b);  // 1
    printf("%d\n", a < b);  // 0
    printf("%d\n", a >= 10);// 1
    printf("%d\n", b <= 5); // 1
    return 0;
}
```

Do not confuse:
- `=` means assignment.
- `==` means comparison.

## 2.8 Logical operators

Logical operators combine or reverse conditions.

| Operator | Meaning | True when |
|---|---|---|
| `&&` | AND | Both conditions are true |
| `||` | OR | At least one condition is true |
| `!` | NOT | The condition is false |

Truth table:

| A | B | A `&&` B | A `||` B |
|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 |

```c
int age = 22;
int hasId = 1;

printf("%d\n", age >= 18 && hasId == 1); // 1
printf("%d\n", age < 18 || hasId == 1);  // 1
printf("%d\n", !(age >= 18));            // 0
```

`&&` and `||` use short-circuit evaluation: the second condition may not be evaluated if the first already determines the result.

## 2.9 Assignment operators

These operators update a variable using its current value.

| Operator | Same as |
|---|---|
| `a += 5` | `a = a + 5` |
| `a -= 5` | `a = a - 5` |
| `a *= 5` | `a = a * 5` |
| `a /= 5` | `a = a / 5` |
| `a %= 5` | `a = a % 5` |

```c
#include <stdio.h>

int main(void) {
    int a = 10;

    a += 5;
    printf("%d\n", a); // 15

    a -= 3;
    printf("%d\n", a); // 12

    a *= 2;
    printf("%d\n", a); // 24

    a /= 4;
    printf("%d\n", a); // 6

    a %= 4;
    printf("%d\n", a); // 2

    return 0;
}
```

## 2.10 Increment and decrement

```c
int x = 5;
x++; // x becomes 6
x--; // x becomes 5
```

- `++x` (pre-increment): increment first, then use the value.
- `x++` (post-increment): use the old value, then increment.

```c
int a = 5;
printf("%d\n", ++a); // 6

int b = 5;
printf("%d\n", b++); // 5
printf("%d\n", b);   // 6
```

Avoid complex expressions that modify the same variable more than once; they can be difficult to reason about and may have undefined behavior.

---

# Chapter 3 — Conditional Statements

Conditional statements allow a program to make decisions.

## 3.1 The `if` statement

Syntax:

```c
if (condition) {
    // runs when condition is true
}
```

Flowchart:

```text
        Start
          |
          v
    +-------------+
    | Condition?  |
    +-------------+
       /      \
    true      false
     |          |
     v          |
  Run block     |
     |          |
     +----+-----+
          |
          v
         End
```

Example:

```c
#include <stdio.h>

int main(void) {
    int age = 20;

    if (age >= 18) {
        printf("You are eligible to vote.\n");
    }

    return 0;
}
```

## 3.2 The `if-else` statement

Use `else` when you need an alternative action.

```c
if (condition) {
    // true block
} else {
    // false block
}
```

Example: adult or not

```c
#include <stdio.h>

int main(void) {
    int age;

    printf("Enter age: ");
    scanf("%d", &age);

    if (age >= 18) {
        printf("Adult\n");
    } else {
        printf("Not an adult\n");
    }

    return 0;
}
```

Decision diagram:

```text
          age >= 18?
           /     \
         Yes      No
          |        |
          v        v
       "Adult"  "Not adult"
           \      /
             End
```

## 3.3 Example: odd or even

A number is even when its remainder after division by 2 is zero.

```c
#include <stdio.h>

int main(void) {
    int number;

    printf("Enter a number: ");
    scanf("%d", &number);

    if (number % 2 == 0) {
        printf("Even\n");
    } else {
        printf("Odd\n");
    }

    return 0;
}
```

Test:
- Input `8` → `Even`
- Input `7` → `Odd`

## 3.4 The `else if` ladder

Use `else if` when there are multiple possible conditions. The first true branch runs; later branches are skipped.

```c
if (condition1) {
    // block 1
} else if (condition2) {
    // block 2
} else {
    // default block
}
```

Example: age category

```c
#include <stdio.h>

int main(void) {
    int age;

    printf("Enter age: ");
    scanf("%d", &age);

    if (age < 0) {
        printf("Invalid age\n");
    } else if (age < 13) {
        printf("Child\n");
    } else if (age < 20) {
        printf("Teenager\n");
    } else {
        printf("Adult\n");
    }

    return 0;
}
```

Flow:

```text
          age < 0?
          /     \
        Yes      No
         |        |
      Invalid   age < 13?
                 /    \
               Yes     No
                |       |
              Child  age < 20?
                      /    \
                    Yes     No
                     |       |
                 Teenager  Adult
```

## 3.5 Nested `if`

An `if` statement can be placed inside another `if`.

```c
#include <stdio.h>

int main(void) {
    int age = 20;
    int hasId = 1;

    if (age >= 18) {
        if (hasId == 1) {
            printf("Entry allowed\n");
        } else {
            printf("ID required\n");
        }
    } else {
        printf("Under age\n");
    }

    return 0;
}
```

Use nested conditions when one decision depends on another. For simpler logic, `&&` may be clearer.

## 3.6 Ternary operator

The ternary operator is a short form of a simple `if-else`.

Syntax:

```c
condition ? expression_if_true : expression_if_false;
```

Example:

```c
#include <stdio.h>

int main(void) {
    int age = 19;

    age >= 18 ? printf("Adult\n") : printf("Not adult\n");

    return 0;
}
```

It can also return a value:

```c
int a = 10, b = 20;
int maximum = (a > b) ? a : b;
printf("Maximum = %d\n", maximum);
```

Remember: the condition selects one of the two expressions. The condition is not required to be exactly `1` or `0`; in C, zero is false and nonzero is true.

## 3.7 `switch` statement

Use `switch` to select a branch based on an integer-like expression, commonly an `int` or `char`.

Syntax:

```c
switch (expression) {
    case constant1:
        // statements
        break;

    case constant2:
        // statements
        break;

    default:
        // runs if no case matches
}
```

Example: day number

```c
#include <stdio.h>

int main(void) {
    int day;

    printf("Enter day (1-7): ");
    scanf("%d", &day);

    switch (day) {
        case 1: printf("Monday\n"); break;
        case 2: printf("Tuesday\n"); break;
        case 3: printf("Wednesday\n"); break;
        case 4: printf("Thursday\n"); break;
        case 5: printf("Friday\n"); break;
        case 6: printf("Saturday\n"); break;
        case 7: printf("Sunday\n"); break;
        default: printf("Invalid day\n");
    }

    return 0;
}
```

`break` exits the switch. Without it, execution continues into the next case (fall-through).

Example using a character:

```c
char choice = 'A';

switch (choice) {
    case 'A':
    case 'a':
        printf("Add selected\n");
        break;
    case 'Q':
    case 'q':
        printf("Quit selected\n");
        break;
    default:
        printf("Unknown choice\n");
}
```

Switch notes:
- `case` labels must be constant values.
- Case labels can be written in any order.
- `default` is optional but useful.
- Nested `switch` statements are allowed.
- Standard C `switch` does not directly support strings or floating-point case labels.

## 3.8 When should you use each condition?

| Situation | Useful choice |
|---|---|
| One condition | `if` |
| True or false alternative | `if-else` |
| Several ranges or conditions | `else if` |
| Short choice between two expressions | Ternary `?:` |
| Many fixed choices for one value | `switch` |

---

# Chapter 4 — Loop Control Statements

A loop repeats a block of code while a condition allows it to continue.

## 4.1 Why do we need loops?

Without a loop:

```c
printf("Hello\n");
printf("Hello\n");
printf("Hello\n");
printf("Hello\n");
printf("Hello\n");
```

With a loop:

```c
for (int i = 1; i <= 5; i++) {
    printf("Hello\n");
}
```

A loop avoids repeated code.

## 4.2 The three main loops

| Loop | Condition is checked | Best for |
|---|---|---|
| `for` | Before each iteration | Known or count-controlled repetitions |
| `while` | Before each iteration | Repetition while a condition remains true |
| `do-while` | After each iteration | A block that must run at least once |

## 4.3 `for` loop

Syntax:

```c
for (initialization; condition; update) {
    // repeated statements
}
```

Example:

```c
#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 5; i++) {
        printf("%d\n", i);
    }

    return 0;
}
```

Output:

```text
1
2
3
4
5
```

How it works:

```text
Initialization: i = 1
       |
       v
  Check i <= 5
    /      \
  true     false
   |          |
   v          v
 Run body     End
   |
   v
 Update i++
   |
   +--------> Check condition again
```

The three parts:
1. **Initialization:** runs once at the beginning.
2. **Condition:** checked before every iteration.
3. **Update:** runs after the body.

## 4.4 `while` loop

Syntax:

```c
while (condition) {
    // repeated statements
}
```

Example: print 1 to 5

```c
#include <stdio.h>

int main(void) {
    int i = 1;

    while (i <= 5) {
        printf("%d\n", i);
        i++;
    }

    return 0;
}
```

The condition is checked first. If it is false at the start, the body runs zero times.

## 4.5 `do-while` loop

Syntax:

```c
do {
    // repeated statements
} while (condition);
```

Notice the semicolon after `while (condition);`.

Example:

```c
#include <stdio.h>

int main(void) {
    int i = 1;

    do {
        printf("%d\n", i);
        i++;
    } while (i <= 5);

    return 0;
}
```

A `do-while` loop always executes its body at least once.

```text
       +----------------+
       |                |
       v                |
    Run body            |
       |                |
       v                |
  Check condition? -----+
       |
     false
       |
       v
      End
```

## 4.6 Compare the loops

```c
int i = 10;

while (i < 5) {
    printf("while\n"); // runs 0 times
}

do {
    printf("do-while\n"); // runs 1 time
} while (i < 5);
```

Use `for` when counting is natural, `while` when the stopping condition controls repetition, and `do-while` when the body must run at least once.

## 4.7 Increment and decrement in loops

```c
for (int i = 1; i <= 5; i++) {
    printf("%d ", i); // 1 2 3 4 5
}

for (int i = 5; i >= 1; i--) {
    printf("%d ", i); // 5 4 3 2 1
}
```

The loop counter can be an integer, character, or another suitable type. Floating-point counters are possible but are usually avoided for exact counting because floating-point values can have rounding errors.

## 4.8 `break` statement

`break` immediately exits the nearest loop (or `switch`).

```c
#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 10; i++) {
        if (i == 5) {
            break;
        }
        printf("%d ", i);
    }

    return 0;
}
```

Output:

```text
1 2 3 4
```

## 4.9 `continue` statement

`continue` skips the rest of the current loop iteration and moves to the next iteration.

```c
#include <stdio.h>

int main(void) {
    for (int i = 1; i <= 5; i++) {
        if (i == 3) {
            continue;
        }
        printf("%d ", i);
    }

    return 0;
}
```

Output:

```text
1 2 4 5
```

Difference:

```text
break     --> leave the loop completely
continue  --> skip this iteration, then continue looping
```

## 4.10 Nested loops

A loop inside another loop is called a nested loop.

Example: 3 rows and 4 columns

```c
#include <stdio.h>

int main(void) {
    for (int row = 1; row <= 3; row++) {
        for (int col = 1; col <= 4; col++) {
            printf("* ");
        }
        printf("\n");
    }

    return 0;
}
```

Output:

```text
* * * *
* * * *
* * * *
```

Diagram:

```text
Outer loop: row = 1
    Inner loop: col = 1, 2, 3, 4
Outer loop: row = 2
    Inner loop: col = 1, 2, 3, 4
Outer loop: row = 3
    Inner loop: col = 1, 2, 3, 4
```

The inner loop completes all its iterations for each outer-loop iteration.

## 4.11 More loop examples

### A. Sum of numbers from 1 to n

```c
#include <stdio.h>

int main(void) {
    int n, sum = 0;

    printf("Enter n: ");
    scanf("%d", &n);

    for (int i = 1; i <= n; i++) {
        sum += i;
    }

    printf("Sum = %d\n", sum);
    return 0;
}
```

For `n = 5`, the calculation is `1 + 2 + 3 + 4 + 5 = 15`.

### B. Multiplication table

```c
#include <stdio.h>

int main(void) {
    int n;

    printf("Enter a number: ");
    scanf("%d", &n);

    for (int i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", n, i, n * i);
    }

    return 0;
}
```

### C. Factorial

Factorial of 5 is `5 * 4 * 3 * 2 * 1 = 120`. By definition, `0! = 1`.

```c
#include <stdio.h>

int main(void) {
    int n;
    unsigned long long factorial = 1;

    printf("Enter a non-negative number (small enough to fit): ");
    scanf("%d", &n);

    if (n < 0) {
        printf("Factorial is not defined for negative integers.\n");
    } else {
        for (int i = 1; i <= n; i++) {
            factorial *= (unsigned long long)i;
        }
        printf("Factorial = %llu\n", factorial);
    }

    return 0;
}
```

The result eventually exceeds the range of `unsigned long long`; this example is intended for small inputs.

### D. Count digits in a positive integer

```c
#include <stdio.h>

int main(void) {
    int n, count = 0;

    printf("Enter a positive integer: ");
    scanf("%d", &n);

    if (n == 0) {
        count = 1;
    } else {
        while (n > 0) {
            count++;
            n /= 10;
        }
    }

    printf("Digits = %d\n", count);
    return 0;
}
```

### E. Print a right triangle

```c
#include <stdio.h>

int main(void) {
    int rows = 5;

    for (int i = 1; i <= rows; i++) {
        for (int j = 1; j <= i; j++) {
            printf("* ");
        }
        printf("\n");
    }

    return 0;
}
```

Output:

```text
*
* *
* * *
* * * *
* * * * *
```

## 4.12 Infinite loops

A loop that never reaches a false condition is an infinite loop.

```c
// Example: intentional infinite loop
while (1) {
    // Keep running until a break or external termination.
}
```

A missing update can accidentally create an infinite loop:

```c
// Incorrect: i never changes
// int i = 1;
// while (i <= 5) {
//     printf("%d\n", i);
// }
```

Always check that the loop's condition can eventually become false, unless an infinite loop is intentional.

---

# Practice Set

Try to solve these without looking at the answers first. Write each program in its own `.c` file, compile it, and test more than one input.

## Chapter 1 — Variables, data types, input and output

1. Print `Hello, C Programming!`.
2. Declare an integer, float, and character; assign values and print them.
3. Read two integers and print their sum, difference, product, and quotient.
4. Read the length and width of a rectangle; print its area and perimeter.
5. Read marks in three subjects and print the total and average.
6. Read a radius and calculate the area of a circle.
7. Convert Celsius to Fahrenheit.
8. Swap two numbers using a third variable.

## Chapter 2 — Instructions and operators

1. Predict the output of `printf("%d", 10 + 5 * 2);`.
2. Predict the output of `printf("%d", 17 % 5);`.
3. Read two integers and print which one is greater.
4. Check whether a number is divisible by both 5 and 11 using `&&`.
5. Use assignment operators to update a variable.
6. Convert an integer to `float` and demonstrate the difference between `5 / 2` and `(float)5 / 2`.
7. Find the last digit of a positive integer using `% 10`.
8. Check whether a number is in the range 1 to 100 using relational and logical operators.

## Chapter 3 — Conditional statements

1. Check whether a number is positive, negative, or zero.
2. Check whether a number is odd or even.
3. Find the largest of two numbers.
4. Find the largest of three numbers.
5. Check whether a person is eligible to vote.
6. Print a grade based on marks using an `else if` ladder.
7. Build a simple calculator using `switch` for `+`, `-`, `*`, and `/`.
8. Use the ternary operator to find the larger of two numbers.
9. Check whether a year is a leap year.

## Chapter 4 — Loops

1. Print numbers from 1 to 100.
2. Print numbers from 100 down to 1.
3. Print all even numbers from 1 to 50.
4. Print the multiplication table of a number.
5. Find the sum of numbers from 1 to `n`.
6. Find the factorial of a number.
7. Count the digits of a positive integer.
8. Reverse the digits of a positive integer.
9. Check whether a positive integer is a palindrome.
10. Print a square and a right-triangle star pattern.
11. Print numbers from 1 to 20, but skip multiples of 3 using `continue`.
12. Stop a loop when the counter reaches 7 using `break`.

## Selected practice solutions

### 1. Largest of three numbers

```c
#include <stdio.h>

int main(void) {
    int a, b, c;

    printf("Enter three numbers: ");
    scanf("%d %d %d", &a, &b, &c);

    if (a >= b && a >= c) {
        printf("Largest = %d\n", a);
    } else if (b >= a && b >= c) {
        printf("Largest = %d\n", b);
    } else {
        printf("Largest = %d\n", c);
    }

    return 0;
}
```

### 2. Leap year

A year is a leap year if it is divisible by 400, or divisible by 4 but not by 100.

```c
#include <stdio.h>

int main(void) {
    int year;

    printf("Enter year: ");
    scanf("%d", &year);

    if (year % 400 == 0 || (year % 4 == 0 && year % 100 != 0)) {
        printf("Leap year\n");
    } else {
        printf("Not a leap year\n");
    }

    return 0;
}
```

### 3. Simple calculator with `switch`

```c
#include <stdio.h>

int main(void) {
    double a, b;
    char op;

    printf("Enter expression (example: 10 + 5): ");
    scanf("%lf %c %lf", &a, &op, &b);

    switch (op) {
        case '+':
            printf("Result = %.2f\n", a + b);
            break;
        case '-':
            printf("Result = %.2f\n", a - b);
            break;
        case '*':
            printf("Result = %.2f\n", a * b);
            break;
        case '/':
            if (b != 0) {
                printf("Result = %.2f\n", a / b);
            } else {
                printf("Cannot divide by zero\n");
            }
            break;
        default:
            printf("Invalid operator\n");
    }

    return 0;
}
```

### 4. Reverse a positive integer

```c
#include <stdio.h>

int main(void) {
    int n, reverse = 0;

    printf("Enter a positive integer: ");
    scanf("%d", &n);

    while (n > 0) {
        int digit = n % 10;
        reverse = reverse * 10 + digit;
        n /= 10;
    }

    printf("Reverse = %d\n", reverse);
    return 0;
}
```

---

# Quick Revision Sheet

| Topic | Remember |
|---|---|
| Variable | Named storage for a value |
| `int` | Whole-number type |
| `float` | Decimal type |
| `char` | Character / small integer type |
| `const` | Makes an object non-modifiable through that name |
| `printf()` | Displays formatted output |
| `scanf()` | Reads formatted input; usually pass an address with `&` |
| `=` | Assignment |
| `==` | Equality comparison |
| `%` | Integer remainder |
| `&&` | AND |
| `||` | OR |
| `!` | NOT |
| `if-else` | Makes a decision |
| `switch` | Selects among constant case labels |
| `for` | Count-controlled loop |
| `while` | Checks condition before each iteration |
| `do-while` | Runs body at least once |
| `break` | Exits nearest loop or switch |
| `continue` | Skips to the next loop iteration |

## Common beginner mistakes

- Forgetting `;` at the end of a statement.
- Writing `=` when you mean `==` in a condition.
- Forgetting `&` in most `scanf()` variable arguments.
- Using `%d` for a `float` or `%f` for an `int`.
- Using single quotes for a string instead of double quotes.
- Using a variable before declaring or initializing it.
- Forgetting to update a loop counter.
- Forgetting `break` in a `switch` case.
- Writing `while (condition)` after a `do-while` without the final semicolon.
- Expecting `5 / 2` to produce `2.5` when both operands are integers.

## Recommended study method

1. Read one concept.
2. Type the example yourself instead of copy-pasting.
3. Predict the output before running the program.
4. Compile and run it.
5. Change the input and test edge cases.
6. Solve at least three practice questions from that chapter.
7. Explain the code aloud in your own words.

---

**Scope note:** This README covers Installation + Chapters 1–4 only. Chapters 5–11 (functions, pointers, arrays, strings, structures, file I/O, and dynamic memory allocation) are intentionally not included yet.
'''
path = Path("/mnt/data/README.md")
path.write_text(content, encoding="utf-8")
print(f"Created {path} ({path.stat().st_size:,} bytes)")

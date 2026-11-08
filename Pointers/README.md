
## 1. What is a pointer?

**Definition:** A pointer is a variable that stores the memory address of another variable.

A normal variable stores a value. A pointer stores the address where that value is kept.

```c
int age = 22;
int *ptr = &age;
int _age = *ptr;
```

| Expression | Meaning |
|---|---|
| `age` | The value stored in `age` (`22`) |
| `&age` | The memory address of `age` |
| `ptr` | The address stored inside the pointer |
| `*ptr` | The value at the address stored in `ptr` (`22`) |
| `&ptr` | The memory address of the pointer variable itself |

### Memory visualization

The addresses below are **illustrative only**. Actual addresses are assigned by the program at runtime and will vary.

```text
                 MEMORY (illustrative)

 Address          Variable             Stored value
+---------+       +----------------+   +-------------+
|  2010   | ----> | age            |   |     22      |
+---------+       +----------------+   +-------------+
                       ^
                       |
                 ptr stores 2010

+---------+       +----------------+
|  2013   | ----> | ptr            |
+---------+       +----------------+
                  |     2010       |
                  +----------------+
```

In this example:
- `age` contains `22`.
- `&age` gives the address of `age` (illustrated as `2010`).
- `ptr` stores that address.
- `*ptr` follows the address and reads the value `22`.

> Do not assume that real C variables will have addresses such as 2010 or 2013. The diagram uses simple numbers only to explain the idea.

## 2. Pointer operators: `&` and `*`

### Address-of operator (`&`)

The `&` operator returns the memory address of a variable.

```c
int age = 22;
printf("%p\n", (void *)&age);
```

### Dereference operator (`*`)

The `*` operator, when used with a valid pointer, accesses the value stored at the address.

```c
int age = 22;
int *ptr = &age;

printf("%d\n", *ptr);  // 22
```

Remember:
- `&age` means “address of `age`”.
- `*ptr` means “value at the address stored in `ptr`”.
- In a declaration such as `int *ptr`, the `*` indicates that `ptr` is a pointer to an `int`.

## 3. Declaring pointers

The pointer type should match the type of object it points to.

```c
int   *intPtr;    // pointer to int
char  *charPtr;   // pointer to char
float *floatPtr;  // pointer to float
```

A safer initialization example:

```c
int number = 10;
int *ptr = &number;
```

If a pointer does not point to a valid object yet, initialize it to `NULL`:

```c
int *ptr = NULL;
```

Do not dereference a `NULL` or uninitialized pointer.

## 4. Complete pointer program

```c
#include <stdio.h>

int main(void) {
    int age = 22;
    int *ptr = &age;
    int _age = *ptr;

    // Value
    printf("age = %d\n", age);
    printf("_age = %d\n", _age);
    printf("*ptr = %d\n", *ptr);
    printf("*(&age) = %d\n", *(&age));

    // Addresses
    printf("&age = %p\n", (void *)&age);
    printf("ptr = %p\n", (void *)ptr);
    printf("&ptr = %p\n", (void *)&ptr);

    return 0;
}
```

### Code explanation

1. `int age = 22;` creates an integer variable and stores `22` in it.
2. `int *ptr = &age;` declares an integer pointer and stores the address of `age` in it.
3. `int _age = *ptr;` dereferences `ptr`, reads the value `22`, and copies it into `_age`.
4. `printf("%d", age);` prints an integer value.
5. `printf("%p", (void *)&age);` prints the address of `age`.
6. `printf("%p", (void *)ptr);` prints the address stored inside `ptr`—the address of `age`.
7. `printf("%p", (void *)&ptr);` prints the address of the pointer variable itself.

### Expected output (example)

```text
age = 22
_age = 22
*ptr = 22
*(&age) = 22
&age = 0x... 
ptr = 0x...
&ptr = 0x...
```

The three address values are runtime-dependent. The values of `age`, `_age`, `*ptr`, and `*(&age)` are `22`.

### Format specifiers

| Format | Used for |
|---|---|
| `%d` | An `int` value |
| `%c` | A character |
| `%f` | A floating-point value (`float` is promoted to `double` in `printf`) |
| `%p` | A pointer address; pass the pointer as `(void *)ptr` |

## 5. Pointer to pointer

**Definition:** A pointer to pointer is a pointer variable that stores the address of another pointer variable.

For example:

```c
int age = 22;
int *ptr = &age;
int **pptr = &ptr;
```

### Syntax

```c
int   **pptr;  // pointer to pointer to int
char  **pptr;  // pointer to pointer to char
float **pptr;  // pointer to pointer to float
```

### Visualization

```text
+------------------+       +------------------+       +------------------+
| pptr             | ----> | ptr              | ----> | age              |
| stores &ptr      |       | stores &age      |       | stores 22        |
+------------------+       +------------------+       +------------------+
        |                          |                          |
       **pptr                     *pptr                      age
        |                          |                          |
        +--------------------------+--------------------------+
                         **pptr is 22
```

More precisely:
- `pptr` is the address of `ptr`.
- `*pptr` is the pointer value stored in `ptr` (the address of `age`).
- `**pptr` is the integer value stored in `age` (`22`).

### Complete example

```c
#include <stdio.h>

int main(void) {
    int age = 22;
    int *ptr = &age;
    int **pptr = &ptr;

    printf("age   = %d\n", age);
    printf("*ptr  = %d\n", *ptr);
    printf("**pptr = %d\n", **pptr);

    printf("&age  = %p\n", (void *)&age);
    printf("ptr   = %p\n", (void *)ptr);
    printf("*pptr = %p\n", (void *)*pptr);
    printf("&ptr  = %p\n", (void *)&ptr);
    printf("pptr  = %p\n", (void *)pptr);

    return 0;
}
```

## 6. Pointers in function calls

C passes function arguments **by value**. This means a function receives a copy of the argument.

If you pass a variable's address to a function, the function receives a copy of that address. It can then use the pointer to modify the original variable. This is commonly called **call by reference using pointers**, although C itself does not have true reference parameters like C++.

### A. Call by value

The function receives a copy. Changes to its local parameter do not change the original variable.

```c
#include <stdio.h>

void square(int n);

int main(void) {
    int number = 4;

    square(number);
    printf("number after call = %d\n", number);

    return 0;
}

void square(int n) {
    n = n * n;
    printf("square inside function = %d\n", n);
}
```

**Output:**

```text
square inside function = 16
number after call = 4
```

### Call-by-value visualization

```text
main()                         square()
+------------------+          +------------------+
| number = 4       | --copy-> | n = 4            |
+------------------+          +------------------+
                                      |
                                  n = n * n
                                      |
                                  n = 16

Original number is still 4.
```

### B. Modify a variable using a pointer

Pass the address with `&number`. The pointer parameter receives that address and can change the original value through `*n`.

```c
#include <stdio.h>

void square(int *n);

int main(void) {
    int number = 4;

    square(&number);
    printf("number after call = %d\n", number);

    return 0;
}

void square(int *n) {
    *n = (*n) * (*n);
    printf("square inside function = %d\n", *n);
}
```

**Output:**

```text
square inside function = 16
number after call = 16
```

### Pointer-based modification visualization

```text
main()                               square()
+------------------+                +------------------+
| number = 4       |                | n                |
| address: 2010    |                | stores 2010      |
+------------------+                +------------------+
        ^                                    |
        |                                    | *n
        +------------------------------------+
                     points to number

*n = (*n) * (*n)
number changes from 4 to 16.
```

The address `2010` is only an illustration. The important point is that `n` points to the original `number`.

### Comparison

| Call by value | Pointer-based modification |
|---|---|
| Pass `number` | Pass `&number` |
| Function parameter: `int n` | Function parameter: `int *n` |
| Works on a copy | Can modify the original object through `*n` |
| Original remains unchanged by local assignment | Original changes when the pointed-to object is assigned |

## 7. Swapping two numbers using pointers

**Goal:** Exchange the values of two variables.

For example:

```text
Before: x = 3, y = 5
After:  x = 5, y = 3
```

### A. Swap using call by value (does not change the originals)

```c
#include <stdio.h>

void swap(int a, int b);

int main(void) {
    int x = 3;
    int y = 5;

    swap(x, y);
    printf("After call: x = %d, y = %d\n", x, y);

    return 0;
}

void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

    printf("Inside function: a = %d, b = %d\n", a, b);
}
```

**Output:**

```text
Inside function: a = 5, b = 3
After call: x = 3, y = 5
```

Why? `a` and `b` are copies. Swapping those copies does not swap `x` and `y`.

### B. Swap using pointers (changes the originals)

```c
#include <stdio.h>

void swap(int *a, int *b);

int main(void) {
    int x = 3;
    int y = 5;

    swap(&x, &y);
    printf("After swap: x = %d, y = %d\n", x, y);

    return 0;
}

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

**Output:**

```text
After swap: x = 5, y = 3
```

### Step-by-step swap visualization

Initial values:

```text
x = 3                 y = 5
```

1. `int temp = *a;` copies the value of `x` into `temp`.

```text
temp = 3              x = 3              y = 5
```

2. `*a = *b;` copies the value of `y` into `x`.

```text
temp = 3              x = 5              y = 5
```

3. `*b = temp;` copies the saved value into `y`.

```text
temp = 3              x = 5              y = 3
```

Final result:

```text
+----------------+             +----------------+
| x = 5          |             | y = 3          |
+----------------+             +----------------+
       ^                              ^
       |                              |
      *a                             *b
```

**Important correction:** The correct final line is `*b = temp;`. If you write `*b = *a;`, both variables will end up with the same value and the original value will be lost.

## 8. Common pointer mistakes

| Mistake | Why it is a problem | Better approach |
|---|---|---|
| `int *ptr;` followed by `*ptr = 10;` | `ptr` has not been initialized | Point it to a valid `int` first |
| `int *ptr = NULL;` followed by `printf("%d", *ptr);` | Dereferencing `NULL` is invalid | Check `ptr != NULL` before dereferencing |
| `int *ptr = age;` | An integer value is not an address | Use `int *ptr = &age;` |
| Printing an address with `%d` | `%d` is for integers, not pointers | Use `%p` and cast to `(void *)` |
| Returning the address of a local variable | The local variable's lifetime ends when the function returns | Use caller-owned storage or appropriate dynamic allocation |

## 9. Quick revision

| Symbol / expression | Meaning |
|---|---|
| `int *ptr` | Declare a pointer to an integer |
| `&age` | Address of `age` |
| `ptr` | Address stored in the pointer |
| `*ptr` | Value at the address stored in `ptr` |
| `&ptr` | Address of the pointer variable |
| `int **pptr` | Pointer to a pointer to an integer |
| `*pptr` | Pointer stored inside `pptr` |
| `**pptr` | Value reached through both pointer levels |
| `swap(&x, &y)` | Pass addresses so the function can modify the original variables |

### Remember

- A variable stores a value.
- A pointer stores an address.
- `&` gets an address.
- `*` dereferences a pointer to access the pointed-to value.
- A pointer must point to a valid object before you dereference it.
- C uses pass-by-value; passing a pointer lets a function modify the object it points to.

## 10. Practice questions

1. What is a pointer in C?
2. What is the difference between `ptr`, `*ptr`, and `&ptr`?
3. What does the address-of operator (`&`) do?
4. What does the dereference operator (`*`) do?
5. What is a pointer to pointer?
6. Why does call by value not modify the original variable?
7. How can a function modify a variable using a pointer?
8. Write a C program to swap two numbers using pointers.
9. What is `NULL`, and why should you avoid dereferencing it?
10. Why is `%p` used to print an address?

---

# Addressing Modes using GDB

# Overview

This project demonstrates various addressing modes in C programming and analyzes them using the GNU Debugger (GDB). It helps in understanding how data is accessed from memory, registers, arrays, pointers, and stack during program execution.

---

# Aim

To implement and study different addressing modes in C programming and observe their behavior using the GNU Debugger (GDB).

---

# Addressing Modes Covered

- Immediate Addressing
- Direct Addressing
- Register Addressing
- Indirect Addressing
- Register Indirect Addressing
- Indexed Addressing
- Base Register Addressing
- Relative Addressing
- Auto Increment Addressing
- Auto Decrement Addressing
- Stack Addressing

---

# Code Implementation

## Code (`addressing.c`)

```c
#include <stdio.h>

// Direct Addressing (global variable)
int global_var = 50;

void function_example() {

    int x = 5, y = 10;       // Stack Addressing

    int a = 20;              // Immediate Addressing
    int b = a;               // Register Direct Addressing

    int *p = &a;             // Indirect Addressing
    int c = *p;              // Register Indirect Addressing

    int arr[5] = {1,2,3,4,5}; // Indexed Addressing
    int d = arr[2];

    int *base = arr;         // Base Register Addressing
    int e = *(base + 3);

    for(int i = 0; i < 3; i++) { // Relative Addressing
        x += i;
    }

    int f = 0;               // Auto Increment Addressing
    f = arr[f++];

    int g = 2;               // Auto Decrement Addressing
    g = arr[--g];

    printf("%d %d %d %d %d %d %d\n", b, c, d, e, f, g, global_var);
}

int main() {
    function_example();
    return 0;
}
```

---

# How to Run

## Compile with Debug Symbols

```bash
gcc -g addressing.c -o addressing
```

---

# Run Program

```bash
./addressing
```

---

# Run with GDB

```bash
gdb ./addressing
```

---

# Useful GDB Commands

| Command | Description |
|---------|-------------|
| `break main` | Set breakpoint at main function |
| `run` | Start execution |
| `next` | Execute line by line |
| `step` | Enter function |
| `print variable` | Display variable value |
| `print &variable` | Display memory address |
| `x address` | Examine memory contents |
| `info registers` | View register values |
| `continue` | Continue execution |
| `quit` | Exit GDB |

---

# Understanding Addressing Modes

## Immediate Addressing

```c
int a = 20;
```

The value is directly assigned during instruction execution.

---

## Direct Addressing

```c
int global_var = 50;
```

The memory address of the variable is directly accessed.

---

## Register Addressing

```c
int b = a;
```

The value is transferred between CPU registers.

---

## Indirect Addressing

```c
int *p = &a;
```

A pointer stores the address of another variable.

---

## Register Indirect Addressing

```c
int c = *p;
```

The value is accessed indirectly through a pointer register.

---

## Indexed Addressing

```c
int d = arr[2];
```

Array elements are accessed using index values.

---

## Base Register Addressing

```c
int e = *(base + 3);
```

A base address with offset is used to access memory.

---

## Relative Addressing

```c
for(int i = 0; i < 3; i++)
```

Execution depends on relative changes in control flow.

---

## Auto Increment Addressing

```c
f = arr[f++];
```

The pointer/index increments automatically after access.

---

## Auto Decrement Addressing

```c
g = arr[--g];
```

The pointer/index decrements before access.

---

## Stack Addressing

```c
int x = 5, y = 10;
```

Local variables are stored inside stack memory.

---

# Learning Outcomes

Through this experiment, we learned:

- How different addressing modes work internally
- How memory is accessed during program execution
- How arrays and pointers interact with memory
- How registers and stack behave during execution
- How to analyze programs using GDB

---

# Output Example

```text
20 20 3 4 1 2 50
```

---

# Conclusion

This project successfully demonstrates various addressing modes in C programming.

Using GDB, we can clearly observe:

- Memory access operations
- Register usage
- Pointer behavior
- Stack and array execution flow

Overall, this experiment improves understanding of low-level programming, debugging techniques, and system-level execution of C programs.


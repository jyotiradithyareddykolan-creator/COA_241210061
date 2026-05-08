# Experiment 3 - GDB Debugging and Data Structure Analysis

## Objective

This lab focuses on compiling and debugging programs using the GNU Debugger (GDB). It helps in understanding the core concepts of Computer Architecture, memory addressing, and execution flow.

The experiment covers:

* Basic GDB commands
* Compiling C programs using GDB
* Debugging Stack, Queue, and Linked List programs
* Understanding memory and variable tracking during execution

---

# Background Study

The **GNU Debugger (GDB)** is a powerful debugging tool used for programs written in languages like C and C++.

GDB allows programmers to:

* Execute programs line-by-line
* Set breakpoints during execution
* Inspect variable values and memory
* Trace function calls and program flow
* Analyze runtime behavior of programs

To enable debugging, programs must be compiled using the `-g` flag.

---

# Key Concepts

## Breakpoint

A breakpoint is a point where program execution pauses for inspection.

### Example

```bash
break main
```

---

# Step Execution Commands

| Command    | Description                 |
| ---------- | --------------------------- |
| `next`     | Executes the next line      |
| `step`     | Enters into the function    |
| `continue` | Continues program execution |

---

# Variable Inspection

```bash
print variable_name
```

This command displays the current value of a variable.

---

# Data Structures Used

## Stack (LIFO)

Last In First Out structure.

## Queue (FIFO)

First In First Out structure.

## Linked List

Dynamic memory structure connected using pointers.

GDB helps visualize internal operations such as:

* `top` in Stack
* `front` and `rear` in Queue
* `head` pointer in Linked List

---

# Setup Instructions

## Install GDB and GCC

```bash
sudo apt update
sudo apt install build-essential gdb
```

---

# Verify Installation

```bash
gcc --version
gdb --version
```

---

# Compile Program with Debug Symbols

## For Ubuntu/Linux

```bash
gcc -g filename.c -o output
```

## For Mac (M3/M4)

```bash
gcc -g -gdwarf-4 filename.c -o output
```

### Example

```bash
gcc -g stack.c -o stack
gcc -g -gdwarf-4 stack.c -o stack
```

---

# Start GDB

```bash
gdb ./output
```

---

# Important GDB Commands

| Command               | Description                           |
| --------------------- | ------------------------------------- |
| `break main`          | Set breakpoint at main function       |
| `break function_name` | Set breakpoint at a specific function |
| `run`                 | Start program execution               |
| `next`                | Execute next line                     |
| `step`                | Enter function                        |
| `continue`            | Continue execution                    |
| `print variable`      | Display variable value                |
| `info breakpoints`    | Show all breakpoints                  |
| `quit`                | Exit GDB                              |

---

# Debugging Flow

```text
Compile → Open GDB → Set Breakpoint → Run → Step Through → Observe Variables → Exit
```

---

# STACK IMPLEMENTATION

## Code (`stack.c`)

```c
#include <stdio.h>
#define SIZE 5

int stack[SIZE];
int top = -1;

void push(int value) {
    if (top == SIZE - 1) {
        printf("Overflow\n");
        return;
    }
    stack[++top] = value;
}

void pop() {
    if (top == -1) {
        printf("Underflow\n");
        return;
    }
    top--;
}

int main() {
    push(10);
    push(20);
    pop();
    return 0;
}
```

---

# GDB Flow for Stack

```bash
gdb ./stack
break main
run
next
step
print top
print stack
continue
```

---

# Stack Flow

```text
PUSH → Add element → Increase top
POP  → Remove element → Decrease top
```

---

# QUEUE IMPLEMENTATION

## Code (`queue.c`)

```c
#include <stdio.h>
#define SIZE 5

int queue[SIZE];
int front = -1, rear = -1;

void enqueue(int value) {
    if (rear == SIZE - 1) {
        printf("Overflow\n");
        return;
    }
    if (front == -1)
        front = 0;

    queue[++rear] = value;
}

void dequeue() {
    if (front == -1 || front > rear) {
        printf("Underflow\n");
        return;
    }
    front++;
}

int main() {
    enqueue(1);
    enqueue(2);
    dequeue();
    return 0;
}
```

---

# GDB Flow for Queue

```bash
gdb ./queue
break main
run
step
print front
print rear
print queue
continue
```

---

# Queue Flow

```text
ENQUEUE → Insert at rear
DEQUEUE → Remove from front
FIFO (First In First Out)
```

---

# LINKED LIST IMPLEMENTATION

## Code (`linkedlist.c`)

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* head = NULL;

void insert(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = head;
    head = newNode;
}

void display() {
    struct Node* temp = head;

    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
}

int main() {
    insert(10);
    insert(20);
    display();
    return 0;
}
```

---

# GDB Flow for Linked List

```bash
gdb ./linkedlist
break main
run
step
print head
print *head
next
continue
```

---

# Linked List Flow

```text
Create Node → Assign Data → Link Next → Update Head
```

---

# RESULT

Successfully compiled programs using:

```bash
gcc -g -o test filename.c
```

Programs were executed inside GDB and the following operations were performed:

* Set breakpoints at `main()` and other functions
* Executed programs step-by-step
* Observed real-time variable changes
* Verified correctness of Stack, Queue, and Linked List operations

### Observations

* Stack operations updated `top` correctly
* Queue operations updated `front` and `rear` correctly
* Linked List insertion updated the `head` pointer properly

Debugging helped in:

* Identifying logical errors
* Understanding program flow clearly
* Tracking variable and memory changes

---

# CONCLUSION

GDB is an essential debugging tool for analyzing program behavior.

It provides detailed insights into:

* Execution flow
* Variable states
* Memory handling
* Function calls and logic tracing

Through this experiment:

* Practical debugging experience was gained
* Understanding of data structures improved
* Error detection and correction techniques were learned

Overall, GDB improves program reliability and developer productivity by enabling systematic debugging.


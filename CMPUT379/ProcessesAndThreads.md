# Processes and Threads

## Processes

------

- *Process* is a program executing in some environment.

------

### Memory context

------

![image-20220113153334894](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113153334894.png)

- ***initialized data* and *text segment*** are loaded in the memory after calling command in the family of "exec" command on a program file.
- ***text segment*** are usually instruction of the program.
- **Global variables** are in initialized data blocks
- **Non initialized global variables** are allocated in ***uninitialized data segment*** in runtime
- Variables **declared in the function** are allocated in ***stack segment*** in runtime
- ***Stack segment*** starts from high memory. Segment grows down to low memory.
- **Dynamic** variables are allocated in the ***heap segment***.
  - **Global variables** that are allocated dynamically, using *new*, *malloc* and so on, are also in ***heap segment***.
- The arrangement of ***stack*** and ***heap segment*** maximize the use of main memory.
- The **values of arguments input** from the shell when launching the program are in the ***top segment***
- Variables defines in initialization shell file (*.bashrc* and similar) are also in the **top segment** when the program is executed

------

#### Exercise

------

- How to expand a process' stack ? *setrlimit* to expand the process' stack

  ```c++
  #include  <stdio.h>
  void foo (int n) {
      int i, a[5], *b;
      // &i - address of i
      // a - address of first element of array a
      // b - address of first element of array b
      
      if (n == 0) return;
      b = new int[n];
      printf("foo(%d): &i = %p, a = %p, b = %p\n", n, &i, a, b);
      foo(n - 1);
  }
  
  int main() {
      foo(3);
  }
  ```

- Output

  ```
  foo(3): &i = bffff9a4, a = bffff990, b = 80497f0
  foo(2): &i = bffff964, a = bffff950, b = 8049800
  foo(1): &i = bffff924, a = bffff910, b = 8049810
  ```

- Memory Arrangement
  - stack (n = 3) (high address to low address) : i, a[0] ... a[4], b 
  - stack (n = 2) : i, a[0] ... a[4], b
  - ...
  - heap (n = 3) (low address to high address) : b[0] ... b[2]
  - heap (n = 2) : b[0] ... b[1]
  - ....

- Anyway : a process  $\neq$ a program $\neq$ a job
- Change the base of address for the stack and heap provide security 

------

### A Conceptual Framework

------

- Process states

- Process data structures (for a process control block, PCB)

  - PCB contains all relevant information about the program

- Process queues

  - keep track of process sorted by their states

  ![image-20220113180130872](C:\Users\Dekr0\AppData\Roaming\Typora\typora-user-images\image-20220113180130872.png)

  - new - process is created, and acquires resource
  - ready - process is runnable but not yet executed
  - scheduler (process "sched") dispatch give the process control of the CPU 

------

### Daemon

------

- *Daemon* is a program (process)

  - doesn't attach to display and keyboard

  - All communication with daemons process use inter process communication in main memory, or inter process communication involves internet socket

  - name of the process usually ends with "d"

------

### Important Processes 

------

- **pageout** (page daemon) keeps track of the page (virtual memory and main memory).
- **Csh** is a shell program 
  - interacts with user after taking login information and authentications from the users,
  - provides command line interface
  - include a programming language


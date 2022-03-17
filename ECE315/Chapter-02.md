# Chapter 02

## "Hello World!" Example

------

- Tx - Transmit

- Rx - Receive

- `tskIDLE_PRIORITY` is pre-defined constant based on the environment.

- Task with highest priority that is ready to run will have control of CPU.
- vTimerCallback is called when timer is expired. 

------

## C

------

- The cause of potential hazard of C    
  - C is design by a group expert programmers to get the job done.
  - C is not intended to come out the laboratories and be used by other programmers .

------

### Pointers in C

------

- Data structures built on pointer : linked list
- By convention, base address points to the first byte of data in memory. Otherwise, compilers make the decision.
- When dereferencing a type-less pointer, it requires casting 
- It is bad idea to consider the size of integer / other data type is the same for embedded system.

------
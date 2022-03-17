# Chapter 5

## Tasks in FreeRTOS

------

- Two tasks with equal priority will share CPU time together. How?
  - Tick timer, every time a tick timer ticks, switch task.
- Every time a tick timer is called, it is an interrupt instruction.
  - Interrupt frequency should be slowed to avoid interrupt being called to often because it keep using up CPU cycle (waste of CPU time and power)

- There's always an idle task that is running.
  - Its job can be cleaning up, etc.

------

## Critical Section

------

- `taskEnter_CRITICAL()` and `taskEXIT_CRITICAL()` need to be in pair
  - They can be nested
- All other services blocked and freeze and critical section need to finish as soon as possible

------

## Semaphores, Mutexes and Notifications

------

- **Semaphores** is equivalent to signals
- Unblocking a task using **binary** semaphore doesn't necessarily make the task start running.
  - A task needs to compete for CPU time with other tasks
  - To let a task to run right away, give that task higher priority
    - Priority determines the order of execution of tasks
- **Counting semaphore** can count number of devices
- **Mutex** accelerate the low priority task, which blocks higher priority tasks, to allow higher priority tasks to start execute earlier

------

## Others

------

- Don't pass an uninitialized pointer. Some functions will treat it as a valid pointer.
  - When they deference that pointer, there are garbage data.
  - It can crash the system. 

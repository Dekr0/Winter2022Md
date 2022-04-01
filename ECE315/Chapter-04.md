# Chapter 04

## Multitasking

------

- An interrupt task need to be finished as soon as possible
- Idle task is to safely use up the remaining idle task or handle other low priority task such as garbage collection, clean up, etc.
- As long as the tasks with highest or higher priority is ready to run in **pre-emptive multitasking** system, they can use the CPU and run first compare to other tasks (available to run) with lower priority.
- All the tasks need to have sufficient CPU use time in each cycle, it's up to the system designer to design (how much time each task should have by setting priority and how to implement to each task step by step)
  - Even for the higher priority tasks, they need to be blocked and voluntarily give up CPU in some condition.
    - wait for information to arrive from lower priority tasks
  - If the lower priority task doesn't have any CPU use time, the system is a failure.
    - Lower priority tasks / Idle tasks still do useful work for higher priority tasks
- There are also priorities for interrupts that are managed by hardware.
  - Interrupts can be quite disrupted.
  - Interrupts need to be very soon / short.

------

## Mutex, Semaphore, Deadlock

------

- Functions that implement counting semaphores are also need protection from interrupts.  They turn off the interrupts to perform the update on the data structure (integer count and a queue of tasks).
- Semaphores itself is a critical sections. It has to be protected.
- Highest priority get unblock first. Same priority, the one with longest waiting time get unblock first.
- Similar situations compared to semaphores where a block needs a corresponding unblock, dynamic memory allocation. Memory need to be recycles otherwise it get memory leaked.
- A task shouldn't be blocked forever on a queue. Timeout and send notification.
  - A task blocked on queue should reduce its priority so that another task in the other sides queue can consume the content.
- Edward Coffman's four conditions for deadlock:
  - Resources can be assigned exclusively to tasks, and there is no way for them to give it up.
    - Solution : deadline or set limit on use time
  - 2nd condition is hard to fix because a task need two or more resources quiet often.
  - 3rd condition is hard to implement
  - 4th condition, it is not obvious

------

## Watchdog Timer

------

- If we are entrust the operation of large scale equipment / potential dangerous equipment, or equipment that are in a distance that operators and developers can't get access easily, there must be ways to let it recover from catastrophic failure (software and hardware failure)
  - Standard trick : watchdog timer (independent of operating system, must away from the users)
- Watchdog doesn't necessarily fix the deadlock. It depends how critical the situation of deadlock is. If a watchdog timer is not implemented properly, it will ignore it.
- Watchdog is not sufficient on it own. It requires one to design a sufficient petting routine that check the system status.
- Watchdog timer service routine
  - During health check, each flag need to be set to 1 to indicate normal / healthy execution.
  - The flags would be cleared by the watchdog timer service routine.
- In some situations, it is better to use mutexes than binary semaphores due to priority inversion issues.
- Deadlock is similar to priority inversion due to the characteristic of which tasks are blocked each other.
  - Deadlock is more serious and there's no simple to way to fix it.

------

## Figures of Merit (Property) for Real-Time Kernels

------

- Making decision on what OS to use => what sort things are looked for and consider.
- Scalability - if there are features that are not needed, then is it possible to let them out.
- Faster response time is not sufficient
  - fast in all time? but slow in some situation
  - worst case
- How to make a system more predictable and deterministic?
  - Use of priority.
  - If some services / tasks in a system are more important than others, higher priority should be assigned to them
  - so that better quality of service => faster response and more deterministic response.

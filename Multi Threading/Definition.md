- Thread ,process = small tasks , part of a program

- Multithreading  = Running two  or more process in parallel.

- when to use:
   when we have  tasks which are  independent to each other.

- why we use:
  To optimize and full use of multi cores.

- Race Condition:
  when two or more threads try to change a single  global variable this situation is called race condition.

- Critical section:
  If  the race condition is found then the section which cause the race condition is called critical section.

- Mutex:
  Mutual Execution
  When we encounter a critical section to make then synchronize we use mutex it is a class so create a mutex object .
  **Types**
  - mutex 
  - recursive_mutex 
  - timed_mutex 
  
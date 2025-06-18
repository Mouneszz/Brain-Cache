
- When we say **"switching the CPU for multiple processes,"** it means that the CPU is allocated to different processes at different times to maximize efficiency and resource utilization.
- A modern **CPU** can have multiple **cores**, where each core acts as an independent processing unit capable of executing its own instructions. When discussing **CPU scheduling**, if a system has only **one core**, it can run only **one process at a time**, and scheduling determines **which process gets the core next**.

***BURST TIME***
- **CPU Burst**: The period when a process is actively using the CPU to perform computations or execute instructions.
- **I/O Burst**: The period when a process is waiting for or performing input/output operations (like reading from disk or waiting for user input).

***CPU Scheduler***
- When the CPU becomes idle, the OS must select one process which is in the ready queue to be executed. This selection process is done by CPU scheduler.
***Dispatcher***
- When the CPU scheduler selects the process to execute, the dispatcher  stops the process which is waiting in CPU and select the one to start.

**Preemptive scheduling** 
- When there is a choice to schedule/choose the process to execute 
- When a process switches from **running state** to **ready state**.
- When a process switches from **waiting state** to **ready state**

**Non Preemptive Scheduling**
- When there is no choice to choose the process
- When a process switches from **running state** to **waiting state**
- When a process **terminates** which leaves no choice, so choosing the process which is in  the ready queue is idle.

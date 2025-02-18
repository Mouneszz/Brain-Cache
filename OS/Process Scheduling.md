### What is a  process?
-  It is nothing but a simple program which runs, everything that runs in a computer is a process.
- its is an active entity, unlike a program which is passive entity.

### How does a process look like in a memory ?
- Text section: A text or code segment contains executable instructions.
- Stack: The stack contains the temporary data such as parameters, and local variables.
- Data section: Contains the global  variable.
- Heap section: Dynamically allocated memories present here.

### PCB (Process control Block):
 -  Every  process will have a PCB.
 -  It will have all the important information about the process.
 -  Example : Process ID...

### States of processing:
- ### Two state model:
	- Running : actively using the CPU
	- Not running: Not actively using the CPU, could be waiting for an input or data or may be paused.
	- When a new process is created  it is initialize not running state, will be kept in a dispatcher.
- ### Five state model:
     - New :  This state have the newly created process that are not started running yet.
     - Ready : A process which is ready to run as soon as the CPU is available.
     - Running : Same as in two state, process which are currently executing.
     - Blocked/Waiting : The state means the process cannot continue executing right now.
     - Exit/Terminate: A process which is finished its execution or has been stopped explicitly by user.

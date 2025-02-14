What is an OS?
- An OS is system software that manages hardware and software resources, providing services for programs.
- An operating system acts as an intermediary between the user of a computer and computer hardware. In short its an interface between computer hardware and user.

Functions of OS:
- **Process Management** – Handles process creation, scheduling, and termination.
- **Memory Management** – Allocates and deallocates memory for processes.
- **File System Management** – Organizes and controls access to files.
- **I/O Device Management** – Manages input/output operations and device drivers.
- **Security & Protection** – Ensures secure access to system resources.

CPU:
- It executes instructions from programs and manages system operations.
- CPU **executes instructions**, the **OS acts as a manager**.
- components :- 
 1. **Arithmetic Logic Unit (ALU)** – Performs calculations and logic operations.
 2. **Control Unit (CU)** – Directs execution flow and manages communication between components.
 3. **Registers** – Small, fast storage inside the CPU for temporary data.
 4. **Cache Memory** – Stores frequently used data for quick access.
 ```
+---------------------+
| User Runs Program  |
+---------------------+
          |
          v
+---------------------+
| OS Loads Program   |
| into Memory (RAM)  |
+---------------------+
          |
          v
+---------------------+
| CPU Fetches        |
| Next Instruction   |
+---------------------+
          |
          v
+---------------------+
| CPU Decodes &      |
| Executes the       |
| Instruction        |
+---------------------+
          |
          v
+---------------------+
| If I/O is Needed?  |-- Yes --> OS Handles I/O (Disk, Network)
| (File, Network)    |-- No --> Continue Execution
+---------------------+
          |
          v
+---------------------+
| Program Completes  |
| and OS Frees Memory|
+---------------------+

```

Registers:
- **A type of computer memory unit used to accept, store, and transfer data and instructions used by the CPU right away(For immediate use). **
- **Registers** are small, high-speed memory units inside the CPU that store data temporarily during execution.

Driver:
- **Device Drivers** are software programs that allow the operating system to communicate with hardware devices like printers, keyboards, and graphics cards.
- Convert **OS instructions** into device-specific commands.

System call:
 - A system call is a programmatic way in which a computer program requests a service from the kernel of the operating system. It is a way for programs to **interact with the operating system****.

Kernel mode:
- **Kernel Mode** is a privileged execution mode where the operating system has full access to hardware and system resources.

Context Switching:
 - A system call requires a [context switch](https://www.geeksforgeeks.org/context-switch-in-operating-system/), which involves saving the state of the current process and switching to the kernel mode to execute the requested service. This can introduce overhead, which can impact system performance.

Interrupt:
- An **interrupt** is a signal sent to the CPU to stop its current execution and handle an urgent task. It helps the OS manage multiple processes efficiently.





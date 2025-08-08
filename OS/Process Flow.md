### 🚀 **Flow of a Process Execution (with Key OS Concepts)**

1. **Program Stored on Disk (Secondary Storage)**
    
    - A process begins as a **program** (a .exe, .out, etc.) stored in disk.
        
2. **Process Created by OS (Process Control Block – PCB)**
    
    - When a program is executed, OS:
        
        - Allocates memory for it (creates its **logical address space**).
            
        - Creates its **PCB**, which contains:
            
            - PID (Process ID)
                
            - Program Counter (PC) → address of next instruction
                
            - CPU registers
                
            - Process state (Ready, Running, etc.)
                
            - Memory info (page table, etc.)
                
3. **Paging (if used)**
    
    - OS divides the **logical address space** into **pages** (fixed-size chunks).
        
    - Pages are mapped to **frames** in **physical memory (RAM)** using a **page table**.
        
    - Only required pages are loaded into RAM (demand paging).
        
4. **Scheduler Picks the Process**
    
    - CPU Scheduling algorithm (like FCFS, RR, SJF) decides which process runs.
        
    - Context switch occurs → CPU loads the PCB info (registers, PC) of the chosen process.
        
5. **Process Runs in CPU**
    
    - CPU executes instructions using data from **main memory**.
        
    - If a required page is not in memory → **page fault** occurs → OS loads the page from disk (Virtual Memory concept).
        
    - **Page Replacement** may occur using LRU or FIFO if memory is full.
        
6. **Interrupt or Time Slice Over**
    
    - If an interrupt occurs or time quantum ends (in RR), context switch happens again.
        
    - PCB of current process is saved; next process is loaded from its PCB.
        
7. **Process Terminates or Waits**
    
    - If the process completes → OS deletes its PCB and frees memory.
        
    - If it waits (I/O), state changes to **Waiting**.
        

---

### 💡 Summary of Key Concepts in Flow:

| Concept              | Role in Flow                                    |
| -------------------- | ----------------------------------------------- |
| **PCB**              | Stores process state, loaded during switch      |
| **Program Counter**  | Points to next instruction                      |
| **Scheduler**        | Picks which process runs                        |
| **Paging**           | Maps virtual pages to physical frames           |
| **Page Table**       | Used to translate logical to physical address   |
| **Page Replacement** | Used when memory is full                        |
| **Virtual Memory**   | Enables large processes to run with limited RAM |
| **Context Switch**   | Switches CPU from one process to another        |
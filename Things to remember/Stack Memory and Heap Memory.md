### **Stack Memory**

- **Purpose**: Used for managing function calls, local variables, and control flow.
- **Structure**: Linear, Last In First Out (LIFO).
- **Size**: Fixed size determined at compile time.
- **Usage**:
    - Stores local variables and function arguments.
    - Keeps track of function calls (call stack).
- **Lifetime**: Automatically deallocated when a function ends.
- **Advantages**:
    - Faster memory access.
    - Automatic memory management.
- **Disadvantages**:
    - Limited size.
    - Cannot allocate memory dynamically.
```cpp
int a = 10;
```

### **Heap Memory**

- **Purpose**: Used for dynamic memory allocation.
- **Structure**: Non-linear; memory is allocated from a pool.
- **Size**: Typically larger and grows during runtime.
- **Usage**:
    - Stores objects and data that need to persist beyond function scope.
    - Memory is explicitly allocated and freed using functions like `new`/`delete` in C++ or `malloc`/`free` in C.
- **Lifetime**: Managed manually by the programmer; persists until explicitly deallocated or the program ends.
- **Advantages**:
    - Flexible size and dynamic allocation.
    - Can allocate memory at runtime.
- **Disadvantages**:
    - Slower access compared to the stack.
    - Risk of memory leaks if not properly deallocated.
      ```cpp
      int* p = new int(10);
```
    

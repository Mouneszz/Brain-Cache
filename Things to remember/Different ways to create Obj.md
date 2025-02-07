Memory for the object is automatically allocated when the statement is executed and deallocated when the object goes out of scope (e.g., when the function ends).
```cpp
classname obj;
```

Memory for the object is explicitly allocated, and it is the programmer's responsibility to free the memory using `delete` when the object is no longer needed.
```cpp
classname* obj = new classname();
```


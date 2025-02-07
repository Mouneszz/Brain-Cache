# **Switch**
- A `switch` statement **checks for the matching case once**. When a case matches, execution starts from **that case** and continues **until a `break` statement is found** (or until the `switch` block ends). This is called **fall-through behavior**.
```c
#include <stdio.h>
int main() {
    int n = 0, i;
    for (i = 0; i < 3; i++) {
        switch (i) {
            case 0:
                n -= i;  // n = 0 - 0 = 0
                // No break, so it falls through to case 1
            case 1:
                n += i;  // n = 0 + 1 = 1
                // No break, so it falls through to case 2
            case 2:
                n *= i;  // n = 1 * 2 = 2
                break;   // Breaks out of switch
            default:
                n += 5;  // This is never executed
                break;
        }
    }
    printf("%d %d", n, i); // 12 3
    return 0;
}
```

# **Increment and Decrement**
🔹 **Pre-increment (`++x`)** → Increases `x` **before** using it.  
🔹 **Post-increment (`x++`)** → Increases `x` **after** using it.
```c
#include <stdio.h>
int main() {
    int x = 5;
    
    printf("Pre-increment: %d\n", ++x); // Increment first than prints // 6 x = 6
    
    x = 5;  // Reset x
    printf("Post-increment: %d\n", x++); // Prints than increments  // 5 but x =6
    printf("Final value of x: %d\n", x);
    
    return 0;
}

```

🔹 **Pre-decrement (`--x`)** → Decreases `x` **before** using it.  
🔹 **Post-decrement (`x--`)** → Decreases `x` **after** using it.
```c
#include <stdio.h>
int main() {
    int x = 5;
    int y = x++ + x; // 5 + 6
    printf("%d %d", y, x); // 11 6
    return 0;
}

```
In the code the order if execution is important first the post increment is happening so now in the x place is 5 spawned but real value of x is 6 so 5 + 6.

## Increment and decrement in **pointers**
```c
#include <stdio.h>
int main() {
    int arr[] = {10, 20, 30, 40};
    int *ptr = arr; // Points to arr[0] arr == &arr[0]

    printf("Value at ptr: %d\n", *ptr); // 10
    ptr++;  // Moves to the next integer (arr[1])
    printf("Value at ptr after increment: %d\n", *ptr); // 20

    return 0;
}
```
When you increment or decrement a pointer, it **moves by the size of the data type it points to.**
```c
#include <stdio.h>
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int *ptr = arr; // Points to arr[0]

    while (ptr <= &arr[4]) { // Until last element
        printf("%d - ",ptr);
        printf("%d",*ptr);
        printf("\n");
        ptr++;
    }
    return 0;
}
```
Lets imagine the `ptr` is storing 600 which is `&arr[0]` the last value's address will 616 so when the incrementing  is happening it will increment by 4 bytes. so when it crosses 616 it will end the loop.
Output:
```
968626864 - 1
968626868 - 2
968626872 - 3
968626876 - 4
968626880 - 5
```

**Difference Between `ptr++` and `(*ptr)++`**
🔹 **`ptr++`** → Moves the pointer to the next memory location.  
🔹 **`(*ptr)++`** → Increments the value stored at that pointer.





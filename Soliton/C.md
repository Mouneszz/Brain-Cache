# **Arrays**

```c
int arr[5];
arr[0] = 10;   // Assign 10 to the first element of the array
```
-  here `arr` is an array which have 5 space
- To get an array from user use for loop with 0->n-1;
-  the `arr` points to the first element like this `&arr[0]`
```c
printf("%d\n", *arr);  // Output will be 10, which is the value at arr[0]
```
To find the size of the array.
```c
int size = sizeof(arr) / sizeof(arr[0]);  // Size of array
```
Multi dimensional array 
```c
int arr[2][3] = { {1, 2, 3}, {4, 5, 6} };  // 2x3 array
```



# **Strings**
- In C, strings are just arrays of characters terminated by a **null character** (`'\0'`), which indicates the end of the string.
```c
char str[6] = "Hello";   // Array of characters, includes '\0' automatically we have to have a extra space for the null character '\0'.
```
- We have header file to make our job easy like `string.h`.
```c
#include <string.h>
char str[20];
strcpy(str, "Hello");
printf("String length: %lu\n", strlen(str));  // Output: 5
```
**String as a Pointer**: A string in C is essentially a pointer to the first character. For example, if you declare:
```c
char str[] = "Hello";
printf("%c\n", *str);  // Output: 'H' 
printf("%c\n", *(str + 1));  // Output: 'e'`
```
- `str` points to the address of `'H'`, and `str + 1` would point to `'e'`.

string copy
```c
char str[] = "Helloworld";
char temp[6];
strcpy(temp,str+5); //  temp = "World" , str is a pointer which points the string frist character but when we increment the pointer by five times now it is pointing to the w.
```

# Pointers
So  pointer are like a variable which holds the address of an another  variable .
```c
int a =10;
int* ptr = &a; // here ptr holds 'a' address
printf("%d",*ptr); // 10
```
To access the value in the address we have to use `*ptr`;

```c
int main() {
    int x =5;
    int* ptr = &x;
    printf("%d\n",ptr); // ptr is the has the address of the x
    printf("%d\n",*ptr); // *ptr is  gives the value which is in the ptr
    printf("%d",&ptr); // &ptr gives the address of the ptr itself
    }
```

**Size of Pointer**

- Size of the pointers is not depend on the data type which it holds it depends on the compiler and system architect type.
     - 64 bit  - 8 byte
     - 32 bit  - 4 byte
     - 
- `void*` -  it is a pointer which can store any data type  of variables




# Precedence

Order to perform operators:
- ()	        Highest
- []	        Highest	
- ++, --	High (Unary)	
- `*`, /, %	High (Binary)	
- +, -	        Medium	
- =, +=, -=	Low
If two or more Operators have same precedence perform them by **associativity**.
- **Left-to-right** associativity means the operators are evaluated from **left to right**. Common for most binary operators (`+`, `-`, `*`, `/`).
- **Right-to-left** associativity means the operators are evaluated from **right to left**. Common for assignment (`=`), conditional (`?:`), and post-increment (`i++`) operators.
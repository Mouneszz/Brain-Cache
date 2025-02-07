```cpp
// way to find a the left most bit of an number 
int  a=5; //a||5 = 0100
if(a&1==1){ // 0100 & 0001 returns 1||0001
	cout<<"The left most bit is 1";
}
```
Swaping two numbers without three variables
use xor to swap 
```cpp
int a = 5;
int b = 6;
a  = a^b; // a = 5^6  : a = 3;
b = a^b; // a = 3^6 : b = 5;
a = a^b; // a = 3^5 : a = 6; 
```



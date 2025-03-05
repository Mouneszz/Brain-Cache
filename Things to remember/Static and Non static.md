**Static**:
Static member is same for every instance of the class it cannot be changed if an new object change the static data member will also change  other objects.
```cpp
#include <iostream>
using namespace std;
class base{
public:
    int x;
 static int y;
};
int base::y = 0; // this line is important, as we declared in  the class but we should define this outside class to access
int main() {
    base a;
    base b;
    a.y = 20;
    cout<<a.y<<endl;
    base::y=40;
    cout<<a.y;
    return 0;
}
```

A Static function belongs to the class not the object
only access static members only
```cpp
classname::funcname();
```

**Non static function**:
A non static function belongs to the object
can access both static and non static functions
```cpp
classname obj;
obj.funcname();
```




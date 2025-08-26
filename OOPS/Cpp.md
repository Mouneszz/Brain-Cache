 ```cpp
 
 class student{
	 public:
	 int roll;
	 string name;
	 void display(){ // definition
	 cout<<roll<<endl;
	 cout<<name;
	 }
 };
 
```

When we want to  write a method/member functions outside of side the class, 
```cpp
 class student{
	 public:
	 int roll;
	 string name;
	 void display(string); // declaration
	
 };
  void student::display(string newname){ // definition
	 cout<<roll<<endl;
	 cout<<name;
	}
```

**Constructers**
It is a special method in which is called when an object is created name should be same as the class 
- no return type 
- We dont need to call manually like a member function


```cpp
 class student{
	 public:
	 int roll;
	 string name;
	 student(){ // non parameterized constructer
	 cout<<"A constrcuter is created"";
	 }
	 void display(string); // declaration
	
 };
  void student::display(string name){ // definition
	 cout<<roll<<endl;
	 cout<<name;
	}
```

There are two ways to create a object
```cpp
student student1("mounesh");

student* student1 = new student("mounesh");
```
### 1. `student student1("mounesh");`
- Creates a **stack object**.
- `student1` is an actual object of type `student`.
- Memory is automatically managed — when the scope ends, the destructor is called and memory is freed.
- Access members using `.`
Example:
```cpp
student student1("mounesh");
student1.display();   // dot operator
```
### 2. `student* student1 = new student("mounesh");`
- Creates a **heap object** using `new`.
- `student1` is a **pointer** to a `student` object.
- Memory is **not automatically freed** → you must manually `delete` it to avoid memory leaks.
- Access members using `->`
Example:
```cpp
student* student1 = new student("mounesh");
student1->display();   // arrow operator

delete student1;       // free memory

```

***If we dont provide any access specifier it will automatically be a private***

***Access specifiers***
- *Public* -  can access from the main class also and from the class itself
- *Private* - Cannot able to access from outside of this class 
- *Protected*  - cannot be accessed from the main class but can be accessed by the child class even it is inherited with a **Private** key


### Inheritance
```cpp
class  childclass : public parentclass {

} 
```

**Scope Ambiguous  operator** (`::`)
In multiple inheritance if two parent classes  have **same variable names** then we use `::`
before the name to ensure it is being used from that specific class
```cpp
parentclass::variablename 
```
***And if variable name in the child class is same as the parent class it can be overridden***

**Type of inheritance**
- Single - Having a single parent class inherited
- Multiple - having more than one parent classes
- Multi level - having a parent class which is a child class
- Hierarchical - having more than one child class
- Hybrid - using more than one type of  inheritance 

```cpp
#include <iostream>
using namespace std;

class Parent {
public:
    void pubFn() { cout << "Public fn\n"; }
protected:
    void protFn() { cout << "Protected fn\n"; }
private:
    void privFn() { cout << "Private fn\n"; }
};

class ChildPublic : public Parent {
public:
    void test() {
        pubFn();    // ✅ accessible
        protFn();   // ✅ accessible
        // privFn(); // ❌ not accessible
    }
};

class ChildPrivate : private Parent {
public:
    void test() {
        pubFn();    // ✅ still accessible inside child
        protFn();   // ✅ still accessible inside child
    }
};

int main() {
    ChildPublic cp;
    cp.pubFn();     // ✅ works (public stays public)
    // cp.protFn(); // ❌ error (protected not visible outside)
    // cp.privFn(); // ❌ error (private never visible)

    ChildPrivate cpr;
    // cpr.pubFn(); // ❌ error (became private in ChildPrivate)
    cpr.test();     // ✅ child can still use Parent’s functions internally
}

```

### Polymorphism

Compile time Polymorphism - Overloading 
Run time Polymorphism - Overriding 

**Overloading**
```cpp
class Test {
public:
    void print(int x)   { cout << "int: " << x << endl; }
    void print(double y){ cout << "double: " << y << endl; }
};

int main() {
    int n;
    cin >> n;   // runtime value
    Test t;
    t.print(n); // compiler already decided: print(int)
}
```

**Overriding**
When we only know the class type in the runtime and we want to have a overridable function in the base class so use virtual function (*Runtime Overriding*)
Having *Pure virtual function* in a class will not let you to  create obj() of the base class. we should override it with the derived class methods 

```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
using namespace std;
class remote{
    public:
    virtual void show(){
        cout<<"A Normal remote"<<endl;
    }
};
class ac: public remote{
    public:
    void show(){
        cout<<"AC remote"<<endl;
    }
};
class tv: public remote{
    public:
    void show(){
        cout<<"TV remote"<<endl;
    }
};
int main() {
    remote* pt1 = new tv();
    pt1->show();
    
    remote* pt2 = new ac();
    pt2->show();
    return 0;
}
```
Here the class remote function `show` is overridden by the derived class.
if we make it as pure virtual function like 
```cpp
class remote{
    public:
    virtual void show() = 0;
};
```
here even if we simply create an object for the base class we cannot 
```cpp
 remote* pt3 = new remote()
    pt3->show(); // this is not possible because now its a abstract class
```

**If it is a normal virtual function** we can create a object for that class with that class pointer to class obj.
but if it is **pure virtual function**  we will not be able to create a obj for its own with the base class pointer


### Abstract class
If a **base class has at least one pure virtual function**, that class becomes an **abstract class** in C++.

👉 **Abstract class rule:**
- You **cannot** create an object of an abstract class.
- But you **can** create pointers or references of the abstract class type and point them to derived class objects.


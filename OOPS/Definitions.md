**Class** - A **class** is a user-defined blueprint or template in object-oriented programming (OOP) that is used to create objects. It groups  data members (like variables) and member functions (like methods) into a single unit.

Objects - An instance of a class. which  holds the class's data members and member functions. A class is like a blueprint but the object is the concrete representation of it.

**Four main principles of oops:**
- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

**Encapsulation:**
- So its nothing, just having data members and member functions inside a class is called is Encapsulation.
**Abstraction**:
- Hiding unnecessary  information and showing the Essentials.
**Inheritance:**
- A class inheriting its data members and member functions from another class.
- Types:
	 - Single
	 - Multiple
	 - Hierarchical 
	 - Hybrid
	 - Virtu
**Polymorphism**:
	 Types:
	 - Function Overloading 
	 - Operator Overloading 
- A function name can be used as many times as possible if the arguments passed is different it takes many forms based on the operator.

**Access Specifiers:**
- Public: Any one can access even outside.
- Private: Only inside the class is accessible and the derived classes can not access it.
- Protected:  can access in both inside the class and by derived classes.



Virtual function:
-  A function in class  which must be override  by other derived class.
-  That class cannot create object of it own.
```cpp
class shape{
public:
virtual viod func() = 0;
}
```
The `= 0` makes it a **pure virtual function**.


Abstract class:
-  A class which cannot be used to create  objects but can be inherited by  other classes.
-  A class with minimum one virtual function  is called Abstract class.

Constructor:
- Calls when the class is created.
Types:
- Default 
- Parameterized 
- Copy Constructer


**Friend Function/Class**:
A function which is not a member function but can still access the private ,protected data members and member functions.

For function:
` friend returntype functionname(arguments)`
For Class:
 `friend class classname`
 
we should declare this inside a class so in the function/class  we can use the private and protected data members, member functions.













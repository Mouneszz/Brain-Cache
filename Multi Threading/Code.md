
```cpp
#include<iostream>
using namespace std;
bool isodd(int num){
	if(num%2!=0) return true;
}
int main(){
	std::thread t1(isodd(),2);
	std::thread t2(isodd(),3);
	t1.join();
	t2.join();
	return 0;
}
```
after the thread creation function  continues  to execute in main function so we use  join() to wait for it complete before executing the return 0.

```cpp
t1.detach();
```
so when  we declare a thread we should either use join or detach so the main thread can wait for the child thread to finish or abandon   the child and take no ownership to it and the child grows in the background .
if we didn't do anything when the function call ends before the thread to finish an exception error will be called so it is a good practice to detach a thread if the work can be  done  in background.

```cpp
this_thread::sleep_for(chrono::seconds(5));
```
Its not  related but quite fun and useful.
**Mutex:**
```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;
int amount = 0;
std:: mutex m;
void addamount(){
	m.lock();
	amount++;
	m.unlock();
}
int main(){
	thread t1(addamount);//t1 access amount and locks it
	thread t2(addamount);//t2 waits for t1 to perform unlock so t1 can access it.
	t1.join();
	t2.join();
	cout<<amount<<endl;
	return 0;
}
```
we use  mutex when both threads access a  global  variable  and  try changing  it, that section cause critical section so we use m,lock() this locks that section when the any one of the thread access the next thread waits for the first thread to unlock it so it can use that amount


try_lock() it can act as a condition to check if the mutex is locked or not unlike lock() does not wait just return true or false.
```cpp
int amount=0;
void addamount(){
	for(int i=0;i<100000;i++){
	 if(m.try_lock()){ // if mutex is not locked, lock it and produce true 
		cout<<"Mutex is locked"<<endl;
		amount++;
		m.unlock(); // unlocks the mutex 
	 }
	 else{
		cout<<"Mutex is locked by another thread"<<endl;
	 }
	 }

}
int main(){
	thread t1(addamount);// here the lock locks the mutex
	thread t2(addamount); // when this thread is called it checks is the mutex is locked or not if not the try_lock  executes or skips the if and next loop
	t1.join();
	t2.join();
	cout<<amount<<endl;
	return 0;
}
```
Recursive mutex:
so when we lock  in recursion and call recursion it will create a dead lock situation  so we use recursion mutex to lock even when the mutex is already locked it still lock it and move
if  recursive mutex is locked 10 times by  a thread and  then that thread should unlock the mutex 10 times.
```cpp
std::recursive_mutex m1;
void recursive(int one){
if(one==ten) return;
one++;
m1.lock();
recursive(one);
m1.unlock();
}
```
above the t1 should unlock and lock the  mutex same(10) number of times.

Lock Guard:
The Syntax for the lock guard is 
```cpp
std:: lock_guard<mutex> lock(m1) // its a template class so we need to give mutex and create a objet with passing mutex into it.
```
So we use lock(m1) instead of m1.lock(),m1.unlock() it will perform both.
```cpp
#include<iostream>
#include<thread>
#include<mutex>
using namespace std;
std:: mutex m1;
int buffer=0;
int global=0; //its a global
void printtimes(int n,const char* tname){
	lock_guard<mutex> lock(m1);
	for(int i=0;i<n;i++){
	cout<<tname << ":" << ++buffer <<endl
	}
}
int main(){
thread t1(printtimes,5,'T1');
thread t2(printtimes,5,'T2');
t1.join();
t2.join();
return 0;
}
```
In the above code we dont explicitly unlock the m1 mutex but in here  by using the lock guard it will automatically unlock the m1 mutex when the lock in lock guard goes out of scope. 
- when we create the lock obj it automatically locks the m1.
- We cannot explicitly unlock the lock guard.

***Timed Mutex***
- Locking Mutex by using try_lock_for(chrono::seconds(5);
- If the mutex is already locked than it will wait for the mutex to unlock for the seconds mentioned after that it will return 0 and move on to the next condition.
```cpp
#include <iostream>
#include <thread>
#include <mutex>
#include <chrono>
using namespace std;

timed_mutex m1; // should intialize timed_mutex so we can use try_lock_for
void summa(const char* name){
    if(m1.try_lock_for(chrono::seconds(3))){ 
        cout<<"This thread is on progress: "<<name<<endl;
        this_thread::sleep_for(chrono::seconds(4));
        m1.unlock();
    }
    else{
        cout<<"This thread is blocked: "<<name<<endl;
    }
    
}
int main() {
    thread t1(summa,"T1");
    thread t2(summa,"T2");
    t1.join();
    t2.join();
    return 0;
}

```
In the above code which  thread first access the mutex and lock it will perform for 4 seconds and by that time the another thread will wait for 3 seconds then it proceeds to next case.

**Unique Lock**
- It is template like lock guard
- It is a mutex wrapper and take ownership of the entire mutex
```cpp
unique_lock<mutex> lock(m1);
```








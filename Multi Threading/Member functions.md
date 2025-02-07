```cpp
t1.join();
```
the main function waits for t1 to finish.
```cpp
t1.detach();
```
we  should either use join or detach.
when detached the t1 thread is not under the main thread, it run independently
even after main ends but when the program terminates it ends.
```cpp
//mutex m1;
m1.lock();
```
this code locks the m1 mutex so  if two or more threads try to access the race section the first one locks after that next threads will wait for the first thread to unlock().
```cpp
m1.unlock();
```
this unlocks the lock which is executed .
```cpp
if(m1.try_lock());
```
it returns 0 if it is already locked and so the thread can go down or perform next codes. Instead of waiting buy using m1.try_lock can execute  below codes.
```cpp

```

### Bubble Sort
Intuition: In a single iteration the last value should be placed right so the second loop range is decremented by i `j<n-i-1`. If the the current j is larger than j+1 than we swap.
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <vector> 
using namespace std;
int main() {
    vector<int> vec = {5,4,3,2,1};
    int n = vec.size();
   for(int i=0;i<n-1;i++){
       int swapped =0;
       for(int j=0;j<n-i-1;j++){
           if(vec[j]>vec[j+1]){
               int temp = vec[j];
               vec[j] = vec[j+1];
               vec[j+1] = temp;
               swapped =1;
           }
       }
       if(!swapped){
           return 0;
       }
       for(int i:vec){
           cout<<i<<" ";
       }
       cout<<endl;
   }
    return 0;
}
```

### Selection Sort
Intuition: Find the min the from range of  `j to n` where `j=i+1` because we have to change the `i`
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <vector> 
using namespace std;
int main() {
    vector<int> vec = {5,4,3,2,1};
    int n = vec.size();
    for(int i=0;i<n-1;i++){
        int minindex = i;
        for(int j=i+1;j<n;j++){
            if(vec[j]<vec[minindex]){
                minindex = j;
            }
        }
        int temp = vec[minindex];
        vec[minindex] = vec[i];
        vec[i] = temp;
        
        for(int i:vec){
            cout<<i<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```

### Insertion Sort
Intuition : It is similar to find the correct position of an element in an array to insert, but we have to do it from index `1`  to all numbers
```cpp
// Online C++ compiler to run C++ program online
#include <iostream>
#include <vector> 
using namespace std;
int main() {
    vector<int> vec = {5,4,3,2,1};
    int n = vec.size();
    for(int i=1;i<n;i++){
        int key = vec[i];
        int j=i-1;
        while(j>=0 && vec[j]>key){
            vec[j+1]=vec[j];
            j--;
        }
        vec[j+1]=key;
        for(int i:vec){
            cout<<i<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```
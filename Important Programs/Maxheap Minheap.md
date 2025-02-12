[973. K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)
Intuition : This problem is similar to the largest kth element in the stream its opposite version of that problem here we declare a max heap to store  k elements if the heap size become greater than we pop the top element so we get the k closest elements to the origin.
```cpp
class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        priority_queue<pair<int,vector<int>>> maxheap;
        for(auto it:points){
            int dist = it[0]*it[0]+it[1]*it[1];
            maxheap.push({dist,it});
            if(maxheap.size()>k){
                maxheap.pop();
            }
        }
        vector<vector<int>> ans;
        while(!maxheap.empty()){
            ans.push_back(maxheap.top().second);
            maxheap.pop();
        }
        return ans;
    }
};
```
[1985. Find the Kth Largest Integer in the Array](https://leetcode.com/problems/find-the-kth-largest-integer-in-the-array/)
Intuition: it is similar other heap problems but what makes it medium difficulty is that when we compare string in lexicographical using operators like `>` it checks them by char by char. so by that logic "10" is smaller than "3" so to deal with that if we try to use `stoi` them while pushing it into heap and converting to string and return will cause out of bound error the range is `int`.
- so to solve the above problems we create custom comparator function which gives the order inside the priority queue. 
- We are passing the our comp function instead of the `greater<int>` so we need to pass it inside declare type `decltype` and also explicitly pass the comp in minheap.
- also we should pass the function by the address `&` .
```cpp
class Solution {
public:
    static bool comp(string& a,string& b){
        if(a.size()==b.size()) return a>b;
        return a.size()>b.size();
    }
    string kthLargestNumber(vector<string>& nums, int k) {
        priority_queue<string,vector<string>,decltype(&comp)> minheap(&comp);
        for(string i:nums){
            minheap.push(i);
            if(minheap.size()>k){
                minheap.pop();
            }
        }
        return minheap.top();
    }
};
```
[621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)
Intuition: the intuition is to run and remove the each tasks frequency by one and add n+1 to the answer when the queue become empty just add the temp vector size.
```cpp
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
       unordered_map<char,int> mpp;
       for(char& ch:tasks){
        mpp[ch]++;
       }
       priority_queue<int> qu;
       for(auto m:mpp){
        qu.push(m.second);
       }
       int time=0;
       while(!qu.empty()){
        vector<int> temp;
        for(int i=0;i<n+1;i++){
            if(!qu.empty()){
                temp.push_back(qu.top());
                qu.pop();
            }
        }
        for(int i:temp){
            if(--i>0){
                qu.push(i);
            }
        }
        time += qu.empty()?temp.size():n+1;
       }
       return time; 
    }
};
```

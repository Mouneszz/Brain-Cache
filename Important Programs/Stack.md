[Daily Temperatures](https://leetcode.com/problems/daily-temperatures/)
Intuition -  Its similar to next greater element so we traverse from last  and append the their index and value into stack.  And check if the top element of the stack is lesser than the current element than we pop it. And add 0 zero to answer if the stack is empty that means we have no next greater element than the current.  if its not empty than add the stack top elements index - i, for every iteration we add the i and value to the stack.
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temp) {
        int n = temp.size();
        vector<int> ans;
        stack<pair<int,int>> st;
        for(int i=n-1;i>=0;i--){
            while(!st.empty() && st.top().second<=temp[i]){
            st.pop();
            }
            if(st.empty()) ans.push_back(0);
            else ans.push_back(st.top().first - i);
            st.push({i,temp[i]});
        }
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```
[84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)
Intuition  - So here the problem we have to push elements which are greater than which are in the `st.top()` if not than we find the its height because it will not in the range anymore so here to find the area we have to find the width by `i-st.top()-1` i is the height' next smaller element and
`st.top()` is the previous smaller element so we find  the area by multiplying height and width.
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& nums) {
       stack<int> st;
       int  n= nums.size();
       int maxi = 0;
       for(int i=0;i<=n;i++){ //i<=n is important as it it will go the another iteration and when i==n the current will be zero so the for the elements inside the stack it is thier next smaller element.
        int current = (i==n)?0:nums[i]; 
        while(!st.empty() && current<nums[st.top()]){// found the next smaller element
            int height  = nums[st.top()]; // height if the element
            st.pop(); //  pop to find the previous smaller element
            int width = st.empty()? i : i-st.top()-1; // is it is empty it means there are no smaller element to its left so its zero we simply take width as i
            maxi = max(maxi,height*width);
        }
        st.push(i);
       }
       return maxi;
    }
};
```



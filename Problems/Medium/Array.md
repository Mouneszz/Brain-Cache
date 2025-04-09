[1493. Longest Subarray of 1's After Deleting One Element](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element/)
#slidingwindow 
Intuition : it is same as the  longest subarray 1 after removing k zero, here we have to see if we have got a zero second time by checking a flag , if yes then  move the left until we cross the previous zero and get the length.
```cpp
class Solution {
public:
    int longestSubarray(vector<int>& nums) {
        int left =0;
        int right =0;
        bool iszero = false;
        int ans =0;
        while(right<nums.size()){
            if(nums[right]==0 && iszero){
                while(nums[left]!=0){
                 
					left++;
                }
                left++;
            }
            else if(nums[right]==0){
                iszero = true;
            }
            ans = max(ans,right-left);
            right++;
        }
        return ans;
    }
};
```


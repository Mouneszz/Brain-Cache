[1. Two Sum](https://leetcode.com/problems/two-sum/)
#array #hashmap 
Intuition :  We can simply can have to loops but TC - O(n^2), To optimize the time complexity we can use hash map,  get the difference of the of the num and the target , check is the diff is present in the map if present that that is the two sum, push `i`  as value and  `nums[i]` as key.
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> mpp;
        for(int i=0;i<nums.size();i++){
            int diff = target-nums[i];
            if(mpp.count(diff)){
                return {mpp[diff],i};
            }
            mpp[nums[i]]=i;
        }
        return {};
    }
};
```

[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
#array #twopointer 
Intuition:  Take Two pointers `left` and `right`, the length `l` will be minimum of the `height[left] and height[right]`. the breadth `b` will be `right - left`.
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n=height.size();
        int left=0,right=n-1,ans=0;
        while(left<right){
            int l = min(height[left],height[right]);
            int b = right-left;
            int area = l*b;
            ans=max(ans,area);
            if(height[right]>height[left]){
                left++;
            }
            else{
                right--;
            }
        }
        return ans;
    }
};
```

[169. Majority Element](https://leetcode.com/problems/majority-element/)
#array 
Intuition:  There could be only two elements in the entire array, create  two variables to have a  track of which we currently have,  increment count when `nums[i]` = num , and decrement count if it differs , check when `count==0` that means that previous range have equal count of both, 
so make the `num = nums[i]` so we can keep track. finally `num` will have the  number which is major.
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int num=nums[0],count=0;
        for(int i:nums){
            if(i==num) count++;
            else if(count==0){
                num = i;
            }
            else count--;
        }
        return num;
        
    }
};
```

[53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
#array #subarray
Intuition : When ever we get the sum as negative we make the sum as 0, also check for it before the `sum+=i` because we have to check before we adding the number.
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans=INT_MIN;
        int sum=0;
        for(int i:nums){
            if(sum<0){
                sum=0;
            }
            sum+=i;
        
            ans=max(sum,ans);
        }
        return ans;
    }
};
```

[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
#array #binarysearch 
Intuition: So its a rotated sorted array first we have to find correct sorted partition so the first `if else` will find the correct partition , than the inner conditions will decide either that partition  **left to mid**  have the target or the other  **mid to right** .
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = nums.size();
        int l =0,r=n-1;
        while(l<=r){
            int mid = (l+r)/2;
            if(nums[mid]==target) return mid;
            if(nums[mid]>=nums[l]){
                if(target>=nums[l] && target<=nums[mid]){
                    r=mid-1;
                }
                else{
                    l=mid+1;
                }
            }
            else{
                if(target>=nums[mid] && target<=nums[r]){
                    l=mid+1;
                }
                else{
                    r=mid-1;
                }
            }
        }
        return -1;
    }
};
```
**Love Triangle**
#array 
Intuition: get the tree check is the third ones lovers is the first one if yes print "Yes".
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;
    int f[n + 1];
    for (int i = 1; i <= n; i++) {
        cin >> f[i];
    }
    for (int i = 1; i <= n; i++) {
        int a = f[i];
        int b = f[a];
        int c = f[b];
        if (c == i) {
            cout << "YES" << endl;
            return 0;
        }
    }
    cout << "NO" << endl;
    return 0;
}

```
[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
intuition : so to find the first position of the element given we have to do the lower bound
- lower bound -  return target element pointer if its there or return the next greater element pointer
- upper bound -  only return the next greater element pointer
```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res(2,-1);
        auto lower = lower_bound(nums.begin(), nums.end(), target);
        auto upper = upper_bound(nums.begin(), nums.end(), target);

        if (lower != nums.end() && *lower == target) {
            res[0] = lower - nums.begin();
            res[1] = upper - nums.begin() - 1;
        }
        return res;
    }
};
```
[875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
#binarysearch #array
Intuition  - So here the problem is tricky to solve first we have to find the max in the piles which is the minimum guaranteed speed in which we can finish the piles so we take it as right , and 1 as left
also create a helper function in which we pass the mid as a speed and check if the mid speed is enough or not if enough than we move the right pointer to mid, else move the left to mid+1.
```cpp
class Solution {
public:
    bool canfinish(int speed,vector<int>& piles,int h){
        int hours=0;
        for(int pile:piles){
            hours+=ceil((double)pile/speed);
        }
        return hours<=h;
    }
    int minEatingSpeed(vector<int>& piles, int h) {
        int left =1,right =1;
        for(int n:piles){
            right = max(right,n);
        }
        while(left<right){
            int mid = left + (right-left)/2;
            if(canfinish(mid,piles,h)){
                right = mid;
            }
            else{
                left = mid+1;
            }
        }
        return left;
    }
};
```
[153. Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)
#binarysearch 
Intuition  -  Similar to other binary search problems but we first check if the left to right is already sorted,  and if the left is smaller than the right that means the array is only sorted on left so we move to right if not than we move to left. finally we return number which is pointed by left.
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l = 0, h = nums.size() - 1;
        while (l < h) {
            int mid = (l + h) / 2;
            if (nums[l] <= nums[h]) return nums[l];// if array is already sorted
            
            if (nums[mid] >= nums[l]) { // left is sorted so  move to right
                l = mid + 1;
            } else {
                h = mid;// right is sorted so move to left
            }
        }
        return nums[l];  
    }
};

```

[33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
Intuition its like the above problem but instead of find the smallest element we have to find the target we is  two nested if , else to find if the mid is greater than the left it means it is a sorted range so we check if the target is present if it is than we move the right .
```cpp

```
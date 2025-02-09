[2364. Count Number of Bad Pairs](https://leetcode.com/problems/count-number-of-bad-pairs/)
Intuition : Here the main concept is if it is s bad pair that means `nums[j]-nums[i]!=j-i` so if we rearrange this `nums[j]-j!=nums[i]-i` for good pairs it should be `nums[j]-j==nums[i]-i` is also written as `diff[j]==diff[i]`, so if we encounter a same index in `diff` map it means good pair two numbers with same difference possible so we minus it with the total pair count to get bad pairs.
```cpp
class Solution {
public:
    long long countBadPairs(vector<int>& nums) {
        int n = nums.size();
        long long totalPairs = (long long)n * (n - 1) / 2;
        unordered_map<int, long long> diffCount;
        for (int i = 0; i < n; i++) {
            int diff = nums[i] - i;
            totalPairs -= diffCount[diff];
            diffCount[diff]++;
        }
        return totalPairs;
    }
};
```

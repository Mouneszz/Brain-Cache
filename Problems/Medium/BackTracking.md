[1415. The k-th Lexicographical String of All Happy Strings of Length n](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/)
#backtracking #recursion
Intuition : its like normal permutation but with two different cases
- first we are given  `n` which should be the string length 
- no same two consecutive characters should be present we only do recursion when the string `ds` is empty and `ds.back!=nums[i]`. 
we dont have an index and increment and pass it to the next recursion because the for loop will does that.
```cpp
class Solution {
public:
    void back(string& ds,vector<string>& vec,vector<char>& nums,int n){
        if(ds.size()==n){
            vec.push_back(ds);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(ds.empty() || ds.back()!=nums[i]){
                ds.push_back(nums[i]);
                back(ds,vec,nums,n);
                ds.pop_back();
            }
        }
    }
    string getHappyString(int n, int k) {
        vector<string> vec;
        vector<char> nums = {'a','b','c'};
        string ds="";
        back(ds,vec,nums,n);
        cout<<vec[0];
        if(k>vec.size()){
            return "";
        }
        return vec[k-1];
    }
};
```
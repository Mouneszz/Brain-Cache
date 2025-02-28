[Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)
#slidingwindow #hashmap 
Intuition:  create a map for the p string to check if with the another map we create in while sliding the window . 
 -  create a private function `is_valid` to check if the two maps match.
 -  use left and right variables as the edges of the window increment the window in every iteration and add that character to the map,
 - if the current window size exceeds the p string than short the window by incrementing the left and removing its char frequency in the first map.
```cpp
class Solution {
private:
    bool isvalid(unordered_map<char,int>& mpp1,unordered_map<char,int>& mpp2){
        for(auto m:mpp2){
            if(mpp1.find(m.first)==mpp1.end()){
                return false;
            }
            else if(mpp1[m.first]!=m.second){
                return false;
            }
        }
        return true;
    }
public:
    vector<int> findAnagrams(string s, string p) {
        int left = 0;
        int right = 0;
        unordered_map<char,int> mpp1;
        unordered_map<char,int> mpp2;
        vector<int> ans;
        int psize = p.size();
        for(const auto& ch:p){
            mpp2[ch]++;
        }

        while(right<s.size()){
            char c = s[right];
            mpp1[c]++;
            int currsize = right-left+1;
            if(currsize>psize){
                mpp1[s[left]]--;
                left++;
            }
            if(isvalid(mpp1,mpp2)){
                ans.push_back(left);
            }
            right++;
        }
        return ans;
    }
};
```
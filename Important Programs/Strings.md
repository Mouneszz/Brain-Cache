[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
#hashmap #twopointer #slidingwindow
Intuition - Create a HashMap to store the the indices of the previously visited character
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(s.size()==0) return 0;
        if(s.size()==1) return 1;
        int right =0;
        int left = 0;
        int n =  s.size();
        unordered_map<char,int> mpp;
        int ans=0;
        while(right<n){
            char ch = s[right];
            if(mpp.count(ch)){// returns the count else 0.
                if(mpp[ch]+1>left)//Important
                left = mpp[ch]+1;
            }
            ans = max(ans,right-left+1);
            mpp[ch] = right;
            right++;
        }
        return ans;
    }
};
```
[424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
#hashmap #slidingwindow #twopointer 
Intuition  -  same like the previous problems but here we carry a maxi which have  the max occurrence  of a char.
**(Length-maxi) <=k**
maxi  - maximum number of a char which is in the window.
if we  met the above condition we calculate the length max.
if not than we minus the chars occurrence and increment the left.

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        int left =0,right= 0,ans=0,maxi=0;
        vector<int> occ(26,0);
        while(right<s.size()){
            char ch  = s[right];
            occ[ch-'A']++;
            maxi =max(maxi,occ[ch-'A']); // Finding max of the char occurrence
            if((right-left+1)-maxi>k){   //Important
                occ[s[left]-'A']--;
                left++;
            }
            else ans = max(ans,right-left+1);
            right++;
        }
        return ans;
    }
};
```
[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)
#slidingwindow #hashmap 
Intuition - So there are two strings s1 and s2 in which we have find if any permutation of s1 inside of s2. First we should not think it as a total permutation problem here we can create a frequency map for s1 and create one for s2 in the size of s1 and start a loop which should not exceeds the size of s2 - s1.size() so we can simply add i+s1.size()   to access the right limit of the window and simply use i as the left limit.
***Window Size***  - S1.size();
```cpp
class Solution {
private:
 bool matches(vector<int>& mpp1,vector<int>& mpp2){
    for(int i=0;i<26;i++){
        if(mpp1[i]!=mpp2[i]){
            return false;
        }

    }
    return true;
 }
public:
    bool checkInclusion(string s1, string s2) {
        if(s1.size()>s2.size()) return false;
        vector<int> mpp1(26,0);
        vector<int> mpp2(26,0);
        for(int i=0;i<s1.size();i++){
            mpp1[s1[i]-'a']++;
            mpp2[s2[i]-'a']++;
        }
        for(int i =0;i<s2.size()-s1.size();i++){
            if(matches(mpp1,mpp2)) return true;
            mpp2[s2[i+s1.size()]-'a']++;
            mpp2[s2[i]-'a']--;
        }
        return matches(mpp1,mpp2);
    }
};
```

[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)
#hashmap #slidingwindow #twopointer 
Intuition  -  Its  similar compared to previous but  we want to find the  minimum window in S.
So the approach is to create a map and store the t and its frequency , do a two pointer sliding window approach and call the mini update your value of the start index of the s. and create a matches function to check if the mpps have enough for mppt and if true increment left and decrease the left frequency and add the min of mini. otherwise right increment.
```cpp
class Solution {
private:
    bool matches(unordered_map<char,int>& mpps,unordered_map<char,int>& mppt){
        for(const auto& pair:mppt){
            if(mpps[pair.first]<pair.second) return false; //return false which the freq is lesser compared to mppt.
        }
        return true;
    }
public:
    string minWindow(string s, string t) {
        int left=0,right =0,mini =INT_MAX;
        int start=-1,end=-1;
        unordered_map<char,int> mpps;
        unordered_map<char,int> mppt;
        for(int i=0;i<t.size();i++){
            mppt[t[i]]++;
        }
        while(right<s.size()){
            mpps[s[right]]++;
            while(matches(mpps,mppt)){
                if(right-left+1<mini){
                    start=left;
                    end = right;
                    mini = right-left+1;
                }
                mpps[s[left]]--;
                if(mpps[s[left]]==0){
                    mpps.erase(s[left]);
                }
                left++;
            }
            right++;
        }
        if(start==-1) return "";
        return s.substr(start,mini);
    }
};
```
[22. Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
#backtracking 
Intuition  -  there are two conditions here we can have the closing parenthesis  is it is smaller than the opening and can have the opening brackets lesser than n
```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        string ds="";
        vector<string> ans;
        dfs(0,0,n,ds,ans);
        return ans;
    }
    void dfs(int open,int close,int n,string ds,vector<string>& ans){
        if(open == close && open+close==n*2){
            ans.push_back(ds);
            return;
        }
        if(open <n){
            dfs(open+1,close,n,ds+"(",ans);
        }
        if(close < open){
    dfs(open, close + 1, n, ds + ")", ans);
         }
        return;
    }
};
```

[127. Word Ladder](https://leetcode.com/problems/word-ladder/)
#bfs 
Intuition: We have to  use bfs to solve this problem, easy bfs we have to change every char in the string from  a to z and check if it presents, yes than add that to the queue.
- have a pair inside queue so we can return the steps it needed.
```cpp
class Solution {
public:
    int ladderLength(string beginword, string endword, vector<string>& wordList) {
        queue<pair<string,int>> qu;
        qu.push({beginword,1});
        unordered_set<string> st(wordList.begin(),wordList.end());
        st.erase(beginword);
        while(!qu.empty()){
            string word = qu.front().first;
            int steps = qu.front().second;
            qu.pop();
            if(word==endword) return steps;
            for(int i=0;i<word.size();i++){
                string orginal  = word;
                for(char ch = 'a';ch<='z';ch++){
                    word[i]=ch;
                    if(st.find(word)!=st.end()){
                        st.erase(word);
                        qu.push({word,steps+1});
                    }
                    word = orginal;
                }
            }
        }
        return 0;
    }
};
```



[78. Subsets](https://leetcode.com/problems/subsets/)
Intuition : So I am familiar with the back tracking we  have to create two calls one for pick and another one for not pick before the not pick call we have to pop the element from the ds.
```cpp
class Solution {
public:
    void sub(int index,vector<int> nums,vector<int>& ds,vector<vector<int>>& ans,int n){
        if(n==index){
            ans.push_back(ds);
            return;
        }
        ds.push_back(nums[index]);
        sub(index+1,nums,ds,ans,n);
        ds.pop_back();
        sub(index+1,nums,ds,ans,n);
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> ds;
        sub(0,nums,ds,ans,nums.size());
        return ans;
    }
};
```
[39. Combination Sum](https://leetcode.com/problems/combination-sum/)
Intuition: It is similar to the above problem here we only have to check if the value which we are going to add is smaller than the target if it is we perform the pick backtrack call and after that  call end we pop. while passing the target subtract it with the value you took.
```cpp
class Solution {
public:
    void sub(int index,vector<int>&arr,int target,vector<vector<int>>& ans,vector<int>& ds){
        if(index==arr.size()){
            if(target==0){
                ans.push_back(ds);
            }
            return;
        }
        if(arr[index]<=target){
            ds.push_back(arr[index]);
            sub(index,arr,target-arr[index],ans,ds);
            ds.pop_back();
        }
        sub(index+1,arr,target,ans,ds);

    }
    vector<vector<int>> combinationSum(vector<int>& arr, int target) {
        vector<vector<int>> ans;
        vector<int> ds;
        sub(0,arr,target,ans,ds);
        return ans;
    }
};
```
[40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
Intuition: The main difference is we have to only take the  distinct elements to pick to get the target sum, so we run a for loop and we continue the iteration if we have the same value as  the previous one.  Here we dont have to do the un pick stuff because the condition in the for loop does it with the if  condition.
```cpp
class Solution {
public:
    void sub(int index,int target,vector<int>& arr,vector<vector<int>>& ans,vector<int>&ds){
            if(target==0){
                ans.push_back(ds);
                return;
        }
            for(int i=index;i<arr.size();i++){
                if(i!= index && arr[i]==arr[i-1]) continue;
                if (arr[i] > target) break;
                    ds.push_back(arr[i]);
                    sub(i+1,target-arr[i],arr,ans,ds);
                    ds.pop_back();
            }
    }
    vector<vector<int>> combinationSum2(vector<int>& arr, int target) {
        vector<int> ds;
        sort(arr.begin(),arr.end());
        vector<vector<int>> ans;
        sub(0,target,arr,ans,ds);
        return ans;
    }
};
```
[90. Subsets II](https://leetcode.com/problems/subsets-ii/)
Intuition: same as the combination sum II we dont perform the not pick operation  because the not picking is performed by the for loop if we encounter same element in the same recursion level we skip it.
```cpp
class Solution {
public:
    void recur(int index,vector<int>& nums,vector<int>& ds,vector<vector<int>>& ans){
        ans.push_back(ds);
        for(int i=index;i<nums.size();i++){
        if(i!=index && nums[i]==nums[i-1]) continue;
        ds.push_back(nums[i]);
        recur(i+1,nums,ds,ans);
        ds.pop_back();
    }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
    vector<vector<int>> ans;
    vector<int> ds;
    sort(nums.begin(),nums.end());
    recur(0,nums,ds,ans);
    return ans;
    }
};
```
[131. Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)
Intuition: here its normal backtracking but slight difficult to understand the main goal is to check if that range from index to  i is palindrome if it is then add into the ds. all distinct char will be a palindrome so after that call we remove the last single char and check the index to i(index+1 ) range if its is a palindrome if it is then we add that and check for the index becoming the size of the string.  if it is then add that to the ans.
```cpp
class Solution {
public:

    void par(int index,string & str,vector<string>& ds,vector<vector<string>> & ans){
        if(index==str.size()){
            ans.push_back(ds);
            return;
        }
        for(int i=index;i<str.size();i++){
            if(ispalin(str,index,i)){
                ds.push_back(str.substr(index,i-index+1));
                par(i+1,str,ds,ans);
                ds.pop_back();
            }

        }
    }
    bool ispalin(string& str,int index,int i){
        while(index<=i){
            if(str[index]!=str[i]) return false;
            index++;
            i--;
        }
        return true;
    }
    vector<vector<string>> partition(string s) {
    vector<vector<string>> ans;
    vector<string> ds;
    par(0,s,ds,ans);
    return ans;
    }
};
```
For the input `aab`
```
Start at index 0
 ├── "a" (index 0-0) → Move to index 1
 │   ├── "a" (index 1-1) → Move to index 2
 │   │   ├── "b" (index 2-2) → Move to index 3 (Base case)
 │   │   └── ✅ ["a", "a", "b"] added to ans
 │   └── "ab" (index 1-2) ❌ (Not a palindrome)
 ├── "aa" (index 0-1) → Move to index 2
 │   ├── "b" (index 2-2) → Move to index 3 (Base case)
 │   └── ✅ ["aa", "b"] added to ans
 ├── "aab" (index 0-2) ❌ (Not a palindrome)
```
[17. Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)
Intuition : first create a vector for the digits and the values to access them by the index as the number in keypads, do a for loop to iterate over the letters inside the number in `digitchar` so we can generate all possible combinations we take the words by the index the index we get we check if the string size == index if its then add the string to the result and return.
```cpp
class Solution {
public:
    const vector<string> digitToChar = {
        "",
        "",     
        "abc",  
        "def",  
        "ghi",  
        "jkl",  
        "mno",  
        "pqrs", 
        "tuv",  
        "wxyz"  
    };
    void backtrack(int index,const string& digits,vector<string> &result,string& temp){
        if(index==digits.length()){
            result.push_back(temp);
            return;
        }
        string possi = digitToChar[digits[index]-'0'];
        for(const char& ch: possi){
            temp.push_back(ch);
            backtrack(index+1,digits,result,temp);
            temp.pop_back();
        }
    }
    vector<string> letterCombinations(string digits) {
        if(digits.empty()) return{};
        vector<string> result;
        string temp;
        backtrack(0,digits,result,temp);
        return result;
    }
};
```
[51. N-Queens](https://leetcode.com/problems/n-queens/)
Intuition: It is a hard problem, first the main thing is to find the backtrack logic so  there are certain conditions should be checked to place the queen in a position so we create a `isvalid` function to check is that position  is it valid. and  we mark the position as queen in board and after that recursion ends we unmark it we carry the `col` variable  as it points that in which column we should place the queen so we only have to iterate the rows. in `isvalid` we check for the is it present in the same row and is it present diagonally from both upward and downward, we dont check for the column as we increment the col once for every backtrack call.
```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<char>> board(n,vector<char>(n,'.'));
        vector<vector<string>> result;
        back(board,0,result);
        return result;
    }
    void back(vector<vector<char>>& board,int col,vector<vector<string>>& ans){
        if(col==board.size()){
            ans.push_back(construct(board));
        }
        for(int i=0;i<board.size();i++){
            if(isvalid(i,col,board)){
            board[i][col] = 'Q';
            back(board,col+1,ans);
            board[i][col] = '.';
            }
        }
    }
    vector<string> construct(vector<vector<char>>& board){
        vector<string> ans;
        for(int i=0;i<board.size();i++){
            string str="";
            for(int j=0;j<board.size();j++){
                str+=board[i][j];
            }
            ans.push_back(str);
        }
        return ans;
    }
    bool isvalid(int row,int col,vector<vector<char>>& board){
        for(int i=0;i<board.size();i++){ // checking the row 
            if(board[row][i]=='Q') return false;
        }
        for(int i = row,j =col;i>=0 && j>=0;i--,j--){ 
            if(board[i][j]=='Q') return false; // going left upwards
        }
        for(int i= row,j=col; i<board.size() && j>=0;i++,j--){
            if(board[i][j]=='Q') return false; // going left downwards
        }
    return true;
    }
};
```

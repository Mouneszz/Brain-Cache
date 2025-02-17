Reverse a Linked list:
#linkedlist 
```cpp
Node* reverse(Node* head){
Node* prev = nullptr;
Node* curr = head;
Node* next = nullptr;
	 while(curr!=nullptr){
		 next = curr->next;
		 curr->next = prev;
		 prev = curr;
		 curr = next;
	 }
	return prev;
}
```
Subsequence of n elements:
#backtracking
```cpp
void backtrack(int index,vector<int>& ds,vector<vector<int>>& ans,vector<int>& nums){
	if(index==nums.size()){
		ans.push_back(ds);
		return;
	}
	ds.push_back(nums[index]);
	backtrack(index+1,ds,ans,nums);
	ds.pop_back();
	backtrack(index+1,ds,ans,nums);
}
```
Permutation:
#backtracking 
```cpp
void backtrack(string& str, vector<bool>& used, string& ds, set<string>& result) {
        if (ds.size() == str.size()) { // Full-length permutation
            result.insert(ds); // Set ensures uniqueness
            return;
        }
        for (int i = 0; i < str.size(); i++) {
            if (used[i]) continue; // Skip already used characters
            used[i] = true;
            ds.push_back(str[i]);
            backtrack(str, used, ds, result);
            ds.pop_back();
            used[i] = false;
        }
```

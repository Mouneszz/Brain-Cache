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
DFS in Binary tree

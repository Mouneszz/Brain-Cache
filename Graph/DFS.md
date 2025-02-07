For Adjacency List
```cpp 
//assume you have the adjacent array or vector
// Only the recursion function write the main code own your own 
void dfs(int n,vector<int> ans,vector<vector<int>>& adj,unordered_map<int,bool> check){
	ans.push_back(n);
	check[n]=1;
	for(auto it:adj[n]){
		if(!check[it]){
			dfs(it,ans,adj,check);
		}
	}
}
```
For Adjacency Matrix
```cpp
```
For this the graph should be DAG(Directed Acyclic Graph).
```cpp
void dfs(int n,vector<vector<int>>& adj,stack<int> &st,vector<int>& check){
	check[n] = 1;
	for(int i:adj[n]){
		if(!check[i]){
			dfs(i,adj,st,check);
		}
	}
		st.push(n);
}
vector<int> topo(vector<vector<int>>& adj){
	int n = adj.size();
	vector<int> check(n,0);
	stack<int> st;
	for(int i=0;i<n;i++){
		dfs(i,adj,st,check);
	}
	vector<int> sorted;
	while(!st.empty()){
		sorted.push_back(st.top());
		st.pop();
	}
	return sorted;
}
```
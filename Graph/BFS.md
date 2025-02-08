For Adjacency List
```cpp
// Assume you already have the adjecent array
vector<int> bfs;
int check[n];
check[startingnode] =1;
queue<int> qu;
qu.push(startingnode);
while(!qu.empty()){
	int n  = qu.front();
	qu.pop();
	bfs.push_back(n);
	for(auto it:adj[n]){
		if(!check[it]){
			check[it]=1;
			qu.push(it);
		}
	}
}
```
For Adjacency matrix
```cpp
// Assume you have the matrix and r and c to start
int m  = matrix.size();
int n = matrix[0].size();
vector<vector<int>> check(m,vector<int>(n,0));
queue<pair<int,int>> qu;
qu.push({r,c});
check[r][c] = 1;
vector<int> dr = {-1,1,0,0};
vector<int> dc = {0,0,1,-1};
while(!qu.empty()){
int trow = qu.front().first;
int tcol = qu.front().second;
qu.pop();
for(int i=0;i<4;i++){
	int row = trow+dr[i];
	int col = tcol+dc[i];
	if(row>=0 && row<m && col>=0 && col<n && check[row][col]==0 && matrix[row][col]==1){
	check[row][col]=1;
	qu.push({row,col});
	}
}
}
```

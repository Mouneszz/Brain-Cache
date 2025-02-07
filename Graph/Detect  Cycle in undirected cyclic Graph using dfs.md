Intuition - As we already know dfs  same as finding cyclic in bfs 
```cpp

class Solution {
  private:
    bool dfs(int n,int parent,vector<int>& check,vector<vector<int>>& adj){
        check[n]=1;
        for(int i:adj[n]){
            if(check[i]!=1){
                if(dfs(i,n,check,adj)==true) return true;
            }
            else if(i!=parent){
                return true;
            }
            }
            return false;
        }
        
public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(vector<vector<int>>& adj) {
        int n=adj.size();
        vector<int> check(n,0);
        for(int i=0;i<n;i++){
            if(check[i]!=1){
            if(dfs(i,-1,check,adj)==true) return true;
        }
        }
        return false;
    }
};
```



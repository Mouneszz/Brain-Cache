Intuition -  as it is directed a node can have many paths  so we want to have a state
0 - Not processed
1 - Being Processed in this recursion cycle, if it occurs than cycle is present.
2 - if that n is completed then mark it as 2  so even checked and is 2 then that n has no cycles
```cpp
class Solution {

public:

    bool dfs(int n,vector<int>& check,vector<vector<int>>& adj){

        if(check[n]==1) return true;

        if(check[n]==2) return false;

        check[n]=1;

        for(int i:adj[n]){

            if(dfs(i,check,adj)) return true;

        }

        check[n]=2;

        return false;

    }

    bool canFinish(int num, vector<vector<int>>& pre) {

        vector<vector<int>> adj(num);

        for(auto p:pre){

            adj[p[1]].push_back(p[0]);

        }

        vector<int> check(num);

        for(int i=0;i<num;i++){

            if(check[i]==0 && dfs(i,check,adj)) return false;

        }

        return true;

    }

};
```

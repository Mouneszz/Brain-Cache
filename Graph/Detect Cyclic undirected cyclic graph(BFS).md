Intuition -  We know that in bfs we traverse level by level but when we meet a same element twice we use check array to check but in this case their previous nodes cannot form a cyclic so take previous node with you using a stack and do else if we that visited is not the parent then it is a cycle
```cpp
class Solution {
  private:
  bool detect(int n,vector<int>& check,vector<vector<int>>& adj){
      queue<pair<int,int>>qu;
      qu.push({n,-1});
      check[n]=1;
      while(!qu.empty()){
          int num = qu.front().first;
          int parent = qu.front().second;
          for(int i:adj[num]){
              if(check[i]!=1){
                  check[i]=1;
                  qu.push({i,num});
              }
              else if(i!=parent){
                  return true;
              }
          }
      }
      return false;
  }
    
  public:
    bool isCycle(vector<vector<int>>& adj) {
        int n = adj.size();
        vector<int> check(n,0);
        for(int i=0;i<n;i++){
            if(check[i]!=1){
                if(detect(i,check,adj)){
                   return true; 
                }
            }
        }
        return false;
    }
};
```
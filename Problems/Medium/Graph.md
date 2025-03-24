[All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)**
**Intuition  - As i already solved some dfs problems in tree and Combination sum with back tracking its easy for me.**
```cpp
class Solution {
public:
    void dfs(int start,vector<vector<int>>& graph,vector<vector<int>>&ans,unordered_map<int,bool>&check,vector<int>& path){

        if(start==graph.size()-1){

            ans.push_back(path);

        }

        for(int n:graph[start]){

            check[n]=1;

            path.push_back(n);

            dfs(n,graph,ans,check,path);

            path.pop_back();

            check[n]=0;

        }

    }

    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {

        vector<vector<int>> ans;

        unordered_map<int,bool> check;

        vector<int> path;

        check[0] = 1;

        path.push_back(0);

        dfs(0,graph,ans,check,path);

        return ans;

    }

};
```

**[547. Number of Provinces](https://leetcode.com/problems/number-of-provinces/)**
**Intuition -   as we already  learned  the graph traversal its quite easy but the logic we don't have the adjacent list to get to know their i th neighbors so we   create our own list** 
```cpp
class Solution {

public:

    void dfs(int start,vector<vector<int>>& adj,vector<int>& check){

        check[start] = 1;

        for(int n:adj[start]){

            if(!check[n])

            dfs(n,adj,check);

        }

    }

    int findCircleNum(vector<vector<int>>& isConnected) {

        int n = isConnected.size();

        int ans = 0;

        vector<vector<int>> adj(n);

        for(int i=0;i<n;i++){

            for(int j=0;j<n;j++){

                if(isConnected[i][j]==1 && i!=j){

                    adj[i].push_back(j);

                }

            }

        }

        vector<int> check(n, 0);

        for(int i=0;i<n;i++){

            if(!check[i]){

                ans++;

                dfs(i,adj,check);

            }

        }

        return ans;

    }

};
``` 
***Topology sort***

**IMPORTANT - Only can do for DAG(Directed Acyclic Graph)**
**Intuition -   This is a  new concept so we have to by heart this as so  now one thing in common like when we don't have the starting point to start a graph we just run a for loop for all i in n and do dfs to every thing  which are not visited and only add them to the stack when their loop  for the adj is finished** 
```cpp
//{ Driver Code Starts
#include <bits/stdc++.h>
using namespace std;


// } Driver Code Ends
class Solution {
  private:
     void dfs(int n,stack<int>& st,int vis[],vector<vector<int>>& adj){
         vis[n] = 1;
         for(int num:adj[n]){
             if(!vis[num]) dfs(num,st,vis,adj);
         }
         st.push(n);
     }
  public:
    // Function to return list containing vertices in Topological order.
    vector<int> topologicalSort(vector<vector<int>>& adj) {
        int n = adj.size();
        stack<int> st;
        int vis[n]={0};
        for(int i=0;i<n;i++){
            if(!vis[i]){
                dfs(i,st,vis,adj);
            }
        }
        vector<int> ans;
        while(!st.empty()){
            ans.push_back(st.top());
            st.pop();
        }
        return ans;
        // Your code here
    }
};
```
**[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)**
**Intuition - As we already learned the bfs its codable we are given a matrix of 0,1 first create a check vertices , and run double for loop for every indices which are not visited and its land**
**do count every one do dfs in where we have to check four sides so create a tow arrays for the 4 combinations . and push them into queue if they pass and make them as marked after that** 
```cpp
class Solution {

public:
    void bfs(int row,int col,vector<vector<int>>& check,vector<vector<char>>& grid){

        check[row][col] = 1;

        queue<pair<int,int>> qu;

        qu.push({row,col});

        int m = grid.size();

        int n = grid[0].size();

        while(!qu.empty()){

            int nrow = qu.front().first;

            int ncol = qu.front().second;

            qu.pop();

            int dr[] = {-1, 1, 0, 0};

            int dc[] = {0, 0, -1, 1};

            for(int i=0;i<4;i++){

                    int r = nrow+dr[i];

                    int c = ncol+dc[i];

                    if(r>=0 && r<m && c>=0 && c<n && check[r][c]==0 && grid[r][c]=='1'){

                        qu.push({r,c});

                        check[r][c] = 1;

                }

            }

        }

    }

    int numIslands(vector<vector<char>>& grid) {

        int m = grid.size();

        int n = grid[0].size();

        vector<vector<int>> check(m,vector<int>(n,0));

        int ans=0;

        for(int i=0;i<m;i++){

            for(int j=0;j<n;j++){

                if(check[i][j]==0 && grid[i][j]=='1'){

                    ans++;

                    bfs(i,j,check,grid);

                }

            }

        }

        return ans;

    }

};
```

**}**

**GFG - Flood fill algorithm** 
**Intuition - as we already solved the number of island and bfs its quite easy solved it without an explanation  we have a matrix with some random numbers as colors and given and col number and row number which have the start color index , in which we have to fill all the up down left right and which are same color to the start color with new color**

```cpp
using namespace std;

class Solution {
  public: 
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc,
                                  int newColor) {
        int m =image.size();
        int n =image[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        queue<pair<int,int>> qu;
        qu.push({sr,sc});
        check[sr][sc]=1;
        int color = image[sr][sc];
        image[sr][sc] = newColor;
        vector<int> dr = {-1,1,0,0};
        vector<int> dc = {0,0,-1,1};
        while(!qu.empty()){
            int tr = qu.front().first;
            int tc = qu.front().second;
            qu.pop();
            for(int i=0;i<4;i++){
                int row = tr+dr[i];
                int col = tc+dc[i];
                if(row>=0 && row<m && col>=0 && col<n && check[row][col]!=1 && image[row][col]==color){
                    check[row][col] =1;
                    image[row][col] = newColor;
                    qu.push({row,col});
                }
            }
        }
        return image;
    }
};
```

**[542. 01 Matrix](https://leetcode.com/problems/01-matrix/)**
**Intuition  -  So it was simple like others  we first store the indexes which have 0 and 0 as their step as  they are their nearest 0 like queue<pair<pair<int,int>,int> , create a visited matrix and do BFS store  their step as  their previous indexes step+1 and add them in every while loop.**
```cpp
class Solution {

public:

    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {

        int m = mat.size();

        int n = mat[0].size();

        vector<vector<int>> check(m,vector<int>(n,0));

        vector<vector<int>> ans(m,vector<int>(n,0));

        queue<pair<pair<int,int>,int>> qu;

        for(int i=0;i<m;i++){

            for(int j=0;j<n;j++){

                if(mat[i][j]==0){

                    qu.push({{i,j},0});

                    check[i][j]=1;

                }

            }

        }

  

        while(!qu.empty()){

            int i = qu.front().first.first;

            int j = qu.front().first.second;

            int step = qu.front().second;

            qu.pop();

            ans[i][j] = step;

            vector<int> dr = {-1,1,0,0};

            vector<int> dc  = {0,0,-1,1};

            for(int k=0;k<4;k++){

                int r = i+dr[k];

                int c = j+dc[k];

                if(r>=0 && r<m && c>=0 && c<n && check[r][c]!=1){

                        qu.push({{r,c},step+1});

                        check[r][c]=1;

                    }

                }

            }

        return ans;

    }

};
```
**[Course Schedule](https://leetcode.com/problems/course-schedule/)**
**Intuition -  we are given edges between course  in a directed way, so using this we create a adjacency  list , after that we create a visited array and use 1 and 2 variables as 2 means that course i already ready to be competed as it dont have any cycles if we occur somthing with it means that that is being processed so  we create a loop so return true and in main thread return  false is cycle is present.**
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

**[210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)**
**same as the above we detect the cycle by checking if the n is being processed and not finished but getting their second recursion call so we return true if  the for in main function we check for if that return true then return empty vector.**
```cpp
class Solution {

public:

    bool dfs(stack<int>& st,int n,vector<vector<int>>& adj,vector<int>& check){

        if(check[n]==1) return true;

        if(check[n]==2) return false;

        check[n] = 1;

        for(int i:adj[n]){

                if(dfs(st,i,adj,check)) return true;

        }

        st.push(n);

        check[n]=2;

        return false;

    }

    vector<int> findOrder(int num, vector<vector<int>>& pre) {

        vector<vector<int>> adj(num);

        for(auto p:pre){

            adj[p[1]].push_back(p[0]);

        }

        stack<int> st;

        vector<int> check(num,0);

        for(int i=0;i<num;i++){

            if(check[i]==0)

            if(dfs(st,i,adj,check)) return{};

        }

        vector<int> ans;

        while(!st.empty()){

            ans.push_back(st.top());

            st.pop();

        }

        return ans;

  

    }

};
```
**GFG - Replace "O" with "X".**
Intuition  - So it is similar to other matrix problems in array where we move to four directions which are not already went and(&&) which are with 'O' , move in dfs across  four cells and mark ,Finally do double loop and change 'O' with 'X' which are checked.
```cpp
class Solution {
  public:
    void dfs(int tr,int tc,vector<vector<int>>& check,vector<vector<char>>& mat){
       int m = mat.size();
       int n = mat[0].size();
       check[tr][tc]=1;
       vector<int> dr = {0,0,1,-1};
       vector<int> dc = {-1,1,0,0};
       for(int i=0;i<4;i++){
           int r = tr+dr[i];
           int c = tc+dc[i];
           if(r>=0 && r<m && c>=0 && c<n && mat[r][c]=='O' && check[r][c]!=1){
               dfs(r,c,check,mat);
           }
           
       }
      
    }
    vector<vector<char>> fill(vector<vector<char>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        for(int i =0;i<n;i++){
            //first row 
            if(!check[0][i] && mat[0][i]=='O'){
                dfs(0,i,check,mat);
            }
            //last row
            if(!check[m-1][i] && mat[m-1][i]=='O'){
                dfs(m-1,i,check,mat);
            }
        }
        
        for(int j=0;j<m;j++){
            if(!check[j][0] && mat[j][0]=='O'){
                dfs(j,0,check,mat);
            }
            if(!check[j][n-1] && mat[j][n-1]=='O'){
                dfs(j,n-1,check,mat);
            }
        }
        for(int i=0;i<m;i++){
            for(int j =0;j<n;j++){
                if(mat[i][j]=='O' && check[i][j]==0){
                    mat[i][j]='X';
                }
            }
        }
            return mat;
    }
};
```
GFG- Number of enclaves
Intuition -  It is just same as the above one one slight change is we count the '1' which are  not checked 
```cpp
class Solution {
  public:
    void dfs(int tr,int tc,vector<vector<int>>& check,vector<vector<int>>& grid){
        check[tr][tc]=1;
        int m = grid.size();
        int n = grid[0].size();
        vector<int> dr = {0,0,-1,1};
        vector<int> dc = {1,-1,0,0};
        for(int i=0;i<4;i++){
            int r = tr+dr[i];
            int c= tc+dc[i];
            if(r>=0 && r<m && c>=0 && c<n && check[r][c]!=1 && grid[r][c]==1){
                dfs(r,c,check,grid);
            }
        }
        
    }
    int numberOfEnclaves(vector<vector<int>> &grid) {
        int m = grid.size();
        int n = grid[0].size();
        //first row and last row
        vector<vector<int>>check(m,vector<int>(n,0));
        for(int j=0;j<n;j++){
            if(!check[0][j] && grid[0][j]==1){
                dfs(0,j,check,grid);
            }
            if(!check[m-1][j] && grid[m-1][j]==1){
                dfs(m-1,j,check,grid);
            }
        }
        //first col and last col
        for(int i=0;i<m;i++){
            if(!check[i][0] && grid[i][0]==1){
                dfs(i,0,check,grid);
            }
            if(!check[i][n-1] && grid[i][n-1]==1){
                dfs(i,n-1,check,grid);
            }
        }
        int ans=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==1 && check[i][j]==0) ans++;
            }
        }
        
        return ans;
    }
};
```
[2658. Maximum Number of Fish in a Grid](https://leetcode.com/problems/maximum-number-of-fish-in-a-grid/)
Intuition  -  Simple bfs do all four  directions  and  and add the sum,  return max form every starting point.
```cpp
class Solution {
private:
    int bfs(int tr,int tc,vector<vector<int>>& check,vector<vector<int>>& grid){
        int sum=grid[tr][tc];
        int m=grid.size();
        int n = grid[0].size();
        vector<int> dr = {0,0,-1,1};
        vector<int> dc = {-1,1,0,0};
        queue<pair<int,int>> qu;
        qu.push({tr,tc});
        check[tr][tc]=1;
        while(!qu.empty()){
            int r = qu.front().first;
            int c = qu.front().second;
            qu.pop();
            for(int i=0;i<4;i++){
                int row = r+dr[i]; 
                int col = c+dc[i];
                if(row>=0 && row<m && col>=0 && col<n && check[row][col]==0 && grid  [row][col]>0){
                qu.push({row,col});
                check[row][col]=1;
                sum+=grid[row][col];
                } 
            }
        }
        return sum;
    }
public:
    int findMaxFish(vector<vector<int>>& grid) {
        int ans=0;
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(check[i][j]!=1 && grid[i][j]>0){
                   ans = max(ans,bfs(i,j,check,grid));
                }
            }
        }
        return ans;

    }
};
```
GFG - ### Number of Distinct Islands
Intuition - Similar to the number of island where we check for every one and mark the adjacent ones in check vector, here we have to only tell the distinct which means it should be same as one island but i can be anywhere.
**So we need to something to store the shape we can match any of the islands by subtracting the base indices and push them into set so we can finally return the set size.**
```cpp
class Solution {
  private:
   void dfs(int tr,int tc,vector<pair<int,int>>& vec,vector<vector<int>>& check ,vector<vector<int>>& grid,int baser,int basec){
       check[tr][tc] =1;
       vec.push_back({tr-baser,tc-basec});
       int m = grid.size();
       int n = grid[0].size();
       vector<int> dr = {-1,1,0,0};
       vector<int> dc = {0,0,-1,1};
       for(int i=0;i<4;i++){
           int row = tr+dr[i];
           int col = tc+dc[i];
           if(row>=0 && row<m && col>=0 && col<n && check[row][col]==0 && grid[row][col]==1){
               dfs(row,col,vec,check,grid,baser,basec);
               
           }
       }
   }
  public:
    int countDistinctIslands(vector<vector<int>>& grid) {
        // code here
        int m = grid.size();
        int n = grid[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        set<vector<pair<int,int>>> st;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(!check[i][j] && grid[i][j]==1){
                    vector<pair<int,int>> vec;
                    dfs(i,j,vec,check,grid,i,j);
                    st.insert(vec);
                }
           }
        }
           return st.size();
    }
};
```
GFG - ### Bipartite Graph
Intuition - Similar to every other traversal we only return false if we have the same color as the parent, because it might be visited by other node
```cpp
class Solution {
  public:
    bool isBipartite(vector<vector<int>>& adj) {
    int m = adj.size();
    vector<int> check(m,-1);
    queue<int> qu;
    qu.push(0);
    check[0]=0;
    
    while(!qu.empty()){
        int n = qu.front();
        qu.pop();
        for(int i:adj[n]){
            if(check[i]==-1){
                qu.push(i);
                check[i]=!check[n];
            }
            else if(check[i]==check[n]){
                return false;
            }
        }
    }
    return true;
    }
};
```
[841. Keys and Rooms](https://leetcode.com/problems/keys-and-rooms/)
Intuition   -  here its  simple like other traversal just have to check the unvisited node if it is then it cannot be visit if we start from room 0.
```cpp
class Solution {
public:

    void dfs(int n,vector<int>& check,vector<vector<int>>& rooms){
        check[n]=1;
        for(int i:rooms[n]){
            if(check[i]!=1)
            dfs(i,check,rooms);
        }
    }
    bool canVisitAllRooms(vector<vector<int>>& rooms) {
        int n  = rooms.size();
        vector<int> check(n,0);
        dfs(0,check,rooms);
        for(int i=0;i<n;i++){
            if(check[i]==0) return false;
        }
        return true;
    }
};
```

[695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
Intuition: Similar to number of island just have to get the sum from from every one and return the max  of it.
```cpp
class Solution {
public:
    int helper(int i,int j,vector<vector<int>>& grid,vector<vector<int>>& check,int sum){
        int m = grid.size();
        int n = grid[0].size();
        check[i][j] =1;
        vector<int> dr ={0,0,1,-1};
        vector<int> dc ={1,-1,0,0};
        for(int k=0;k<4;k++){
            int row =i+dr[k];
            int col =j+dc[k];
            if(row>=0 && row<m && col>=0 && col<n && grid[row][col]==1 && check[row][col]==0){
                sum = helper(row,col,grid,check,sum+1);
            }
        }
        return sum;
        
    }
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int m =grid.size();
        int n = grid[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        int ans=0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==1 && check[i][j]==0)
                ans= max(ans,helper(i,j,grid,check,1));
            }
        }
        return ans;
    }
};
```

[994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)
Intuition : here its we  have to visit all adjacent cells of the rotten oranges `2` and mark the good oranges `1` as rotten oranges `2`  push them into queue , like normal bfs  a while loop is necessary
but in a single  iteration we should check all the rotten oranges at once so a for loop which  traverse from 0 to the size of the queue for every  position we go into the four directions to find the good orange and make it into rotten and push into queue.
```cpp
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        int cnt=0;
        int oranges =0;
        vector<vector<int>> check(m,vector<int>(n,0));
        queue<pair<int,int>> qu;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==2){
                    qu.push({i,j});
                    check[i][j]=1;
                }
                else if(grid[i][j]==1){
                    oranges++;
                }
            }
        }
        vector<int> dr = {-1,1,0,0};
        vector<int> dc = {0,0,-1,1};
        while(!qu.empty()){
            int size = qu.size();
            bool ischange=false;
            for(int i=0;i<size;i++){
            int r = qu.front().first;
            int c = qu.front().second;
            qu.pop();
            for(int i=0;i<4;i++){
                int row = r+dr[i];
                int col = c+dc[i];
                if(row>=0 && row<m && col>=0 && col<n && check[row][col]==0 && grid[row][col]==1){
                    qu.push({row,col});
                    grid[row][col] = 2;
                    check[row][col]=1;
                    ischange =true;
                    oranges--;
                }
            }
            }
            if(ischange) cnt++;
        }
        return (oranges==0)?cnt:-1;
    }
};
```
[1765. Map of Highest Peak](https://leetcode.com/problems/map-of-highest-peak/)
Intuition : normal like other bfs traversals first we push the cell with water and 0 as the indices pair, in the while loop we get the current step as the queue second (step)+1 and assign it in the answer push that to the queue, so we can get the max peak element.
```cpp
class Solution {
public:
    vector<vector<int>> highestPeak(vector<vector<int>>& water) {
        int m =water.size();
        int n =water[0].size();
        vector<vector<int>> check(m,vector<int>(n,0));
        queue<pair<pair<int,int>,int>> qu;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(water[i][j]==1){
                    water[i][j]=0;
                    qu.push({{i,j},0});
                    check[i][j] =1;
                }
            }
        }
        vector<int> dr ={1,-1,0,0};
        vector<int> dc ={0,0,-1,1};
        while(!qu.empty()){
            int r = qu.front().first.first;
            int c = qu.front().first.second;
            int step = qu.front().second;
            qu.pop();
            for(int i=0;i<4;i++){
                int row=r+dr[i];
                int col=c+dc[i];
                if(row>=0 && row<m && col>=0 && col<n && check[row][col]!=1){
                    water[row][col] = step+1;
                    check[row][col]=1;
                    qu.push({{row,col},step+1});
                }
            }
        }
        return water;
    }
};
```
[1020. Number of Enclaves](https://leetcode.com/problems/number-of-enclaves/)
Intuition : its simple we have to perform dfs for every 1 which are in the boundary and mark it as 0 and count the remaining 1 and return it.
```cpp
class Solution {
public:
    void dfs(int i,int j,vector<vector<int>>& grid){
        int m = grid.size();
        int n = grid[0].size();
        if(i<0 || i>=m || j<0 || j>=n || grid[i][j]!=1) return;
        grid[i][j] =0;
        dfs(i+1,j,grid);
        dfs(i-1,j,grid);
        dfs(i,j+1,grid);
        dfs(i,j-1,grid);
    }
    int numEnclaves(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        int cnt=0;
        for(int i=0;i<m;i++){
            if(grid[i][0]==1)
            dfs(i,0,grid);
        }
        for(int i=0;i<m;i++){
            if(grid[i][n-1]==1)
            dfs(i,n-1,grid);
        }
        for(int j=0;j<n;j++){
            if(grid[0][j]==1)
            dfs(0,j,grid);
        }
        for(int j=0;j<n;j++){
            if(grid[m-1][j]==1)
            dfs(m-1,j,grid);
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j]==1) cnt++;
            }
        }
        return cnt;
    }
};
```
[2685. Count the Number of Complete Components](https://leetcode.com/problems/count-the-number-of-complete-components/)
Intuition: For a graph component to complete component the edges should  be equal to k(k-1)/2.
k=nodes.
```cpp
class Solution {
public:
    void dfs(int i,vector<vector<int>>& adj,vector<int>& check,int& node,int& edge){
        if(check[i]==1) return;
        check[i]=1;
        node++;
        for(int num:adj[i]){
            edge++;
            if(check[num]==0){
            dfs(num,adj,check,node,edge);
            }
        }
    }
    int countCompleteComponents(int n, vector<vector<int>>& edges) {
        vector<int> check(n,0);
        int ans=0;
        vector<vector<int>> adj(n);
        for(vector<int> num:edges){
            adj[num[0]].push_back(num[1]);
            adj[num[1]].push_back(num[0]);
        }
        for(int i=0;i<n;i++){
            
            if(check[i]==0){
                int node=0,edge=0;
                dfs(i,adj,check,node,edge);
                edge/=2;
                if(edge==(node*(node-1)/2)){
                ans++;
            }
            }
        }
        return ans;
    }
};
```
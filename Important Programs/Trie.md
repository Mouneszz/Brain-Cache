[212. Word Search II](https://leetcode.com/problems/word-search-ii/)
#trie 
Intuition:
Its a hard problem so in this we have to solve  multiple problems the 
- first one is we have to create a `trie` and insert every word into the root.
- and do a tow for loop to find if the any characters in the matrix is a children `Trienode` of the root.
- if it is then pass the row and col , root to a helper function and also have a duplicate gird to make changes and undo them.
- in helper make the `newgrid[row][col]='#'` and undo after the recursion ends in the specific function.
- in helper check if the `curr` which is the `root` children `trienode`. if it have the word. if it is then it means that it is the final character of the depth so add that to the answer. 
- prune the current `trienode` after completing its four directions traversal, check if that current dont have any children than clear its `root->mpp`.
```cpp
class TrieNode{
public:
    unordered_map<char,TrieNode*> mpp;
    string word = "";
    TrieNode(){
        
    }
};
class Solution {
public:
    vector<vector<char>> fullboard;
    vector<string> ans;
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        TrieNode* root = new TrieNode();
        for(string word:words){
            TrieNode* node = root;
            for(char ch:word){
                if(node->mpp.count(ch)){
                    node = node->mpp[ch];
                }
                else{
                    node->mpp[ch] = new TrieNode();
                    node = node->mpp[ch];
                }
            }
            node->word = word;
        }
        fullboard = board;
        for(int r=0;r<board.size();r++){
            for(int c=0;c<board[0].size();c++){
                if(root->mpp.count(board[r][c])){
                    helper(root, r, c);
                }
            }
        }
        return ans;
    }
        void helper(TrieNode* root,int r,int c){
            if(root==nullptr) return;
            char letter =  fullboard[r][c];
            TrieNode* curr = root->mpp[letter];
            if(curr==nullptr) return;
            if(curr->word!=""){
                ans.push_back(curr->word);
                curr->word = "";
            }
            fullboard[r][c] = '#';
            vector<int> dr = {0,0,-1,1};
            vector<int> dc = {-1,1,0,0};
            for(int i=0;i<4;i++){
                int row = r+dr[i];
                int col = c+dc[i];
                if(row<0 || row>=fullboard.size() || col<0 || col>=fullboard[0].size()){
                    continue;
                }
                if(curr->mpp.count(fullboard[row][col])){
                    helper(curr,row,col);
                }
            }
            fullboard[r][c] = letter;
            if (curr->mpp.empty()) {
            root->mpp.erase(letter);
        }
        }
};
```
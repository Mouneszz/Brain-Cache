```cpp
void levelorder(vector<vector<int>>& levels,Treenode* root){
queue<Treenode*> qu;
if(root==nullptr) return;
qu.push(root);
while(!qu.empty()){
	int n = qu.size();
	vector<int> level;
	for(int i=0;i<size;i++){
	Treenode* node = qu.front();
	qu.pop();
	if(node->left!=nullptr) qu.push(node->left);
	if(node->right!=nullptr) qu.push(node->right);
	level.push_back(node->val);
	}
	levels.push_back(level);
}
}
```
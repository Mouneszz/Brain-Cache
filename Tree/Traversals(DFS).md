Preorder Traversal
```cpp
void preorder(Treenode* root){
	if(root==nullptr) return;
	cout<<root->val;
	preorder(root->left);
	preorder(root->right);

}
```
Inorder Traversal
```cpp
void inorder(Treenode* root){
	if(root==nullptr) return;
	inorder(root->left);
	cout<<root->val;
	inorder(root->right);

}
```
Postorder Traversal
```cpp
void postorder(Treenode* root){
if(root==nullptr) return;
postorder(root->left);
postorder(root->right);
cout<<root->val;
}
```


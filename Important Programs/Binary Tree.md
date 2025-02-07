[226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
#binarytree
Intuition :  In this problem its simple just use recursion and swap them from bottom up.
```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root==nullptr)
        return root;
        TreeNode* right = invertTree(root->right);
        TreeNode* left = invertTree(root->left);
        root->left =right;
        root->right = left;
        return root;
    }
};
```
[104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
#binarytree 
Intuition : Normal recursion with base but add 1 for it  own depth.
```cpp
class Solution{
public:
	int  depth(TreeNode* root){
		if(root==nullptr) return 0;
		int left = depth(root->left);
		int right = depth(root->right);
		return max(left,right)+1;
	}
}
```
[572. Subtree of Another Tree](https://leetcode.com/problems/subtree-of-another-tree/)
Intuition  -  Here is similar to the same tree problem just have to check for every other node and the subtree 
```cpp
class Solution {
public:
    bool issame(TreeNode* root,TreeNode* subRoot){
        if(root == nullptr && subRoot == nullptr) return true;
        if(root == nullptr || subRoot == nullptr) return false;
        if(root->val !=subRoot->val) return false;

        return issame(root->left,subRoot->left) && issame(root->right,subRoot->right);


    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(root==nullptr) return false;
        if(issame(root,subRoot)) return true;
        return isSubtree(root->left,subRoot) || isSubtree(root->right,subRoot);
    }
};
```
[235. Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)
Intuition: So here we have to check if the root value is greater than both value, if it is pass the function but with root of right. Both smaller than the root value than pass the function but with root of left. if both cases failed it means either the root value is similar to either one of the value or its between those so it is the lowest  common Ancestor.
```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        int rootval = root->val;
        int pval = p->val;
        int qval = q->val;
        if(pval> rootval && qval>rootval){
            return lowestCommonAncestor(root->right,p,q);
        }
        if(pval<rootval && qval<rootval){
            return lowestCommonAncestor(root->left,p,q);
        }
        return root;
    }
};
```
[1448. Count Good Nodes in Binary Tree](https://leetcode.com/problems/count-good-nodes-in-binary-tree/)
Intuition : Normal like other problems  have a base case which return from the recursion call and have a  two path recursion which have the maxi from its path we calculate the maxi by finding the max of the maxi , root->value .
```cpp

```

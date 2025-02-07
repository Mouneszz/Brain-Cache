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
class Solution {
public:
    int count=0;
    void good(TreeNode* root,int maxi){
        if(root==nullptr) return;
        if(root->val>=maxi) count++;
        good(root->left,max(maxi,root->val));
        good(root->right,max(maxi,root->val));
    }
    int goodNodes(TreeNode* root) {
        good(root,root->val);
        return count;
    }
};
```
[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)
Intuition: here what we simply check if the binary tree is valid or not pass to helper function max ,min, root. the root value should be greater than the minimum and lesser than the maximum if not than return false also ,return true if root == `nullptr`. and return a  `&&` for two function when we go to left, the maximum will become the root value , for the right the min become root value.
```cpp
class Solution {
public:
    bool check(TreeNode* root,long min,long max){
        if(root == nullptr) return true;
        if(root->val<=min || root->val>=max) return false;
        return check(root->right,root->val,max) && check(root->left,min,root->val);
    }
    bool isValidBST(TreeNode* root) {
        return check(root,LONG_MIN,LONG_MAX);
    }
};
```
[230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)
Intuition -  When ever we comeback from a left sub tree call we count++ if that count reaches k we simply  assign answer the current root value because it is the kth smallest element  . do this inside the preorder skeleton code.
```cpp
class Solution {
public:
    int count=0;
    int ans;
    void inorder(TreeNode* root,int k) {
        if (!root) return;
        inorder(root->left,k);
        count++;
        if(count==k) ans =root->val;
        inorder(root->right,k);
    }

    int kthSmallest(TreeNode* root, int k) {
        inorder(root,k);
        return ans;
    }
};

```
[105. Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
Intuition: So here we have give `inorder` and `preorder` 
- The first step is to realize that in preorder the first element will always be the root node.
- The left subarray from zero to the first element (of preorder). will always be the left subtree in the `inorder` to the root .
```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        map<int,int> mpp;
        for(int i=0;i<inorder.size();i++){
            mpp[inorder[i]]=i;
        }
        TreeNode* root = build(preorder,0,preorder.size()-1,inorder,0,inorder.size(),mpp);
        return root;
    }
    TreeNode* build(vector<int>& preorder,int pst,int ped,vector<int>& inorder,int ist,int ied,map<int,int>& mpp){
        if(pst>ped || ist>ied) return nullptr;
        TreeNode* root = new TreeNode(preorder[pst]);
        int inroot = mpp[root->val];
        int nleft = inroot -ist;
        root->left = build(preorder,pst+1,pst+nleft,inorder,ist,inroot-1,mpp);
        root->right = build(preorder,pst+nleft+1,ped,inorder,inroot+1,ied,mpp);
        return root;
    }
};
```
[124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)
Intuition: In this problem we have to calculate  the max path so we have to keep and pass a maxi value  which will update in every recursion and also have to return the root value and max of(left and right). in that way the max value is calculated by adding the root value and the left and right max value we finally only return the max value we passed.
```cpp
class Solution {
public:
    int maxpath(TreeNode* root,int& maxi){
        if(root==nullptr){
            return 0;
        }
        int l = max(0,maxpath(root->left,maxi));
        int r = max(0,maxpath(root->right,maxi));
        maxi = max(maxi,root->val+l+r);
        return root->val+max(l,r);
    }
    int maxPathSum(TreeNode* root) {
        int maxi=INT_MIN;
        maxpath(root,maxi);
        return maxi;
    }
};
```

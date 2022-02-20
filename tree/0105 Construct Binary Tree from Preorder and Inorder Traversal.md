# 105. Construct Binary Tree from Preorder and Inorder Traversal
https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/  
Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154846727-1d7d50c1-69cd-45d5-b38b-899bcaf76457.png)  
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]  
Output: [3,9,20,null,null,15,7]  

Example 2:  
Input: preorder = [-1], inorder = [-1]  
Output: [-1]  

Constraints:  
1 <= preorder.length <= 3000  
inorder.length == preorder.length  
-3000 <= preorder[i], inorder[i] <= 3000  
preorder and inorder consist of unique values.  
Each value of inorder also appears in preorder.  
preorder is guaranteed to be the preorder traversal of the tree.  
inorder is guaranteed to be the inorder traversal of the tree.  

``` cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    unordered_map<int,int> index;
    TreeNode* myBuildTree(const vector<int>& preorder, const vector<int>& inorder, int pre_left,int pre_right, int in_left, int in_right){
        if (pre_left>pre_right) return nullptr;
        int pre_root=pre_left;
        int in_root=index[preorder[pre_root]];
        TreeNode* root = new TreeNode(preorder[pre_root]);
        int left_size=in_root-in_left;
        root->left=myBuildTree(preorder,inorder,pre_root+1,pre_root+left_size,in_left,pre_root-1);
        root->right=myBuildTree(preorder,inorder,pre_root+left_size+1,pre_right,in_root+1,in_right);
        return root;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int n=preorder.size();
        for (int i=0; i<n; i++) index[inorder[i]]=i;
        return myBuildTree(preorder,inorder,0,n-1,0,n-1);
    }
};
```

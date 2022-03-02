# 236. Lowest Common Ancestor of a Binary Tree
https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/  
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.  

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/156284015-882b60e2-a789-4257-926f-db5cd2cfce1c.png)  
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1  
Output: 3  
Explanation: The LCA of nodes 5 and 1 is 3.  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/156284087-d91becdd-79c2-4108-876e-333ae6a090ab.png)  
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4  
Output: 5  
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.  

Example 3:  
Input: root = [1,2], p = 1, q = 2  
Output: 1  

Constraints:  
The number of nodes in the tree is in the range [2, 10^5].  
-10^9 <= Node.val <= 10^9  
All Node.val are unique.  
p != q  
p and q will exist in the tree.  

``` cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root==nullptr || root==p|| root==q) return root;
        TreeNode* lnode=lowestCommonAncestor(root->left,p,q);
        TreeNode* rnode=lowestCommonAncestor(root->right,p,q);
        if (lnode==nullptr) return rnode;
        if (rnode==nullptr) return lnode;
        return root;
    }
};
```

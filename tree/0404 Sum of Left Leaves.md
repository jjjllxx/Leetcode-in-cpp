# 404. Sum of Left Leaves
https://leetcode-cn.com/problems/sum-of-left-leaves/  
Given the root of a binary tree, return the sum of all left leaves.  

Example 1:  
Input: root = [3,9,20,null,null,15,7]  
Output: 24  
Explanation: There are two left leaves in the binary tree, with values 9 and 15 respectively.  

Example 2:  
Input: root = [1]  
Output: 0  

Constraints:  
The number of nodes in the tree is in the range [1, 1000].  
-1000 <= Node.val <= 1000  

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
    int ans=0;
    void dfs(TreeNode* root){
        if (root->left!=nullptr && root->left->left==nullptr && root->left->right==nullptr) {
            ans+=root->left->val;
        }
        if (root->left!=nullptr) dfs(root->left);
        if (root->right!=nullptr) dfs(root->right);
    }
    int sumOfLeftLeaves(TreeNode* root) {
        dfs(root);
        return ans;
    }
};
```

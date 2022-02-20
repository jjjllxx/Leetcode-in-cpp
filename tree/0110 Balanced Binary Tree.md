# 110. Balanced Binary Tree
https://leetcode-cn.com/problems/balanced-binary-tree/  
Given a binary tree, determine if it is height-balanced.  
For this problem, a height-balanced binary tree is defined as:  
a binary tree in which the left and right subtrees of every node differ in height by no more than 1.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154847015-15191d4c-e48c-42bb-ac27-bc8f7e10dc89.png)  
Input: root = [3,9,20,null,null,15,7]  
Output: true  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/154847032-42a5bf98-ca58-414e-bb4e-7a9f0f6d2839.png)  
Input: root = [1,2,2,3,3,null,null,4,4]  
Output: false  

Example 3:  
Input: root = []  
Output: true  

Constraints:  
The number of nodes in the tree is in the range [0, 5000].  
-10^4 <= Node.val <= 10^4  

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
    int height(TreeNode* node){
        if (node==nullptr) return 0;
        return max(height(node->left),height(node->right))+1;
    }
    bool isBalanced(TreeNode* root) {
        if (root==nullptr) return true;
        return abs(height(root->left)-height(root->right))<=1 && isBalanced(root->left) && isBalanced(root->right);
    }
};
```

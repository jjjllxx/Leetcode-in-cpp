# 113. Path Sum II
Given the root of a binary tree and an integer targetSum, return all root-to-leaf paths where the sum of the node values in the path equals targetSum. Each path should be returned as a list of the node values, not node references.
A root-to-leaf path is a path starting from the root and ending at any leaf node. A leaf is a node with no children.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154854218-ae7ba0d7-f8e5-4c5d-bdcf-f6ede50a2afc.png)  
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22  
Output: [[5,4,11,2],[5,8,4,5]]  
Explanation: There are two paths whose sum equals targetSum:  
5 + 4 + 11 + 2 = 22  
5 + 8 + 4 + 5 = 22  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/154854186-4265d969-7182-4626-b8a3-57571a80096b.png)  
Input: root = [1,2,3], targetSum = 5  
Output: []  

Example 3:  
Input: root = [1,2], targetSum = 0  
Output: []  

Constraints:  
The number of nodes in the tree is in the range [0, 5000].  
-1000 <= Node.val <= 1000  
-1000 <= targetSum <= 1000  

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
    vector<int> stk;
    vector<vector<int>> ans;

    void backtrack(TreeNode*node, int targetSum){
        if (targetSum==0 && node->right==nullptr && node->left==nullptr){
            ans.emplace_back(stk);
            return;
        }
        if (node->left!=nullptr){
            stk.emplace_back(node->left->val);
            backtrack(node->left,targetSum-node->left->val);
            stk.pop_back();
        }
        if (node->right!=nullptr){
            stk.emplace_back(node->right->val);
            backtrack(node->right,targetSum-node->right->val);
            stk.pop_back();
        }
        
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        if (root==nullptr) return {};
        stk.emplace_back(root->val);
        backtrack(root,targetSum-root->val);
        return ans;
    }
};
```

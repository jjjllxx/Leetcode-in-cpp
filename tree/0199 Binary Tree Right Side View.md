# 199. Binary Tree Right Side View
https://leetcode-cn.com/problems/binary-tree-right-side-view/  
Given the root of a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/155825946-58c326b6-29a3-49e5-b8e3-75ca30be20c0.png)  
Input: root = [1,2,3,null,5,null,4]  
Output: [1,3,4]  

Example 2:  
Input: root = [1,null,3]  
Output: [1,3]  

Example 3:  
Input: root = []  
Output: []  

Constraints:  
The number of nodes in the tree is in the range [0, 100].  
-100 <= Node.val <= 100  

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
    vector<int> rightSideView(TreeNode* root) {
        if (root==nullptr) return {};
        vector<TreeNode*> mp,tmp;
        vector<int> ans;
        mp.push_back(root);
        while (!mp.empty()){
            tmp.clear();
            ans.push_back(mp[mp.size()-1]->val);
            for(int i=0;i<mp.size();i++){
                if (mp[i]->left!=nullptr) tmp.push_back(mp[i]->left);
                if (mp[i]->right!=nullptr) tmp.push_back(mp[i]->right);
            }
            mp=tmp;
        }
        return ans;
    }
};
```

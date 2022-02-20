# 103. Binary Tree Zigzag Level Order Traversal
Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/154846408-c5115310-d48a-46b3-ac90-cc10dd968f71.png)  
Input: root = [3,9,20,null,null,15,7]  
Output: [[3],[20,9],[15,7]]  

Example 2:  
Input: root = [1]  
Output: [[1]]  

Example 3:  
Input: root = []  
Output: []  

Constraints:  
The number of nodes in the tree is in the range [0, 2000].  
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (root==nullptr) return {};
        vector<vector<int>> ans;
        vector<int> value;
        vector<TreeNode*> mp,tmp;
        int layer=1;
        value.push_back(root->val);
        mp.push_back(root);
        while(!mp.empty()){
            ans.push_back(value);
            value.clear();
            if (layer%2==1){
                for(int i=mp.size()-1;i>=0;i--){
                    if (mp[i]->right!=nullptr){
                        tmp.push_back(mp[i]->right);
                        value.push_back(mp[i]->right->val);
                    }
                    if (mp[i]->left!=nullptr){
                        tmp.push_back(mp[i]->left);
                        value.push_back(mp[i]->left->val);
                    }
                    
                }
            }
            else{
                for (int i=mp.size()-1;i>=0;i--){
                    if (mp[i]->left!=nullptr){
                        tmp.push_back(mp[i]->left);
                        value.push_back(mp[i]->left->val);
                    }
                    if (mp[i]->right!=nullptr){
                        tmp.push_back(mp[i]->right);
                        value.push_back(mp[i]->right->val);
                    }    
                }

            }
            layer++;
            mp=tmp;
            tmp.clear();
        }
        return ans;
    }
};
```

# 230. Kth Smallest Element in a BST
https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/  
Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.  

Example 1:  
![image](https://user-images.githubusercontent.com/60777462/156282133-69211e3b-74ab-43e4-881b-ec0c75c6f410.png)  
Input: root = [3,1,4,null,2], k = 1  
Output: 1  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/156282152-ff4db2db-c5ec-42b3-9a03-a5f90a306bed.png)  
Input: root = [5,3,6,2,4,null,null,1], k = 3  
Output: 3  

Constraints:  
The number of nodes in the tree is n.  
1 <= k <= n <= 10^4  
0 <= Node.val <= 10^4  

Follow up: If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?  

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
    int pos,ans;
    void inorder(TreeNode* root){
        if (root==nullptr) return;
        inorder(root->left);
        pos--;
        if (pos==0) ans=root->val;
        inorder(root->right);
    }
    int kthSmallest(TreeNode* root, int k) {
        pos=k;
        inorder(root);
        return ans;
    }
};
```

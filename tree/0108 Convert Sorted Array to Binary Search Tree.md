# 108. Convert Sorted Array to Binary Search Tree
Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.    
A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.    

Example 1:    
![image](https://user-images.githubusercontent.com/60777462/154846899-bdb367fe-cfe9-491b-ba7d-444612f3ba38.png)  
Input: nums = [-10,-3,0,5,9]  
Output: [0,-3,9,-10,null,5]  
Explanation: [0,-10,5,null,-3,null,9] is also accepted:  
![image](https://user-images.githubusercontent.com/60777462/154846920-3f45c830-adac-41ed-b188-8478fa7050f0.png)  

Example 2:  
![image](https://user-images.githubusercontent.com/60777462/154846937-072b6c18-06c6-4605-aadd-8ef68838317d.png)  
Input: nums = [1,3]  
Output: [3,1]  
Explanation: [1,3] and [3,1] are both a height-balanced BSTs.  

Constraints:  
1 <= nums.length <= 10^4  
-10^4 <= nums[i] <= 10^4  
nums is sorted in a strictly increasing order.  

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return helpler(nums,0,nums.size()-1);
    }
    TreeNode* helpler(vector<int>& nums, int left,int right){
        
        if (left>right) return nullptr;

        int mid=(left+right+rand()%2)/2;

        TreeNode* root= new TreeNode(nums[mid]);
        root->left=helpler(nums,left,mid-1);
        root->right=helpler(nums,mid+1,right);
        return root;
    }
};
```

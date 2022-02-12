# 46. Permutations
https://leetcode-cn.com/problems/permutations   
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.  

Example 1:  
Input: nums = [1,2,3]  
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  

Example 2:  
Input: nums = [0,1]  
Output: [[0,1],[1,0]]  

Example 3:  
Input: nums = [1]  
Output: [[1]]  
 

Constraints:  
1 <= nums.length <= 6  
-10 <= nums[i] <= 10  
All the integers of nums are unique.  

``` cpp
class Solution {
public:
    vector<vector<int>> ans;
    void backtrack(vector<int>& stk, int first,int len){
        if (first==len) {
            ans.emplace_back(stk);
            return;
        }
        for(int i=first;i<len;i++){
            swap(stk[first],stk[i]);
            backtrack(stk,first+1,len);
            swap(stk[first],stk[i]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        backtrack(nums,0,nums.size());
        return ans;
    }
};
```

# 90. Subsets II
https://leetcode-cn.com/problems/subsets-ii/   
Given an integer array nums that may contain duplicates, return all possible subsets (the power set).  
The solution set must not contain duplicate subsets. Return the solution in any order.  

Example 1:   
Input: nums = [1,2,2]  
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]  

Example 2:  
Input: nums = [0]  
Output: [[],[0]]  

Constraints:  
1 <= nums.length <= 10  
-10 <= nums[i] <= 10  

``` cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> stk;

    void backtrack(bool pre,vector<int>& nums, int cur){
        if (cur==nums.size()){
            ans.push_back(stk);
            return;
        }
        backtrack(false,nums,cur+1);  
        if (!pre && cur>0 && nums[cur-1]==nums[cur]) return;
        stk.push_back(nums[cur]);
        backtrack(true,nums,cur+1);
        stk.pop_back();
        
    }

    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        backtrack(false,nums,0);
        return ans;
    }
};
```

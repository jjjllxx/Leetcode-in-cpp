# 78. Subsets
https://leetcode-cn.com/problems/subsets  
Given an integer array nums of unique elements, return all possible subsets (the power set).  
The solution set must not contain duplicate subsets. Return the solution in any order.  

Example 1:  
Input: nums = [1,2,3]  
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]  

Example 2:  
Input: nums = [0]  
Output: [[],[0]]  

Constraints:  
1 <= nums.length <= 10  
-10 <= nums[i] <= 10  
All the numbers of nums are unique.  

``` cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> stk;

    void backtrack(vector<int>& nums, int cur){
        if (cur==nums.size()){
            ans.push_back(stk);
            return;
        }
        stk.push_back(nums[cur]);
        backtrack(nums,cur+1);
        stk.pop_back();
        backtrack(nums,cur+1);  
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        backtrack(nums,0);
        return ans;
    }
};
```

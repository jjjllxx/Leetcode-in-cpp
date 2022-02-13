# 47. Permutations II
https://leetcode-cn.com/problems/permutations-ii  
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.  

Example 1:  
Input: nums = [1,1,2]  
Output:  
[[1,1,2],  
 [1,2,1],  
 [2,1,1]]  
 
Example 2:  
Input: nums = [1,2,3]  
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]  
 

Constraints:  
1 <= nums.length <= 8  
-10 <= nums[i] <= 10  

``` cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> visited;
    vector<int> stk;

    void backtrack(vector<int>& nums, int first){
        if (first==nums.size()){
            ans.emplace_back(stk);
            return;
        }
        for(int i=0; i<nums.size(); i++){
            if (visited[i] || i>0 && nums[i-1]==nums[i] && !visited[i-1]) continue;
            stk.emplace_back(nums[i]);
            visited[i]=1;
            backtrack(nums,first+1);
            stk.pop_back();
            visited[i]=0;
        }
    }
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        visited.resize(nums.size());
        backtrack(nums,0);
        return ans;
    }
};
```

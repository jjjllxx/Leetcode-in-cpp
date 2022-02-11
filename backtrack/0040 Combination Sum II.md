# 40. Combination Sum II
https://leetcode-cn.com/problems/combination-sum-ii   
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.  
Each number in candidates may only be used once in the combination.  
Note: The solution set must not contain duplicate combinations.  

Example 1:  
Input: candidates = [10,1,2,7,6,1,5], target = 8  
Output:   
[  
[1,1,6],  
[1,2,5],  
[1,7],  
[2,6]  
]  

Example 2:  
Input: candidates = [2,5,2,1,2], target = 5  
Output:   
[  
[1,2,2],  
[5]  
]  
 
Constraints:  
1 <= candidates.length <= 100  
1 <= candidates[i] <= 50  
1 <= target <= 30  

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> stk;

    void backtrack(vector<int>& candidates, int target, int idx){
        if (target==0){
            ans.emplace_back(stk);
            return;
        }
        for(int i=idx; i<candidates.size() && candidates[i]<=target; i++){
            if (i>idx && candidates[i]==candidates[i-1]) continue;
            stk.emplace_back(candidates[i]);
            backtrack(candidates,target-candidates[i],i+1);
            stk.pop_back();
        }    
    }

    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        backtrack(candidates,target,0);
        return ans;
    }
};
```

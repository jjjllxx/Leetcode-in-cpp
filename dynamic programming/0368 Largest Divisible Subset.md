# 368. Largest Divisible Subset
https://leetcode-cn.com/problems/largest-divisible-subset/  
Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:

answer[i] % answer[j] == 0, or  
answer[j] % answer[i] == 0  
If there are multiple solutions, return any of them.  

Example 1:  
Input: nums = [1,2,3]  
Output: [1,2]  
Explanation: [1,3] is also accepted.  

Example 2:  
Input: nums = [1,2,4,8]  
Output: [1,2,4,8]  

Constraints:  
1 <= nums.length <= 1000  
1 <= nums[i] <= 2 * 10^9  
All the integers in nums are unique.

``` cpp
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n=nums.size(),maxn=0,maxl=0;
        vector<int> dp(n,0);
        for(int i=0;i<n;i++){
            for(int j=i;j>=0;j--){
                if (nums[i]%nums[j]==0){
                    dp[i]=max(dp[i],dp[j]+1);
                }    
            }
            if(dp[i]>maxl){
                maxl=dp[i];
                maxn=nums[i];
            }
        }
        vector<int> ans;
        for(int i=n-1;i>=0;i--){
            if (maxn%nums[i]==0 && dp[i]==maxl){
                maxl--;
                maxn=nums[i];
                ans.emplace_back(nums[i]);
            }
        }
        reverse(ans.begin(),ans.end());
        return ans;

    }
};
```

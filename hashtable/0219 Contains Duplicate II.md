# 219. Contains Duplicate II
https://leetcode-cn.com/problems/contains-duplicate-ii/  
Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.  

Example 1:  
Input: nums = [1,2,3,1], k = 3  
Output: true  

Example 2:  
Input: nums = [1,0,1,1], k = 1  
Output: true  

Example 3:   
Input: nums = [1,2,3,1,2,3], k = 2  
Output: false  

Constraints:  
1 <= nums.length <= 10^5  
-10^9 <= nums[i] <= 10^9  
0 <= k <= 10^5  

``` cpp
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int,int> pos;
        int n=nums.size();
        for(int i=0;i<n;i++){
            if (pos.find(nums[i])!=pos.end() && i-pos[nums[i]]<=k) return true;
            pos[nums[i]]=i;
        }
        return false;
    }
};
```

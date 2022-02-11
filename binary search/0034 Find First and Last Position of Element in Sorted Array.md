# 34. Find First and Last Position of Element in Sorted Array
https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array  
Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value.  

If target is not found in the array, return [-1, -1].  

You must write an algorithm with O(log n) runtime complexity.  


Example 1:  
Input: nums = [5,7,7,8,8,10], target = 8  
Output: [3,4]  

Example 2:  
Input: nums = [5,7,7,8,8,10], target = 6  
Output: [-1,-1]  

Example 3:  
Input: nums = [], target = 0  
Output: [-1,-1]  

Constraints:
0 <= nums.length <= 105  
-109 <= nums[i] <= 109  
nums is a non-decreasing array.  
-109 <= target <= 109  

``` cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if (nums.size()==0) return {-1,-1};
        int left=0, right=nums.size()-1;
        int middle=(right-left)/2+left;
        while (left<=right){
            middle=(right-left)/2+left;
            if (nums[middle]==target) break;
            if (nums[middle]<target) left=middle+1;
            else right=middle-1;
        }
        if (nums[middle]!=target) return {-1,-1};
        left=middle;right=middle;
        while (left>=0 && nums[left]==target) left--;
        while (right<nums.size() && nums[right]==target) right++;
        return {left+1,right-1};
    }
};
```

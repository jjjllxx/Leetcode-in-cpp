# 56. Merge Intervals
https://leetcode-cn.com/problems/merge-intervals  
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

Example 1:  
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]  
Output: [[1,6],[8,10],[15,18]]  
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].  

Example 2:  
Input: intervals = [[1,4],[4,5]]  
Output: [[1,5]]  
Explanation: Intervals [1,4] and [4,5] are considered overlapping.  

Constraints:  
1 <= intervals.length <= 10^4  
intervals[i].length == 2  
0 <= starti <= endi <= 10^4  

``` cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.size()==0) return {};
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        ans.emplace_back(intervals[0]);
        for(vector<int> interval:intervals){
            if (interval[0]<=ans.back()[1]){
                ans.back()[1]=max(ans.back()[1],interval[1]);
            }
            else ans.emplace_back(interval);
        }
        return ans;
    }
};
```

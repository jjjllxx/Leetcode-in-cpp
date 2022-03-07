# 347. Top K Frequent Elements
https://leetcode-cn.com/problems/top-k-frequent-elements/  
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.  

Example 1:  
Input: nums = [1,1,1,2,2,3], k = 2  
Output: [1,2]  

Example 2:  
Input: nums = [1], k = 1  
Output: [1]  
 
Constraints:  
1 <= nums.length <= 10^5  
k is in the range [1, the number of unique elements in the array].  
It is guaranteed that the answer is unique.  

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.  

``` cpp
class Solution {
public:
    static bool cmp(pair<int,int>& m, pair<int,int>& n) {
        return m.second>n.second;
    }
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> fre;
        for(auto& k:nums) fre[k]++;
        priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(&cmp)> q(cmp);
        for(auto& [num,count]:fre){
            if (q.size()==k){
                if (q.top().second<count){
                    q.pop();
                    q.emplace(num,count);
                }
            }
            else{
                q.emplace(num,count);
            }
        }
        vector<int> ans;
        while(!q.empty()){
            ans.emplace_back(q.top().first);
            q.pop();
        }
        return ans;
    }
};
```
